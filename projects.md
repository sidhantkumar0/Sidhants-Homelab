---
layout: post
title: Projects
---

<img src="{{ '/assets/img/dashboard-5g.png' | relative_url }}" alt="5G slice control dashboard" loading="lazy" />

### Virtualized 5G Network Slicing — Capstone Project
*Carleton University · Oct 2025 – Apr 2026 · 🏆 Best Video Award, Capstone Showcase*

- Built a 5G standalone core (free5GC v4.1.0 + UERANSIM v3.2.6) across KVM virtual machines
- Two slices simulating a hospital network: an isolated URLLC slice for ICU patient vitals, a shared eMBB slice for telemedicine/radiology data
- Flask dashboard with SSH remote control of every VM and live tunnel/patient-data monitoring over MQTT
- Simulated a DDoS attack from a third UE through the 5G tunnel — the shared slice congested while the isolated URLLC slice stayed fully operational
- UDP load testing with iperf3 (bitrate, jitter, packet loss) from 10 to 110 parallel streams
- [View project](https://github.com/sidhantkumar0/CAPSTONE-5G-SLICES)

---

<img src="{{ '/assets/img/WhatsApp%20Image%202026-10-02%20at%201.15.17%20PM%20(1).jpeg' | relative_url }}" alt="Arduino with DHT11 temperature sensor" loading="lazy" />

### Arduino Temperature & Humidity Sensor

- DHT11 sensor on an Arduino Uno, taped to the wall and wired over USB
- Custom Python Prometheus exporter, containerized and running in the K3s cluster
- Grafana "Homelab-Thermo" dashboard + Alertmanager email alerts on high temperature

---

<img src="{{ '/assets/img/WhatsApp%20Image%202026-10-02%20at%201.15.17%20PM%20(2).jpeg' | relative_url }}" alt="Raspberry Pi cluster" loading="lazy" />

### K3s Cluster

- 4x Raspberry Pi 4 running K3s v1.36 — one control plane, three agents
- Hosts the full monitoring stack: Prometheus, Grafana, Alertmanager (email alerts)
- Headlamp dashboard for a visual cluster view
- [Docs](https://github.com/sidhantkumar0/Sidhants-Homelab/tree/main/K3s)

---

<img src="{{ '/assets/img/WhatsApp%20Image%202026-10-02%20at%201.15.17%20PM.jpeg' | relative_url }}" alt="PC converted into Proxmox server" loading="lazy" />

### Proxmox Server
*Work in progress*

- Old desktop PC converted into a Proxmox virtualization host
- Planned: Proxmox Backup Server, Pi-hole, and a NAS once internal drives arrive

---

<img src="{{ '/Network/Updated_Topo.png' | relative_url }}" alt="Homelab network topology" loading="lazy" />

### Homelab Network Infrastructure

- Built the lab's network foundation from scratch: Cisco Catalyst 3850 + TP-Link Omada stack
- VLANs 10 (management) and 20 (servers), 802.1Q trunking, SSH, LLDP
- [Docs](https://github.com/sidhantkumar0/Sidhants-Homelab/tree/main/Network)
