---
title: Understanding the Bind Shell via My First Pentest
description: My First Pentest Using Netcat
subtitle: PENTEST · NETCAT · BIND SHELL
category_label: BIND SHELL PENTEST
image_class: neural
section_index: /LAB
---

## Summary

This experiment explored how an exposed bind shell can lead to direct remote command execution.

The most interesting observation was not obtaining root access itself, but understanding how quickly system trust boundaries collapse once shell access becomes remotely reachable.

## Enumeration

Initial scanning revealed an unexpected open port on the target system.

```bash
nmap -sV 10.10.10.100
```

<img src='/figures/2026-05-14/namp_result.png' />

Port 1524 appeared accessible and potentially exposed a remote shell service.

## Observation

The service behaviour suggested that the target machine was exposing direct command execution over a listening socket. Unlike SSH, this mechanism lacked:

- authentication
- session control
- access restrictions

This effectively exposed remote shell access directly to the network.

## Execution

Connection to the exposed service was established using netcat:

```bash
nc 10.10.10.100 1524
```

The session immediately returned a shell context.

```bash
whoami
```

<img src='/figures/2026-05-14/netcat_result.png' />

## What is a Bind Shell

A bind shell is a remote shell where the target machine opens a listening port and binds a command shell to it. An attacker connects directly to that port to execute commands remotely, bypassing normal authentication entirely.

Metasploitable exposes one on port 1524 by default. The command that creates it looks like this:

```bash
nc -lvp 1524 -e /bin/bash
```

| Component | Meaning |
| --------- | ------- |
| `nc` | Netcat |
| `-l` | Listen mode |
| `-v` | Verbose |
| `-p 1524` | Listen on port 1524 |
| `-e /bin/bash` | Execute bash shell on connection |

## System Behaviour

Once shell access was established, the system effectively treated remote input as local command execution. This changes the infrastructure trust model significantly:

- commands execute directly on the host
- privilege boundaries become critical
- visibility decreases rapidly
- lateral movement may become possible

## Defender Perspective

This attack raised a question: how would a defender discover or prevent this?

That will be covered in the next post.

## Architectural Reflection

Remote execution is not merely a vulnerability — it fundamentally changes system trust assumptions. Once direct shell execution becomes remotely reachable, the problem shifts from authentication to infrastructure survivability and visibility.
