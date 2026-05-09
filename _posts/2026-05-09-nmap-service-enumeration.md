---
title: Nmap service enumeration checklist
description: A practical Nmap service enumeration checklist for cybersecurity lab work.
subtitle: DISCOVER. FINGERPRINT. DOCUMENT.
excerpt_text: A concise workflow for turning an unknown target into a clean map of hosts, ports, services, versions, and next investigative steps.
section_index: /ENUMERATION
category_label: SERVICE FINGERPRINTING
image_class: portal
permalink: /blog/nmap-service-enumeration.html
---

## 1. Confirm scope

Before scanning, write down the exact IP ranges, target names, rules of engagement, and timing constraints. In a lab, this prevents messy notes; in a real assessment, it prevents scanning the wrong systems.

```bash
nmap -sn 192.168.56.0/24 -oA scans/host-discovery
```

## 2. Build an initial port map

Start broad, then get specific. A full TCP sweep helps avoid missing services running outside common ports.

```bash
nmap -p- --min-rate 5000 192.168.56.20 -oA scans/all-tcp-ports
```

## 3. Fingerprint services

Re-scan discovered ports with version detection and default scripts. Keep output in normal, grepable, and XML formats so notes and tooling can use the same scan data.

```bash
nmap -sC -sV -p 22,80,445 192.168.56.20 -oA scans/service-fingerprint
```

## 4. Turn findings into questions

Enumeration is not just collecting banners. Each service should produce a short list of next questions: What version is it? Is authentication required? Are there default credentials? Is there a known CVE? What logs would a defender see?

## 5. Keep a repeatable note format

For each host, record IP, hostname, open ports, service versions, evidence paths, screenshots if needed, and next actions. This makes lab work easier to revisit and turns practice into reusable methodology.
