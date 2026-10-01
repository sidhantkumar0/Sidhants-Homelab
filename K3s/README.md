# K3s Cluster Services

What runs on the 4-node K3s cluster (pi-server3 = server, pi-server1/2/4 = agents) beyond the base install. Hardware and cluster build notes live in [`../Raspberry-Pi/`](../Raspberry-Pi/).

## Workloads

| Workload | Namespace | Access |
|---|---|---|
| kube-prometheus-stack (Prometheus + Grafana) | `monitoring` | Grafana on NodePort `32000` |
| arduino-exporter | `monitoring` | Prometheus ServiceMonitor (15s scrape) |
| Headlamp | `headlamp` | NodePort `30937` — token login |

## Headlamp

In-cluster Kubernetes dashboard, installed via Helm on pi-server3:

```bash
# On pi-server3
helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/
helm repo update
helm install headlamp headlamp/headlamp \
  --namespace headlamp --create-namespace \
  --set service.type=NodePort
```

Login uses a token from the `headlamp-admin` ServiceAccount (bound to cluster-admin):

```bash
# On pi-server3
sudo kubectl create token headlamp-admin -n headlamp --duration=8760h
```

Open `http://<any-pi-ip>:30937` on the LAN (or the Tailscale IP when remote) and paste the token at the login screen.

## Alertmanager

Alertmanager ships with kube-prometheus-stack; it was wired up with:

- **Receiver:** email via Gmail SMTP (`smtp.gmail.com:587`), authenticated with a Gmail app password stored in the `gmail-app-password` Secret in `monitoring`. The password itself is never committed — the manifest only references the secret by name.
- **Rules:** custom `PrometheusRule` `homelab-custom-alerts` (see `manifests/`):
  - `ArduinoHighTemperature` — room temperature over 30°C for 5 minutes
  - `ArduinoSensorStale` — no Arduino metrics for 10 minutes
  - `NodeDown` — node-exporter silent for 5 minutes
  - `NodeHighCpuLoad` — CPU over 85% for 10 minutes
  - `NodeHighMemoryUsage` — memory over 90% for 10 minutes
- The stack's built-in rules already cover pod crash-looping and disk pressure.

The `AlertmanagerConfig` (`homelab-email`) is picked up automatically by the Prometheus Operator — no Helm changes needed. To add a rule, edit the PrometheusRule manifest and re-apply.

## Gotchas hit along the way

- The old Headlamp chart URL (`headlamp-k8s.github.io/headlamp/`) 404s — the chart moved to `https://kubernetes-sigs.github.io/headlamp/`.
- The operator merges `AlertmanagerConfig` resources into a **gzipped** generated secret (`alertmanager.yaml.gz`, not `alertmanager.yaml`) — decode with `base64 -d | gunzip` when inspecting it.
- The operator injects a `namespace="monitoring"` matcher into AlertmanagerConfig routes, so every alert needs that label to reach the email receiver — API test alerts need it set manually, and `PrometheusRule` alerts need `namespace: monitoring` in their rule labels too (Prometheus doesn't attach it on its own). Without it, alerts fall through to the null receiver silently: no error, no email. This one cost a full debugging session on 2026-10-01.
- Gmail app passwords must be used with **no spaces**; revoke and rotate if one ever lands in chat or logs.
