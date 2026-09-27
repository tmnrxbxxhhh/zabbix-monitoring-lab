# Enterprise Network Monitoring & Troubleshooting Lab

## Overview

This project demonstrates a practical enterprise monitoring and troubleshooting environment using Zabbix and Ubuntu Server.

The lab follows a complete operational workflow:

**Monitor → Detect → Troubleshoot → Fix → Verify → Document**

The environment includes:

- Ubuntu Server 24.04 LTS
- Zabbix 7.0
- Zabbix Agent
- MariaDB
- Apache2
- VirtualBox
- Cisco Packet Tracer
- SNMP
- Syslog
- Wireshark

## Lab Architecture

The monitoring server runs on an Ubuntu Server virtual machine hosted in VirtualBox.

### Network Configuration

- Adapter 1: NAT for Internet access
- Adapter 2: Host-Only Network for management and monitoring
- Ubuntu monitoring IP: `192.168.56.10`

### Monitoring Components

- Zabbix Server
- Zabbix Agent
- Zabbix Web Interface
- MariaDB
- Apache2

## Zabbix Configuration

A Zabbix host named `NMS-Server` was configured using the:

**Linux by Zabbix agent**

template.

The Zabbix Agent communicates with the Zabbix Server using:

- IP address: `192.168.56.10`
- Port: `10050`

The Zabbix Agent availability was successfully verified from the Zabbix web interface.

## Monitoring

Zabbix collects multiple system performance metrics from the Ubuntu server, including:

- CPU utilization
- Memory utilization
- Disk utilization
- System uptime
- Linux system performance metrics

The monitoring host successfully reported data to Zabbix.

## Troubleshooting Scenario: High CPU Utilization

This scenario demonstrates how a monitoring alert can be investigated and resolved using Zabbix and Linux troubleshooting tools.

### 1. Detect

A controlled CPU-load scenario was created to simulate a high CPU utilization incident.

Zabbix reported an increased CPU utilization of approximately:

**18%**

![High CPU utilization](screenshots/01-cpu-high.png)

This represents the **Detect** stage of the troubleshooting workflow.

### 2. Troubleshoot

The Linux `top` command was used to identify the processes responsible for the increased CPU usage.

The output showed multiple `yes` processes consuming significant CPU resources.

Examples included:

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

The unwanted CPU-intensive processes were stopped using:

```bash
pkill yes
The command terminated the yes processes that were generating the artificial CPU load.

4. Verify

After stopping the processes, CPU utilization returned to approximately:

3%

Zabbix confirmed that the system returned to a normal CPU utilization level.

Troubleshooting Methodology

The scenario demonstrates a practical incident-response workflow:

Monitor — Zabbix continuously collects system metrics.
Detect — Increased CPU utilization is observed.
Troubleshoot — Linux top identifies the responsible processes.
Fix — The unwanted processes are terminated.
Verify — Zabbix confirms CPU utilization has returned to normal.
Document — The investigation and evidence are recorded.
Tools Used
Tool	Purpose
Zabbix	Infrastructure and system monitoring
Zabbix Agent	Collecting system metrics
Ubuntu Server	Monitoring server and troubleshooting environment
MariaDB	Zabbix database
Apache2	Zabbix web interface
VirtualBox	Virtualized lab environment
Cisco Packet Tracer	Network topology and troubleshooting simulation
SNMP	Network monitoring protocol
Syslog	Centralized event logging
Wireshark	Network traffic analysis
Future Improvements

Planned extensions for the lab include:

SNMP-based device monitoring
Centralized Syslog collection
Network traffic analysis with Wireshark
Additional troubleshooting scenarios
Network availability monitoring
Interface and packet-loss monitoring
Alerting and trigger configuration
Technical incident documentation
Important Lab Note

Cisco Packet Tracer is used in this project for network topology simulation and troubleshooting exercises.

Real SNMP and Syslog integration with Zabbix requires real network-capable devices, virtual network appliances, or another suitable network emulation environment.

Therefore, Packet Tracer devices are not presented as being directly monitored by the Zabbix server.

Project Goals

This project demonstrates practical exposure to:

Linux administration
Infrastructure monitoring
Network monitoring
Troubleshooting
Performance analysis
Incident investigation
Zabbix administration
Technical documentation
