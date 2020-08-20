# Homelab
Documentation of my homelab setup and learning progress

# Table of contents
* [Goal](#goal)
* [Hardware](#Hardware)
* [Software](#Software)
    * [Management and documentation tools](#Management-and-documentation-tools)
    * [Hypervisor](#Hypervisor)
* [Network](#Network)
    * [vSwitches](#vSwitches-(Hyper-V))
    * [Diagram](#Diagram)
    * [ACLs](#ACLs)
* [VMs](#VMs)
* [Future considerations](#Future-considerations)

# Goal
1. Create a base environment for testing and learning about IT systems
2. Continue exploring

# Hardware
So far I've only been using my main [i5-8600K](https://ark.intel.com/content/www/us/en/ark/products/129937/intel-core-i5-8600-processor-9m-cache-up-to-4-30-ghz.html) based PC to host all the VMs

# Software
## Management and documentation tools
* [KeePass 2](https://keepass.info/) password manager
* [Royal TS Lite](https://royalapps.com/ts) remote connection manager (SSH, RDP, VNC and more)
* [draw.io](https://draw.io) diagram making
* [github.com](https://github.com) source code/documentation version control

## Hypervisor
* [Windows 10 Education](https://www.microsoft.com/en-us/windowsforbusiness/compare) (which is [basically Enterprise edition with disabled ads](https://docs.microsoft.com/en-us/education/windows/windows-editions-for-education-customers#windows-10-education)) with Hyper-V feature installed

# Network

## vSwitches (Hyper-V)
* EXT
    * bridged to hardware NIC of the host computer
    * connected only to the main gateway server as a WAN zone
* PRV
    * connected to every VM in the homelab as LAN adapter
    * have IEEE 802.1Q tagging enabled
    * connected to main gateway with a trunk link allowing all VLAN IDs, other hosts are connected via access links to a single VLAN per NIC

## Diagram

![Diagram](img/NetworkDiagram.jpg?raw=true)

## ACLs

All hosts other then the lab gateway itself are only connected to virtual network (PRV), so all external (and also intervlan) traffic comes through the gateway.

By default all traffic is denied, only allowing for specific traffic based on the network subnet purpose.

For detailed ACLs/firewall polices and rules check out [FWRules.csv](FWRules.csv) file

# VMs

Please check out [Servers.csv](Servers.csv) file for information on OS, software, roles and services configured

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
* [ ] more

Improvements:
* [ ] Clean up this doc
