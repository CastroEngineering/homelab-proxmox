# Homelab: Proxmox on a repurposed laptop

A 24/7 home server for learning infrastructure (backend/cloud focus) and real
daily use. Built step by step with a written decision for each choice.

## Hardware
Ryzen 7, 16 GB RAM, single 512 GB SSD, GTX 1650 Ti (4 GB), wired Ethernet,
running with the lid closed.

## Current state
| Piece | Where it runs | Always on? | Status |
|---|---|---|---|
| Proxmox VE | bare metal | yes | running |
| Jellyfin | unprivileged LXC, rootless Podman | yes | running |
| WireGuard, hardening, backups, Immich, n8n, Ollama, TrueNAS | | | planned |

## How to read this repo
- `docs/decisions/`: why each choice was made (context, options, choice, why)
- `docs/log/`: what was done and how it was verified
- `docs/runbooks/`: how to rebuild something from scratch
- `guests/`, `host/`: sanitized configuration files

## Principles
- Verify, don't assume (every milestone has a pass/fail check)
- Least privilege (unprivileged containers, rootless Podman)
- Nothing secret in this repo
