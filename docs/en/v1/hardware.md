# Hardware

## Summary

| Model | Role | Key specs |
|-------|------|-----------|
| Dell Optiplex 3060 Micro (d1) | k3s master node | 6 CPU cores, 24 GB RAM, 1 TB SSD |
| Dell Optiplex 3060 Micro (d2) | k3s master node | 6 CPU cores, 24 GB RAM, 1 TB SSD |
| Dell Optiplex 3060 Micro (d3) | k3s master node | 6 CPU cores, 24 GB RAM, 1 TB SSD |
| Dell Optiplex 3060 Micro (d4) | k3s worker node | 6 CPU cores, 24 GB RAM, 1 TB SSD |
| MikroTik hEX S | Router | 1 Gbit, manages all cluster networking |
| Cudy (unmanaged) | Switch | 8 ports, 1 Gbit |
| Ugreen DXP4800 Pro | NAS | 8 GB RAM, 128 GB SSD (TrueNAS), 2x 10 TB HDD ZFS mirror |
| Keenetic Starter | WiFi bridge and WiFi access | 100 Mbit, bridge to home WiFi and own WiFi network |

## Cluster nodes (d1-d4)

All four nodes are identical **Dell Optiplex 3060 Micro** mini PCs:

- **CPU**: 6 cores
- **RAM**: 24 GB
- **Disk**: 1 TB SSD (internal)
- **Network**: built-in 1 Gbit Ethernet

### Labels and roles

| Node | k3s role | Note |
|------|----------|------|
| d1 | master + etcd | – |
| d2 | master + etcd | – |
| d3 | master + etcd | – |
| d4 | worker | – |

Workloads can run on all nodes, including master nodes (taints removed).

## NAS

- **Model**: Ugreen DXP4800 Pro
- **RAM**: 8 GB (stock)
- **OS**: TrueNAS (installed instead of stock firmware) on 128 GB SSD
- **Storage**: 2x 10 TB WD Red Plus in ZFS mirror
- **Connection**: Ethernet directly into a dedicated MikroTik port (not through the switch)
- **Purpose**: data storage only – cluster backups, media files (Plex, *arr stack), S3 data, torrents, shared folder for direct laptop access
- **Principle**: no services run on the NAS – all services run in the k3s cluster and access the NAS over the network for data

## Networking equipment

### MikroTik hEX S

The primary network device for the cluster. A 1 Gbit router responsible for all networking: DHCP, routing, firewall. All cluster network configuration is intentionally concentrated on this device.

### Cudy unmanaged switch

8-port switch at 1 Gbit. Connects all four mini PCs to a single MikroTik port. Also leaves room for future cluster expansion (free ports available).

### Keenetic Starter

A 100 Mbit WiFi router. Connects to the home WiFi as a bridge and provides internet to the cluster via cable through MikroTik. Also broadcasts its own WiFi network for accessing public cluster services. The 100 Mbit limitation was a deliberate choice to save on cost, since heavy internet traffic is not expected. Chosen as a budget solution to avoid running Ethernet cable across the apartment.

<!-- ## Photos -->
<!-- ### Overview -->
<!-- ![Cluster overview](../../images/v1/cluster-overview.jpg) -->
<!-- ### Rear view (cables) -->
<!-- ![Cables](../../images/v1/cluster-cables.jpg) -->
<!-- ### Node labels -->
<!-- ![Labels](../../images/v1/node-labels.jpg) -->
