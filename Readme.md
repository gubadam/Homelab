# Homelab

Documentation of my homelab setup and learning progress

# Table of contents

* [Goal](#Goal)
* [Diagram](#Diagram)
* [Servers](#Servers)
* [Network](#Network)
* [Storage](#Storage)
* [Services](#Services)
* [Tools](#Tools)
* [Future considerations](#Future-considerations)

# Goal

1. Create a base environment for testing and learning about IT systems
2. Continue exploring

# Diagram

![Diagram](img/Diagram.png?raw=true)

# Servers

| Hostname      | Resources                              | IP             | Location      | Purpose                                         |
| --------      | ---------                              | --             | --------      | -------                                         |
| AG-PC-1       | i5-8600K <br> 32GB DDR4                | 172.20.0.100   | Labroom       | Type 2 hypervisor (HyperV) + main client        |
| AQ-ESXi-01    | i3-540 <br> 8GB DDR3                   | 172.20.0.3     | Labroom       | Type 1 hypervisor (ESXi)                        |
| AG-QNAP-1     | 2x 500GB RAID-1                        | 172.20.0.10    | Labroom       | Secondary storage array for backups             |
| AG-RPi-1      | Cortex-A72 (4x1.5GHz) <br> 8GB DDR4    | 172.20.0.20    | Labroom       | Lab monitoring (zabbix) + testing
| LAB-GW-02     | 1 vCPU <br> 4GB vRAM                   | 172.20.0.200 <br> 192.168.100.1 <br> 192.168.101.1 | AG-PC-1       | Gateway FW + VPN concentrator (Sophos XG) |
| LAB-Docker-01 | 2 vCPU <br> 4GB vRAM                   | 172.20.0.201   | AQ-ESXi-01    | Docker host (CentOS 7)                           |
| gitlab_web_1  | -                                      | -              | LAB-Docker-01 | Gitlab container                                | 
| LAB-WK-01     | 1 vCPU <br> 2GB vRAM                   | 192.168.101.x  | AG-PC-1       | Client desktop (Windows 10)                     |
| LAB-DC-01     | 1 vCPU <br> 4GB vRAM                   | 192.168.100.2  | AG-PC-1       | ADDS + ADCS + DNS + DHCP (Windows Server 2016) |
| LAB-APP-01    | 2 vCPU <br> 4GB vRAM                   | 192.168.100.3  | AG-PC-1       | MEDesktopCentral + Nessus + IIS hosting static website (Windows Server 2016) |
| LAB-BACKUP-01 | 1 vCPU <br> 4GB vRAM                   | 192.168.100.4  | AG-PC-1       | Backup (Veeam Backup&Replication 10 CE)         |
| GCP-pfsense   | 1 vCPU <br> 0.6GB vRAM <br> (f1-micro) | 10.132.0.2     | GCP cloud     | Gateway FW + VPN concentrator (pfSense)         |


# Network

| VLAN ID | Subnet           | Description    |
| ------- | ------           | -----------    |
| 0       | 172.20.0.0/24    | Home network   |
| 100     | 192.168.100.0/24 | Servers        |
| 101     | 192.168.101.0/24 | Workstations   |
| 0       | 10.132.0.0/20    | Cloud lab      |
| 0       | 10.254.254.0/24  | iSCSI network  |

# Storage

## Main VM storage

* 1x 256GB NVMe SSD
* One parent RO VHD with generalized image of fully patched Windows Server 2016 installed and each VM having a separate child VHD to massively reduce size of the lab and installation speed of new systems

## Backups storage

* 2x 500GB SATA3 HDD in RAID-1 configured on AG-QNAP-1 NAS
* Connected to main compute host AG-PC-01 via physically separate iSCSI network

# Services

| Name | Usecase |
| ---- | ------- |
| SophosXG firewall | <ul><li>Routing and NATing traffic between WAN and LAN networks</li><li>Relaying DHCP requests to main DHCP server</li><li>Filtering traffic to only allow neccesarry services</li><li>Terminating IKEv2/IPSec Site-to-site VPN</li></ul> |
| pfSense | <ul><li>Terminating IKEv2/IPSec Site-to-site VPN</li><li>Terminating remote access OpenVPN (SSL) for remote access to the lab and traffic redirection through USA</li></ul> |
| DHCP | Assigning network configuration to hosts in predefined scopes |
| DNS | Name resolution for hosts and services inside the homelab |
| Active Directory | Domain Services:<ul><li>centralized hosts configuration via GPO</li><li>centralized user authentication and autorization</li></ul>Certificate Services:<ul><li>Management of Public Key Infrastructure issuing certificates for encryption and authentication of secure lab services</li></ul>
| IIS | Hosting static website ([pomodoro-timer app I contributed to](https://github.com/tope96/catch-up-time)) with http to https redirection |
| Veeam Backup Community Edition | Scheduled automatic backup of key lab machines to secondary redundant array of discs |
| Manage Engine Desktop Central | Centralized configuration and patch management and auditing |
| Zabbix | Monitoring and logging of key performance and availability metrics |
| Tenable Nessus | Vulnerability scanner |

# Tools

| Name                                          | Purpose                                               |
| ----                                          | -------                                               |
| [KeePass 2](https://keepass.info/)            | Password manager                                      |
| [Royal TS Lite](https://royalapps.com/ts)     | Remote connection manager (SSH, RDP, VNC and more)    |
| [draw.io](https://draw.io)                    | Diagram making                                        |
| [github.com](https://github.com)              | Documentation version control                         |

# Future-considerations

* Nessus
* RDS
* VDI
* DFS
* FTP
* WSUS
* Mail