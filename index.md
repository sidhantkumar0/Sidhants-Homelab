---
layout: home
title: Sidhant's Homelab
---

I'm Sidhant — I learn networking by building it. This site is where I document my projects, my homelab, and whatever else I'm working on.

## The Equipment

- **4x Raspberry Pi 4** — the K3s cluster, racked and labeled
- **Arduino Uno + DHT11 sensor** — live room temperature and humidity
- **Cisco Catalyst 3850** — the core switch
- **TP-Link Omada stack** — router, controller, and managed switch
- **Old desktop PC** — converted into a Proxmox server (work in progress)
- **1TB SSD + 2TB HDD** — external drives for backups and scratch storage

## What came out of it

- The Pis became a **K3s cluster** running Prometheus, Grafana, and Alertmanager — with email alerts when something needs attention.
- The Arduino became a **live room sensor**, feeding temperature and humidity into that same monitoring stack.
- The Cisco + TP-Link gear became a **VLAN-segmented home network** — management on VLAN 10, servers on VLAN 20.
- The old PC is becoming a **Proxmox server** for VMs and network services.
