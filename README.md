<div align="center">

<br>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0078D4&height=180&section=header&text=Secure%20Enterprise%20Network&fontSize=35&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Defense-in-Depth%20Networking%20Security&descAlignY=55&descSize=18"/>

<br>

<p>
  <img src="https://img.shields.io/badge/VLAN-Segmentation-0078D4?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/DMVPN-IPsec-005A9E?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Cisco_IOS-IPS-1F6FEB?style=for-the-badge&logo=cisco&logoColor=white"/>
  <img src="https://img.shields.io/badge/ASA-Firewall_HA-004578?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/AAA%2FRBAC-Access_Control-003B73?style=for-the-badge"/>
</p>

<p>
  <img src="https://img.shields.io/badge/Status-COMPLETED-2ecc71?style=flat-square&labelColor=0d1117"/>
  <img src="https://img.shields.io/badge/Course-Defense_in_Depth_Networking_Security-0078D4?style=flat-square&labelColor=0d1117"/>
  <img src="https://img.shields.io/badge/Environment-Academic_Lab-6B4CFF?style=flat-square&labelColor=0d1117"/>
</p>

<br>

<p>
  <i>Secure enterprise network infrastructure implementing VLAN segmentation, DMVPN/IPsec, Cisco IOS IPS, ASA firewall high availability, AAA/RBAC, NAT, and ACL security controls.</i>
</p>

<br>

</div>

---

## Table of Contents

