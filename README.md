# Sidhants-Homelab


Welcome to my homelab project.

This repository documents my journey building and expanding a personal homelab — a real, hands-on environment for learning networking, Linux, infrastructure, monitoring, and eventually containerization and Kubernetes.

Coming from a background in Nokia networking, I wanted a place to apply what I already know and push into areas I haven't worked with before. This is a living project: the hardware, network design, and services here will keep changing as I learn.

Each major area of the lab (Cisco, Omada, Raspberry Pi, monitoring, troubleshooting, projects) has its own directory with detailed documentation. This README is the map — it tells you what's here and points you to where the details live.

---

## 🎯 Why I'm Building This

I wanted to move past simulations and labs and work with real equipment that has real consequences when something breaks.

Goals for this project:

- Build and maintain a real, segmented network
- Get more hands-on experience with Cisco equipment
- Learn and implement VLANs and network segmentation
- Work with TP-Link Omada SDN equipment
- Build a Raspberry Pi–based infrastructure cluster
- Strengthen Linux administration skills
- Learn monitoring and observability (Prometheus/Grafana)
- Learn containerization and, eventually, Kubernetes
- Practice troubleshooting real infrastructure problems
- Document the process — successes and failures — using Git and GitHub

---

## 🖥️ Hardware

| Category | Hardware |
|---|---|
| ISP Gateway| Rogers Router |
| Router | TP-Link ER605 |
| SDN Controller | TP-Link OC200 |
| Core Switch | Cisco Catalyst WS-C3850-24T-E (data-only, no PoE) |
| Compute | 3x Raspberry Pi |
| Microcontroller | Arduino (connected to a Pi via USB for data collection) |

---

## 🌐 Network Topology

```text
                         Internet
                            │
                     ┌─────────────┐
                     │ Rogers XB8  │
                     │ ISP Gateway │
                     └──────┬──────┘
                            │
                     ┌──────▼──────┐
                     │  TP-Link    │
                     │   ER605     │
                     │   Router    │
                     └──────┬──────┘
                            │
                        Trunk (VLAN 10 and Vlan 1)
                            │
                   ┌────────▼────────┐
                   │  Cisco Catalyst │
                   │      3850       │
                   │   Core Switch   │
                   └───────┬─────────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
          ┌──▼───┐      ┌──▼───┐      ┌──▼───┐
          │ OC200│      │ Pi's  │      │ Admin │
          │VLAN10│      │VLAN10 │      │Laptop │
          └──────┘      └───────┘      └───────┘
```

The network currently runs as a single flat VLAN 10 across the trunk to the Cisco 3850 (VLAN 1 has been retired). Full topology history and diagrams live in [`/network/`](./network/).

---

## 🔢 VLANs

| VLAN | Name | Network | Status |
|---|---|---|---|
| 10 | Management | 192.168.10.0/24 | 🟢 Active |
| 20 | Servers | TBD | 🔵 Planned |
| 30 | Clients | TBD | 🔵 Planned |
| 40 | IoT | TBD | 🔵 Planned |
| 50 | Cyber Lab | TBD | 🔵 Planned |

All infrastructure (OC200, Raspberry Pis, Cisco management) currently sits on VLAN 10. Additional VLANs will be rolled out gradually as new device categories are added. Detailed VLAN design and DHCP configuration are documented in [`/network/`](./network/).

---

## 🔌 Cisco Equipment

The Cisco Catalyst 3850 is the core switch for the lab, currently used as a Layer 2 switch — VLANs, trunking, access ports, 802.1Q, MAC/ARP tables. Layer 3 inter-VLAN routing is not in use yet; the ER605 handles routing for now.

Configs live in [`/cisco/configs/`](./cisco/configs/)

---

## 📡 Omada Equipment

The ER605 (router) and OC200 (SDN controller) form the Omada side of the network, with an EAP650 providing Wi-Fi. Getting the OC200 and ER605 adopted and communicating across the Cisco trunk involved a fair amount of troubleshooting — VLAN migration, controller connectivity, and mixed-vendor quirks between Omada and Cisco.

Since Omada is mostly GUI-configured, its documentation is screenshot- and decision-based rather than config files. See [`/omada/`](./omada/).

---

## 🥧 Raspberry Pi Cluster

The lab currently runs 3 individual raspberry Pi's, connected to VLAN 10 with SSH enabled. As of now I have an Arduino connected via USB for data collection.

The future plans for it are creating a 3-node cluster and using Kubernetes on it. Some services I might run are: 

- Linux server experiments
- Monitoring
- Containers and (eventually) a K3s Kubernetes cluster
- Storage experiments

Setup notes and hardware decisions (Pi 4 vs. Pi 400, storage choices) are in [`/raspberry-pi/`](./raspberry-pi/).

---

## 📊 Monitoring

Early experimentation with Prometheus and Grafana for infrastructure visibility — Linux metrics, dashboards, and eventually monitoring the Pi cluster and any Kubernetes workloads. See [`/monitoring/`](./monitoring/).

---

## 🛠️ Troubleshooting

A core part of this project is documenting problems, not just working configs — VLAN migrations, OC200/ER605 adoption issues, DHCP quirks, and mixed-vendor telemetry limitations between Cisco and Omada. Each writeup covers the problem, investigation steps, root cause, and fix. See [`/troubleshooting/`](./troubleshooting/).

---

## 🧪 Projects Completed

- [x] Initial network build (Rogers gateway → ER605 → Cisco 3850)
- [x] Cisco 3850 added and configured as core switch
- [x] VLAN 10 management network deployed
- [x] OC200 adopted and migrated onto the management VLAN
- [x] ER605 adoption and Omada controller connectivity resolved
- [x] Arduino connected to a Pi for data collection
- [x] Initial Prometheus/Grafana experimentation

---

## 📚 Currently Learning

**Networking:** VLANs, 802.1Q trunking, Layer 2/3 concepts, DHCP, ARP, Cisco IOS, Omada SDN
**Linux:** administration, SSH, services, system monitoring
**Infrastructure:** Raspberry Pi cluster management, monitoring, troubleshooting mixed-vendor networks
**Other:** Git/GitHub documentation workflow, early containerization concepts

---

## 🚀 Future Plans

- **Server VLAN (20)** — dedicated network for server infrastructure
- **Kubernetes** — turn the Raspberry Pi cluster into a K3s cluster
- **NAS / Storage** — network storage and backups using Pi hardware
- **Proxmox** — introduce a dedicated virtualization host
- **IoT VLAN (40)** — isolated network for Arduino/sensor projects
- **Cybersecurity Lab (50)** — isolated environment for security testing and traffic analysis

---

## 📁 Repository Structure

---

## 📖 Documentation Philosophy

This repo documents the process, not just the end result — what I set out to do, how I built it, what went wrong, how I fixed it, and what I'd do differently. Sensitive information (passwords, keys, credentials) is never committed.

---

This repository will keep evolving as the homelab grows.
