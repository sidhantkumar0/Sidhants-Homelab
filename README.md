# Sidhants-Homelab


# 🏠 Homelab

Welcome to my homelab.

This repository documents the development of my personal homelab as I build, configure, troubleshoot, and experiment with networking, infrastructure, Linux, monitoring, automation, and eventually container orchestration.

The goal of this project is not simply to have a collection of devices running at home. I am using the homelab as a hands-on environment to take concepts I have learned and apply them to real infrastructure, while also experimenting with technologies that I have not worked with extensively before.

Everything in this repository is a work in progress. I am documenting both successful configurations and problems encountered along the way so that the repository represents the actual learning process rather than just the final result.

---

## 📌 Project Goals

The main goals of this homelab are to:

- Build and maintain a real segmented network
- Develop practical networking and infrastructure skills
- Gain more experience with Cisco networking equipment
- Learn and implement VLANs and network segmentation
- Work with TP-Link Omada networking equipment
- Build a Raspberry Pi-based infrastructure environment
- Learn Linux system administration
- Experiment with monitoring and observability
- Learn containerization and orchestration
- Eventually build and operate a Kubernetes cluster
- Experiment with storage and NAS infrastructure
- Build useful applications and services
- Practice troubleshooting real infrastructure problems
- Document the entire process using Git and GitHub

---

# 🗺️ Homelab Architecture

The current network is built around a Rogers gateway, TP-Link Omada equipment, and a Cisco Catalyst 3850 switch.

### Current high-level topology

```text
                         Internet
                            │
                            │
                     ┌─────────────┐
                     │ Rogers XB8  │
                     │ ISP Gateway │
                     └──────┬──────┘
                            │
                            │
                     ┌──────▼──────┐
                     │   TP-Link   │
                     │    ER605     │
                     │   Router    │
                     └──────┬──────┘
                            │
                            │ Trunk
                            │ VLAN 1, VLAN 10
                            │
                  ┌─────────▼─────────┐
                  │   Cisco Catalyst  │
                  │       3850        │
                  │    Core-Switch     │
                  └───────┬────────────┘
                          │
          ┌───────────────┼────────────────┐
          │               │                │
          │               │                │
      ┌───▼───┐       ┌───▼───┐        ┌───▼───┐
      │ OC200 │       │ Pi #1  │        │ Pi #2  │
      │ VLAN10│       │ VLAN10 │        │ VLAN10 │
      └───────┘       └────────┘        └────────┘
                                             
                          ┌───────────────┐
                          │ Admin Laptop  │
                          │ Management    │
                          └───────────────┘