- [Overview](#overview)
- [Topology](#topology)
- [Core Objectives](#core-objectives)
- [Network Segmentation](#network-segmentation)
- [Security Controls Implemented](#security-controls-implemented)
- [VPN and Inter-Branch Connectivity](#vpn-and-inter-branch-connectivity)
- [IDS/IPS Deployment](#idsips-deployment)
- [Firewall High Availability](#firewall-high-availability)
- [AAA and RBAC](#aaa-and-rbac)
- [Validation Summary](#validation-summary)
- [Repository Structure](#repository-structure)

---

## Overview

This repository presents a university group project completed for the **Defense-in-Depth Networking Security** course. The project focuses on building and validating a secure enterprise network infrastructure using multiple layers of protection.

The network was designed to protect internal departments, management services, DMZ services, branch communication, and sensitive internal zones. This repository explains the project using the topology diagram, configuration screenshots, validation screenshots, and short descriptions of the implemented security controls.

---

## Topology

The following topology shows the full enterprise network design, including the HQ hubs, branch routers, ISP connection, core layer, IPS device, ASA firewalls, DMZ, RND zone, and internal VLANs.

![Network Topology](images/topology.png)

---

## Core Objectives

<table width="100%">
  <tr>
    <th>Objective</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><b>Network Segmentation</b></td>
    <td>Separate departments using VLANs for Marketing, Sales, HR, and Management.</td>
  </tr>
  <tr>
    <td><b>L2/L3 Security Hardening</b></td>
    <td>Protect the network from spoofing, MITM attacks, rogue devices, and broadcast storms.</td>
  </tr>
  <tr>
    <td><b>Secure Branch Connectivity</b></td>
    <td>Use dual-hub DMVPN with IPsec to connect HQ and branch offices.</td>
  </tr>
  <tr>
    <td><b>IDS/IPS Protection</b></td>
    <td>Deploy Cisco IOS IPS inline to detect and prevent malicious traffic.</td>
  </tr>
  <tr>
    <td><b>Firewall Enforcement</b></td>
    <td>Use ASA firewalls with Active/Active failover, NAT, ACLs, and security zones.</td>
  </tr>
  <tr>
    <td><b>AAA/RBAC Access Control</b></td>
    <td>Implement centralized authentication and role-based access using RADIUS and parser views.</td>
  </tr>
  <tr>
    <td><b>Validation Testing</b></td>
    <td>Verify the security controls using practical testing and screenshots.</td>
  </tr>
</table>

---

## Network Segmentation

The internal network was divided into separate VLANs for different departments.

<table width="100%">
  <tr>
    <th>VLAN</th>
    <th>Department</th>
    <th>Network</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><b>VLAN 10</b></td>
    <td>Marketing</td>
    <td><code>10.10.1.0/26</code></td>
    <td>Marketing department user segment.</td>
  </tr>
  <tr>
    <td><b>VLAN 20</b></td>
    <td>Sales</td>
    <td><code>10.20.1.0/26</code></td>
    <td>Sales department user segment.</td>
  </tr>
  <tr>
    <td><b>VLAN 30</b></td>
    <td>HR</td>
    <td><code>10.30.1.0/26</code></td>
    <td>Human Resources user segment.</td>
  </tr>
  <tr>
    <td><b>VLAN 99</b></td>
    <td>Management</td>
    <td><code>10.99.1.0/24</code></td>
    <td>Management and administrative services.</td>
  </tr>
</table>

Each VLAN works as a separate broadcast domain. This reduces unnecessary traffic, improves security, and limits lateral movement between departments.

The Management VLAN was separated from normal user VLANs to protect administrative access and management services.

![VLAN Database](images/vlan-database.png)

![SVI Configuration](images/svi-configuration.png)

---

## Security Controls Implemented

<table width="100%">
  <tr>
    <th>Control</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><b>Port Security</b></td>
    <td>Restricts unauthorized devices from connecting to access ports.</td>
  </tr>
  <tr>
    <td><b>DHCP Snooping</b></td>
    <td>Blocks rogue DHCP servers and helps prevent DHCP starvation attacks.</td>
  </tr>
  <tr>
    <td><b>Dynamic ARP Inspection</b></td>
    <td>Prevents ARP spoofing and Man-in-the-Middle attacks.</td>
  </tr>
  <tr>
    <td><b>BPDU Guard</b></td>
    <td>Disables access ports that receive unexpected BPDU packets.</td>
  </tr>
  <tr>
    <td><b>Root Guard</b></td>
    <td>Prevents rogue switches from becoming the STP root bridge.</td>
  </tr>
  <tr>
    <td><b>Loop Guard</b></td>
    <td>Protects against switching loops caused by link failures.</td>
  </tr>
  <tr>
    <td><b>Rate Limiting</b></td>
    <td>Reduces DHCP flooding and Layer 2 DoS attempts.</td>
  </tr>
  <tr>
    <td><b>RFC1918 ACLs</b></td>
    <td>Blocks spoofed private IP traffic from untrusted interfaces.</td>
  </tr>
  <tr>
    <td><b>OSPF Authentication</b></td>
    <td>Protects routing updates from tampering and route injection.</td>
  </tr>
  <tr>
    <td><b>SSH v2</b></td>
    <td>Secures remote management access.</td>
  </tr>
</table>

These controls protect both the access layer and routing/control plane.

![DHCP Snooping](images/dhcp-snooping.png)

![DAI Validation](images/dai-validation.png)

---

## VPN and Inter-Branch Connectivity

A dual-hub DMVPN architecture was implemented to securely connect the headquarters with branch offices.

<table width="100%">
  <tr>
    <th>Site</th>
    <th>Role</th>
  </tr>
  <tr>
    <td><b>HQ-Hub1</b></td>
    <td>Primary DMVPN Hub</td>
  </tr>
  <tr>
    <td><b>HQ-Hub2</b></td>
    <td>Secondary DMVPN Hub</td>
  </tr>
  <tr>
    <td><b>Dubai</b></td>
    <td>Spoke Router</td>
  </tr>
  <tr>
    <td><b>Riyadh</b></td>
    <td>Spoke Router</td>
  </tr>
  <tr>
    <td><b>Doha</b></td>
    <td>Spoke Router</td>
  </tr>
</table>

The DMVPN design provides encrypted branch communication, dynamic spoke registration using NHRP, EIGRP routing over the tunnel, and high availability using two HQ hubs.

<table width="100%">
  <tr>
    <th>Feature</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><b>DMVPN</b></td>
    <td>Provides scalable branch-to-branch connectivity.</td>
  </tr>
  <tr>
    <td><b>IPsec</b></td>
    <td>Encrypts traffic between sites.</td>
  </tr>
  <tr>
    <td><b>NHRP</b></td>
    <td>Allows spokes to register with the hubs.</td>
  </tr>
  <tr>
    <td><b>EIGRP</b></td>
    <td>Provides dynamic routing across the DMVPN tunnel.</td>
  </tr>
  <tr>
    <td><b>Dual-Hub Design</b></td>
    <td>Provides redundancy and failover.</td>
  </tr>
</table>

![DMVPN Validation](images/dmvpn-validation.png)

---

## IDS/IPS Deployment

A Cisco IOS IPS device was deployed inline to inspect traffic and detect malicious activity before it reached internal network segments.

<table width="100%">
  <tr>
    <th>Threat Type</th>
    <th>IPS Response</th>
  </tr>
  <tr>
    <td><b>Port scans</b></td>
    <td>Generate alerts.</td>
  </tr>
  <tr>
    <td><b>TCP NULL scans</b></td>
    <td>Alert and deny packets inline.</td>
  </tr>
  <tr>
    <td><b>TCP SYN/FIN scans</b></td>
    <td>Alert and deny packets inline.</td>
  </tr>
  <tr>
    <td><b>Reconnaissance traffic</b></td>
    <td>Detect suspicious scan behavior.</td>
  </tr>
  <tr>
    <td><b>Policy violations</b></td>
    <td>Log and alert for SOC visibility.</td>
  </tr>
</table>

The IPS validation included scan activity, alert generation, and packet drop evidence.

![IPS Alerts](images/ips-alerts.png)

---

## Firewall High Availability

Cisco ASA firewalls were configured using Active/Active failover and multi-context mode. The firewalls controlled traffic between the Outside, Inside, DMZ, and RND zones.

<table width="100%">
  <tr>
    <th>Firewall Feature</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><b>Active/Active Failover</b></td>
    <td>Provides high availability.</td>
  </tr>
  <tr>
    <td><b>Multi-Context Mode</b></td>
    <td>Separates firewall contexts and policies.</td>
  </tr>
  <tr>
    <td><b>Security Zones</b></td>
    <td>Controls traffic between Outside, Inside, DMZ, and RND.</td>
  </tr>
  <tr>
    <td><b>Static NAT</b></td>
    <td>Publishes selected DMZ services.</td>
  </tr>
  <tr>
    <td><b>Dynamic PAT</b></td>
    <td>Allows internal users to access outside networks.</td>
  </tr>
  <tr>
    <td><b>ACLs</b></td>
    <td>Controls allowed and denied traffic.</td>
  </tr>
  <tr>
    <td><b>Object Groups</b></td>
    <td>Simplifies firewall policy management.</td>
  </tr>
</table>

Failover was tested by shutting down the active firewall and confirming that the standby firewall took over successfully.

![ASA Failover](images/asa-failover.png)

---

## AAA and RBAC

AAA and RBAC were implemented to control administrative access using centralized authentication and role-based permissions.

<table width="100%">
  <tr>
    <th>Role</th>
    <th>Access Level</th>
  </tr>
  <tr>
    <td><b>AdminView</b></td>
    <td>Full administrative access.</td>
  </tr>
  <tr>
    <td><b>AuditView</b></td>
    <td>Read-only auditing access.</td>
  </tr>
  <tr>
    <td><b>UserView</b></td>
    <td>Limited user-level access.</td>
  </tr>
</table>

This ensures that each user only receives the permissions required for their role.

![AAA RBAC Validation](images/aaa-rbac-validation.png)

---

## Validation Summary

<table width="100%">
  <tr>
    <th>Validation Area</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>VLAN segmentation</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>Port security</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>DHCP Snooping</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>Dynamic ARP Inspection</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>BPDU Guard</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>Root Guard</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>DMVPN connectivity</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>NHRP registration</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>IPS alerts</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>IPS packet drops</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>ASA failover</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>NAT and ACL enforcement</td>
    <td>✅ Verified</td>
  </tr>
  <tr>
    <td>AAA/RBAC login tests</td>
    <td>✅ Verified</td>
  </tr>
</table>

---

## Repository Structure

```text
secure-enterprise-network-project/
│
├── README.md
│
└── images/
    ├── topology.png
    ├── vlan-database.png
    ├── svi-configuration.png
    ├── dhcp-snooping.png
    ├── dai-validation.png
    ├── dmvpn-validation.png
    ├── ips-alerts.png
    ├── asa-failover.png
    └── aaa-rbac-validation.png
```
