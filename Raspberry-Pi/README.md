# Raspberry Pi Cluster

## Hardware

Raspberry Pi 1 -> Model 4B 4GB RAM with 32gb sd card [K3s agent — Arduino connected via USB for sensor data collection]
Raspberry Pi 2 -> Model 4B 4GB RAM with 64gb sd card [K3s agent]
Raspberry Pi 3 -> Model 4B 8GB RAM with 128gb sd card [K3s server — control plane]
Raspberry Pi 4 -> Model 4B 4GB RAM with 32gb sd card [K3s agent]

OS: Raspberry Pi OS (64-bit), Desktop version (same for all)
All Pis have static IPs (192.168.20.101 – .104) and SSH access.
All Pis sit on VLAN 20 (server VLAN). Hostnames are pi-server1 through pi-server4.

## K3s Cluster (built September 2026)

4-node K3s cluster:

- pi-server3 = K3s server (control plane)
- pi-server1, pi-server2, pi-server4 = K3s agents

Pod/service networking is pinned to the VLAN 20 interface (eth0, 192.168.20.x).

Workloads running in the cluster:

- **kube-prometheus-stack** (Prometheus + Grafana) in the `monitoring` namespace
- **arduino-exporter**: containerized Python exporter pinned to pi-server1, reads the Arduino over `/dev/ttyACM0`, exposes temperature/humidity/heat-index metrics, scraped by Prometheus via a ServiceMonitor

## Future Plans

- Pi-hole in K3s
- More workloads (Jellyfin, test apps)
- Storage experiments

I will be using GitHub Pages to write down my review and journey.
