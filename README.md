# Homelab

Personal home server cluster for learning and self-hosting. Built as a budget-friendly alternative to renting a VDS, and as a hands-on platform for learning Kubernetes, networking, and infrastructure automation.

> [Читать на русском](docs/ru/README.md)

![Cluster photo](docs/images/v1/homelab.jpg)
![NAS photo](docs/images/v1/nas.jpg)

## Current version

[v1.2](docs/en/v1/README.md) – 4-node k3s cluster on Dell Optiplex 3060 + Ugreen NAS, MikroTik networking, WireGuard VPN via external VPS, Ansible-managed configuration.

## Version history

| Version | Period | Description |
|---------|--------|-------------|
| [v1.2](docs/en/v1/README.md) | May 2026 – present | Remote access via WireGuard VPN through a rented VPS, local access via cable to MikroTik |
| [v1.1](docs/en/v1/README.md) | May 2026 | Added Ugreen DXP4800 Pro NAS with TrueNAS, 2x 10 TB WD Red Plus in ZFS mirror |
| [v1](docs/en/v1/README.md) | November 2025 – May 2026 | 4x Dell Optiplex 3060, k3s cluster (3 masters + 1 worker), MikroTik hEX S, WiFi bridge for internet |
