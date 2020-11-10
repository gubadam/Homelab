# Homelab

Documentation of my homelab setup and learning progress

# Table of contents

* [Goal](#Goal)
* [Servers](#Servers)
* [Network](#Network)
* [Diagram](#Diagram)
* [Tools](#Tools)
* [Future considerations](#Future-considerations)

# Goal

1. Create a base environment for testing and learning about IT systems
2. Continue exploring

# Servers

| Hostname      | Resources                              | IP             | Location      | Purpose                                         |
| --------      | ---------                              | --             | --------      | -------                                         |
| AG-PC-1       | i5-8600K <br> 32GB DDR4                | 172.20.0.100   | Labroom       | Type 2 hypervisor (HyperV) + main client        |
| AQ-ESXi-01    | i3-540 <br> 8GB DDR3                   | 172.20.0.3     | Labroom       | Type 1 hypervisor (ESXi)                        |
| AG-QNAP-1     | 1TB RAID-1                             | 172.20.0.10    | Labroom       | -Not-in-use-                                    |
| LAB-GW-02     | 1 vCPU <br> 4GB vRAM                   | 172.20.0.200 <br> 192.168.100.1 <br> 192.168.101.1 | AG-PC-1       | Gateway FW + VPN concentrator (Sophos XG) |
| LAB-Docker-01 | 2 vCPU <br> 4GB vRAM                   | 172.20.0.201   | AQ-ESXi-01    | Docker host                                     |
| gitlab_web_1  | -                                      | -              | LAB-Docker-01 | Gitlab container                                | 
| LAB-WK-01     | 1 vCPU <br> 2GB vRAM                   | 192.168.100.x  | AG-PC-1       | Client desktop (Windows 10)                     |
| LAB-WK-02     | 1 vCPU <br> 2GB vRAM                   | 192.168.100.x  | AG-PC-1       | Client desktop (Ubuntu 20)                      |
| LAB-DC-01     | 1 vCPU <br> 4GB vRAM                   | 192.168.101.10 | AG-PC-1       | ADDS + DNS + DHCP (Windows Server 2016)         |
| LAB-LOGGER-01 | 1 vCPU <br> 4GB vRAM                   | 192.168.101.30 | AG-PC-1       | Syslog (Graylog) + Network monitor (Zabbix)     |
| LAB-BACKUP-01 | 1 vCPU <br> 4GB vRAM                   | 192.168.101.20 | AG-PC-1       | Backup (Veeam Backup&Replication 10 CE)         |
| GCP-pfsense   | 1 vCPU <br> 0.6GB vRAM <br> (f1-micro) | 10.132.0.2     | GCP cloud     | Gateway FW + VPN concentrator (pfSense)   |


# Network

| VLAN ID | Subnet           | Description    |
| ------- | ------           | -----------    |
| 0       | 172.20.0.0/24    | Home network   |
| 100     | 192.168.100.0/24 | Clients        |
| 101     | 192.168.101.0/24 | Infrastructure |
| 0       | 10.132.0.0/20    | Cloud lab      |


# Diagram

![Diagram](img/Diagram.png?raw=true)

# Tools

| Name                                          | Purpose                                               |
| ----                                          | -------                                               |
| [KeePass 2](https://keepass.info/)            | Password manager                                      |
| [Royal TS Lite](https://royalapps.com/ts)     | Remote connection manager (SSH, RDP, VNC and more)    |
| [draw.io](https://draw.io)                    | Diagram making                                        |
| [github.com](https://github.com)              | Documentation version control                         |

# Future-considerations

Systems to implement:
* [x] Gateway/FW (pfSense, replaced by Sophos XG)
* [x] DC + DNS (WinSrv)
* [x] DHCP (WinSrv)
* [X] Syslog (Graylog)
* [X] Monitoring (Zabbix, maybe try Nagios later?)
* [X] Backup server (Veeam Backup Free Edition)
* [ ] File server (WinSrv>Linux)
* [ ] Mail server
* [ ] WSUS
* [ ] FTP (?)
* [ ] Automated OS deployment (MDT, Ansible)
* [ ] Centralized endpoint management (ME Desktop Central, ?)
* [ ] Webserver (hosting mediawiki)
* [ ] Vulnerability scanner (Nessus)
* [ ] more

Improvements:
* [ ] Clean up this doc
