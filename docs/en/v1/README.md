# Version 1

> November 2025 – present

The first version of the home cluster. Four mini PCs joined into a k3s cluster, with a dedicated router and internet access via a WiFi bridge.

## Goals and principles

- **Budget cluster** for learning Kubernetes and self-hosting
- **Single point of network management** – all network configuration is concentrated on MikroTik
- **Automation via Ansible** – repeatable and idempotent configuration, no manual repetition across nodes
- **No cable across the apartment** – WiFi bridge for internet access instead of running Ethernet
- **Flexibility** – workloads can run on any node, including master nodes

## Architecture

```mermaid
graph LR
    VPS["VPS (WireGuard)"] -.-> Internet["Internet / Home WiFi"]
    Internet --> Keenetic["Keenetic Starter"]
    Keenetic --> MikroTik["MikroTik hEX S\nWireGuard"]
    Laptop["Laptop"] -->|cable| MikroTik
    MikroTik --> Switch["Cudy Switch 8p"]
    MikroTik --> NAS["Ugreen DXP4800 Pro"]
    Switch --> D1["d1 master"]
    Switch --> D2["d2 master"]
    Switch --> D3["d3 master"]
    Switch --> D4["d4 worker"]
    D4 ---|USB3| SSD["Kingston 1TB SSD"]
    subgraph k3sCluster ["k3s Cluster"]
        D1
        D2
        D3
        D4
    end
```

## Detailed documentation

- [Hardware](hardware.md) – specs for all devices, nodes d1-d4, NAS, storage
- [Network](network.md) – network topology, IP addressing, WiFi bridge, cluster access (cable + WireGuard VPN)
- [Software](software.md) – OS, k3s, Ansible, services

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.2 | May 2026 | Remote access via WireGuard VPN (rented VPS), local access via cable |
| v1.1 | May 2026 | Added Ugreen DXP4800 Pro NAS (TrueNAS, 2x 10 TB WD Red Plus, ZFS mirror) |
| v1.0 | November 2025 | Initial build: 4x Dell Optiplex 3060 nodes, k3s cluster, MikroTik, WiFi bridge |
