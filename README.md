# Secure Enterprise Network Infrastructure Project

## Project Overview

This repository explains the implementation of a secure enterprise network infrastructure using a Defense-in-Depth approach. The project includes VLAN segmentation, Layer 2 and Layer 3 security hardening, secure inter-branch connectivity using DMVPN with IPsec, IDS/IPS deployment, ASA firewall high availability, NAT, ACLs, and AAA/RBAC access control.

## Topology

The following topology shows the full enterprise network design, including the HQ hubs, branch routers, ISP connection, core layer, IPS device, ASA firewalls, DMZ, RND zone, and internal VLANs.

![Network Topology](images/topology.png)

## 1. Network Segmentation

The internal network was divided into separate VLANs for different departments. Each VLAN works as a separate broadcast domain, which helps reduce unnecessary traffic, improve security, and limit lateral movement between departments.

```text
+---------+------------+---------------+
| VLAN    | Department | Network       |
+---------+------------+---------------+
| VLAN 10 | Marketing  | 10.10.1.0/26  |
| VLAN 20 | Sales      | 10.20.1.0/26  |
| VLAN 30 | HR         | 10.30.1.0/26  |
| VLAN 99 | Management | 10.99.1.0/24  |
+---------+------------+---------------+
