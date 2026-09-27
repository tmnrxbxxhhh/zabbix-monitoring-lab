# Enterprise Network Monitoring & Troubleshooting Lab

## Overview

This project demonstrates a practical network and server monitoring environment using Zabbix and Ubuntu Server.

The lab focuses on the complete monitoring and troubleshooting workflow:

**Monitor → Detect → Troubleshoot → Fix → Verify → Document**

The environment was built using:

- Ubuntu Server 24.04 LTS
- Zabbix 7.0
- MariaDB
- Zabbix Agent
- VirtualBox
- Cisco Packet Tracer
- SNMP
- Syslog
- Wireshark

## Lab Architecture

The monitoring server runs on an Ubuntu Server virtual machine.

### VirtualBox Network

- Adapter 1: NAT — Internet access
- Adapter 2: Host-Only Network — Management and monitoring network
- Ubuntu monitoring server IP: `192.168.56.10`

### Monitoring Components

- Zabbix Server
- Zabbix Web Interface
- Zabbix Agent
- MariaDB
- Apache2

## Zabbix Configuration

A Zabbix host named `NMS-Server` was configured using the:

**Linux by Zabbix agent**

template.

The Zabbix Agent communicates with the Zabbix Server through:

- IP: `192.168.56.10`
- Port: `10050`

The agent availability was successfully verified in the Zabbix interface.

## Monitoring

The Zabbix environment monitors several system metrics, including:

- CPU utilization
- Memory utilization
- Disk utilization
- System uptime
- Linux system performance metrics

The host successfully reported monitoring data to Zabbix.

## Troubleshooting Scenario: High CPU Utilization

### 1. Detect

A controlled CPU-load scenario was created to simulate a high CPU utilization incident.

The CPU utilization increased to approximately:

**18%**

Zabbix detected and displayed the increased CPU utilization.

![High CPU utilization](screenshots/01-cpu-high.png)

### 2. Troubleshoot

The Linux `top` command was used to identify the process responsible for the increased CPU usage.

The output showed multiple `yes` processes consuming significant CPU resources.

Examples:

- PID 1840 — 57.4% CPU
- PID 1839 — 48.1% CPU
- PID 1844 — 41.3% CPU
- PID 1853 — 40.8% CPU

The system also showed:

- `0.0% idle CPU`
- High load average

This confirmed that the `yes` processes were responsible for the artificial CPU load.

![CPU troubleshooting with top](screenshots/02-top-cpu-process.png)

### 3. Fix

The unwanted processes were stopped using:

```bash
pkill yes
