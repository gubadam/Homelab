# LAB-LOGGER-01

System monitoring and syslog collector/aggregator

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

**Disk** 8GB

# OS

**System** Debian 10

**Documentation** [Online Debian documentation](https://www.debian.org/doc/)

# Software

## Graylog log management
[Install Graylog on Debian](https://docs.graylog.org/en/3.2/pages/installation/os/debian.html)

## Zabbix monitoring
[Install Zabbix on Debian](https://www.zabbix.com/download?zabbix=5.0&os_distribution=debian&os_version=10_buster&db=postgresql&ws=nginx)

# Network interfaces
## eth0
STATIC 192.168.101.30/24

DNS 192.168.101.20

# Published services
## Graylog web interface
http://192.168.101.30:9000/

## Zabbix web interface
http://192.168.101.30/

# Standard Operating Procedures
## Creating new input on Graylog server
Don't use low ports because you'll get errors due to lack of permissions on Linux.

For Sophos use RAW/UDP (I used UDP/1514)
## Creating new extractor for Graylog input
I used these [these extractors](https://raw.githubusercontent.com/zildjian4life218/Sophos-XG-Extractor/master/sophos_xg.json)
## Creating new host on Zabbix server
TODO
## Installing agent on Zabbix client
TODO