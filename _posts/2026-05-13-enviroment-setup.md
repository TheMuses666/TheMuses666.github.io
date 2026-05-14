---
title: Building a Segmented Network Lab with pfSense
description: My virtual environment for cybersecurity-labs study.
subtitle: ISOLATE · CONTROL · SIMULATE
category_label: ENVIRONMENT SETUP
image_class: neural
section_index: /LAB
---

## Architecture

Three isolated zones, one firewall at the centre.

<img src='/figures/2026-05-13/architecture.jpg'/>

| Zone | Machine | IP Range |
|------|---------|----------|
| LAN | — | 192.168.1.0/24 |
| DMZ | Metasploitable | 10.10.10.0/24 |
| Attacker | Kali Linux | 172.16.0.0/24 |

Each zone is a separate VirtualBox Internal Network. VMs cannot communicate directly — all traffic routes through pfSense.

## VirtualBox Network Setup

Each VM's adapter is set to **Internal Network** with the zone name. This creates isolated virtual switches; only machines sharing the same name can see each other.

<img src='/figures/2026-05-13/pfSense_adapters.png'/>

pfSense has four adapters: WAN (NAT) plus one adapter per zone.

## pfSense Interface Configuration

On first boot, pfSense assigns each adapter to a zone via the console. Static IPs and DHCP ranges are set with option 2.

<img src='/figures/2026-05-13/pfSense_console.png'/>

| Interface | IP | DHCP Range |
|-----------|-----|------------|
| LAN (em1) | 192.168.1.1/24 | .100–.200 |
| OPT1/DMZ (em2) | 10.10.10.1/24 | .100–.200 |
| OPT2/Attacker (em3) | 172.16.0.1/24 | .100–.200 |

DHCP starts at `.100` to keep `.1–.99` free for static assignments.

---

_Next: configure pfSense firewall rules and run the first Nmap scan from Kali through the firewall._
