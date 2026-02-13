# Hardware

## Summary

| Model | Role | Key specs |
|-------|------|-----------|
| Dell Optiplex 3060 Micro (d1) | k3s master node | 6 CPU cores, 8 GB RAM, 128 GB SSD |
| Dell Optiplex 3060 Micro (d2) | k3s master node | 6 CPU cores, 8 GB RAM, 128 GB SSD |
| Dell Optiplex 3060 Micro (d3) | k3s master node | 6 CPU cores, 8 GB RAM, 128 GB SSD |
| Dell Optiplex 3060 Micro (d4) | k3s worker node | 6 CPU cores, 8 GB RAM, 128 GB SSD |
| Kingston 1 TB SSD (external) | Backup storage | USB 3.0, connected to d4 |
| MikroTik hEX S | Router | 1 Gbit, manages all cluster networking |
| Cudy (unmanaged) | Switch | 8 ports, 1 Gbit |
| Keenetic Starter | WiFi bridge | 100 Mbit, connects to home WiFi |

## Cluster nodes (d1-d4)

All four nodes are identical **Dell Optiplex 3060 Micro** mini PCs:

- **CPU**: 6 cores
- **RAM**: 8 GB
- **Disk**: 128 GB SSD (internal)
- **Network**: built-in 1 Gbit Ethernet

### Labels and roles

| Node | k3s role | Note |
|------|----------|------|
| d1 | master + etcd | – |
| d2 | master + etcd | – |
| d3 | master + etcd | – |
| d4 | worker | External SSD attached |

Workloads can run on all nodes, including master nodes (taints removed).

## External storage

- **Model**: Kingston 1 TB SSD
- **Connection**: USB 3.0 to node d4
- **Purpose**: backups and large file storage

## Networking equipment

### MikroTik hEX S

The primary network device for the cluster. A 1 Gbit router responsible for all networking: DHCP, routing, firewall. All cluster network configuration is intentionally concentrated on this device.

### Cudy unmanaged switch

8-port switch at 1 Gbit. Connects all four mini PCs to a single MikroTik port. Also leaves room for future cluster expansion (free ports available).

### Keenetic Starter

A 100 Mbit WiFi router configured as a WiFi bridge. Connects to the home WiFi network and provides internet to the cluster via cable through MikroTik. The 100 Mbit limitation was a deliberate choice to save on cost, since heavy internet traffic is not expected. Chosen as a budget solution to avoid running Ethernet cable across the apartment. No cluster network configuration is done on this device – only the home WiFi connection.

<!-- ## Photos -->
<!-- ### Overview -->
<!-- ![Cluster overview](../../images/v1/cluster-overview.jpg) -->
<!-- ### Rear view (cables) -->
<!-- ![Cables](../../images/v1/cluster-cables.jpg) -->
<!-- ### Node labels -->
<!-- ![Labels](../../images/v1/node-labels.jpg) -->
