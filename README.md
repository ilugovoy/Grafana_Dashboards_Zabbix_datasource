# Grafana dashboards for visualization of metrics from Zabbix

[![Grafana](https://img.shields.io/badge/Grafana-F2F4F9?style=for-the-badge&logo=grafana&logoColor=orange&labelColor=F2F4F9)](https://grafana.com) [![Zabbix](https://img.shields.io/badge/Zabbix-D50000?style=for-the-badge&logo=zabbix&logoColor=white)](https://www.zabbix.com)

This repository contains Grafana dashboard templates for comprehensive monitoring of various services and applications using Zabbix.

## ⚙️ System Requirements

1. **Zabbix Server** 6.0+
2. **Grafana** 11.0+
3. **Zabbix Plugin for Grafana** (alexanderzobnin-zabbix-app)

_Tested with Linux Ubuntu 24 and Windows Server 2022_

## 📂 Content

### System Metrics
- **[Linux VM](./LinuxVM/)**: visualization of Linux virtual machine metrics including CPU, memory, disk, and network statistics with alert thresholds and historical data.
- **[Windows VM](./WindowsVM/)**: Windows server metrics visualization tracking performance counters, service statuses, and system resource utilization.

### Databases
- **[PostgreSQL](./PostgreSQL/)**: PostgreSQL metrics visualization including query performance, replication status, WAL metrics, and database health indicators.
- **[Microsoft SQL](./MSSQL/)**: MS SQL Server metrics visualization with availability group tracking, query statistics, backup status, and performance metrics.

### Other
- **[TOP HOSTS](./TOP_HOSTS/)**: real-time ranking of most heavily loaded hosts by CPU, memory and disk metrics.
- **[Docker Containers](./DockerContainers/)**: container metrics visualization tracking container states, resource usage, images, volumes and Docker daemon health metrics.
- **[Exchange](./Exchange/)**: Microsoft Exchange server metrics visualization including mail queue status, client connectivity, and service health indicators.