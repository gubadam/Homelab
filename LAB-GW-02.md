# LAB-WG-02

This is the main gateway and firewall for the lab.

# Table of contents

* [Hardware](#Hardware)
* [OS](#OS)
* [Software](#Software)
* [Network interfaces](#Network-interfaces)
* [Published services](#Published-services)
* [Standard Operating Procedures](#Standard-Operating-Procedures)

# Hardware

**CPU** 1 vCore

**RAM** 4GB

**Disk** 16GB + 80GB

# OS

**System** Sophos XG Firewall Home Edition Appliance

**Documentation** [Online Sophos documentation](https://www.sophos.com/en-us/support/documentation/sophos-xg-firewall.aspx?platform=Sophos-Firewall-OS-version-18-0#Sophos-Firewall-OS-version-18-0)

# Published services

## Web console
https://192.168.100.1:4444

## Authorization portal
https://192.168.100.1

## Syslog
UDP/1514 > 192.168.101.30

# Network interfaces

## WAN
Bridged via a Hyper-V EXT vSwitch to my home network

## LAN
Interface connected to PRV vSwitch, base interface for all VLANs

For firewall rules checkout [FWRules.csv](FWRules.csv) file

# Standard Operating Procedures

## Creating new VLAN
TODO

## Creating new firewall policy
TODO