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

<table>
  <tr>
    <th>Objective</th>
    <th>Description</th>
    <th>Project Outcome</th>
  </tr>
  <tr>
    <td><b>Network Segmentation</b></td>
    <td>Separate departments using VLANs for Marketing, Sales, HR, and Management.</td>
    <td>Departments were isolated into separate broadcast domains to reduce lateral movement.</td>
  </tr>
  <tr>
    <td><b>L2/L3 Security Hardening</b></td>
    <td>Protect the network from spoofing, MITM attacks, rogue devices, and broadcast storms.</td>
    <td>Security controls were applied across the access, distribution, and routing layers.</td>
  </tr>
  <tr>
    <td><b>Secure Branch Connectivity</b></td>
    <td>Use dual-hub DMVPN with IPsec to connect HQ and branch offices.</td>
    <td>Branches were connected using encrypted tunnels with redundancy and failover support.</td>
  </tr>
  <tr>
    <td><b>IDS/IPS Protection</b></td>
    <td>Deploy Cisco IOS IPS inline to detect and prevent malicious traffic.</td>
    <td>Reconnaissance and scan traffic were detected using IPS signatures and alerts.</td>
  </tr>
  <tr>
    <td><b>Firewall Enforcement</b></td>
    <td>Use ASA firewalls with Active/Active failover, NAT, ACLs, and security zones.</td>
    <td>Traffic between Outside, Inside, DMZ, and RND zones was controlled and validated.</td>
  </tr>
  <tr>
    <td><b>AAA/RBAC Access Control</b></td>
    <td>Implement centralized authentication and role-based access using RADIUS and parser views.</td>
    <td>Different user roles were tested with limited, read-only, and full administrative access.</td>
  </tr>
  <tr>
    <td><b>Validation Testing</b></td>
    <td>Verify the security controls using practical testing and screenshots.</td>
    <td>Connectivity, failover, IPS alerts, segmentation, and access control were validated.</td>
  </tr>
</table>

---

## Network Segmentation

The internal network was divided into separate VLANs for different departments.

<table>
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
    <td>Marketing department user segment used to isolate marketing users from other departments.</td>
  </tr>
  <tr>
    <td><b>VLAN 20</b></td>
    <td>Sales</td>
    <td><code>10.20.1.0/26</code></td>
    <td>Sales department user segment used to separate sales traffic from other internal zones.</td>
  </tr>
  <tr>
    <td><b>VLAN 30</b></td>
    <td>HR</td>
    <td><code>10.30.1.0/26</code></td>
    <td>Human Resources segment used to protect HR systems and user communication.</td>
  </tr>
  <tr>
    <td><b>VLAN 99</b></td>
    <td>Management</td>
    <td><code>10.99.1.0/24</code></td>
    <td>Management and administrative services segment used for controlled device access.</td>
  </tr>
</table>

Each VLAN works as a separate broadcast domain. This reduces unnecessary traffic, improves security, and limits lateral movement between departments.

The Management VLAN was separated from normal user VLANs to protect administrative access and management services.

![VLAN Database](images/vlan-database.png)

![SVI Configuration](images/svi-configuration.png)

---

## Security Controls Implemented

<table>
  <tr>
    <th>Control</th>
    <th>Purpose</th>
    <th>Security Benefit</th>
  </tr>
  <tr>
    <td><b>Port Security</b></td>
    <td>Restricts unauthorized devices from connecting to access ports.</td>
    <td>Helps prevent unknown devices from gaining access to the internal network.</td>
  </tr>
  <tr>
    <td><b>DHCP Snooping</b></td>
    <td>Blocks rogue DHCP servers and helps prevent DHCP starvation attacks.</td>
    <td>Ensures users receive valid IP configuration only from trusted DHCP sources.</td>
  </tr>
  <tr>
    <td><b>Dynamic ARP Inspection</b></td>
    <td>Prevents ARP spoofing and Man-in-the-Middle attacks.</td>
    <td>Validates ARP traffic and blocks forged ARP packets.</td>
  </tr>
  <tr>
    <td><b>BPDU Guard</b></td>
    <td>Disables access ports that receive unexpected BPDU packets.</td>
    <td>Protects the switching topology from accidental or malicious switch connections.</td>
  </tr>
  <tr>
    <td><b>Root Guard</b></td>
    <td>Prevents rogue switches from becoming the STP root bridge.</td>
    <td>Keeps the STP root bridge controlled and prevents topology manipulation.</td>
  </tr>
  <tr>
    <td><b>Loop Guard</b></td>
    <td>Protects against switching loops caused by link failures.</td>
    <td>Reduces the risk of broadcast storms caused by STP failures.</td>
  </tr>
  <tr>
    <td><b>Rate Limiting</b></td>
    <td>Reduces DHCP flooding and Layer 2 DoS attempts.</td>
    <td>Limits excessive traffic from access ports and improves network stability.</td>
  </tr>
  <tr>
    <td><b>RFC1918 ACLs</b></td>
    <td>Blocks spoofed private IP traffic from untrusted interfaces.</td>
    <td>Prevents attackers from impersonating internal private addresses from outside.</td>
  </tr>
  <tr>
    <td><b>OSPF Authentication</b></td>
    <td>Protects routing updates from tampering and route injection.</td>
    <td>Ensures routing neighbors exchange authenticated and trusted routing updates.</td>
  </tr>
  <tr>
    <td><b>SSH v2</b></td>
    <td>Secures remote management access.</td>
    <td>Prevents plaintext remote login and improves administrative access security.</td>
  </tr>
</table>

These controls protect both the access layer and routing/control plane.

![DHCP Snooping](images/dhcp-snooping.png)

![DAI Validation](images/dai-validation.png)

---

## VPN and Inter-Branch Connectivity

A dual-hub DMVPN architecture was implemented to securely connect the headquarters with branch offices.

<table>
  <tr>
    <th>Site</th>
    <th>Role</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><b>HQ-Hub1</b></td>
    <td>Primary DMVPN Hub</td>
    <td>Main hub used for branch registration, encrypted tunnel communication, and routing exchange.</td>
  </tr>
  <tr>
    <td><b>HQ-Hub2</b></td>
    <td>Secondary DMVPN Hub</td>
    <td>Backup hub used to provide redundancy if the primary hub becomes unavailable.</td>
  </tr>
  <tr>
    <td><b>Dubai</b></td>
    <td>Spoke Router</td>
    <td>Branch router connected to the HQ hubs through the DMVPN/IPsec tunnel.</td>
  </tr>
  <tr>
    <td><b>Riyadh</b></td>
    <td>Spoke Router</td>
    <td>Branch router connected to the HQ hubs through the DMVPN/IPsec tunnel.</td>
  </tr>
  <tr>
    <td><b>Doha</b></td>
    <td>Spoke Router</td>
    <td>Branch router connected to the HQ hubs through the DMVPN/IPsec tunnel.</td>
  </tr>
</table>

The DMVPN design provides encrypted branch communication, dynamic spoke registration using NHRP, EIGRP routing over the tunnel, and high availability using two HQ hubs.

<table>
  <tr>
    <th>Feature</th>
    <th>Purpose</th>
    <th>Project Usage</th>
  </tr>
  <tr>
    <td><b>DMVPN</b></td>
    <td>Provides scalable branch-to-branch connectivity.</td>
    <td>Used to connect multiple branches to HQ through a flexible hub-and-spoke design.</td>
  </tr>
  <tr>
    <td><b>IPsec</b></td>
    <td>Encrypts traffic between sites.</td>
    <td>Used to secure traffic travelling through the DMVPN overlay.</td>
  </tr>
  <tr>
    <td><b>NHRP</b></td>
    <td>Allows spokes to register with the hubs.</td>
    <td>Used to allow branch routers to register and communicate dynamically with the hubs.</td>
  </tr>
  <tr>
    <td><b>EIGRP</b></td>
    <td>Provides dynamic routing across the DMVPN tunnel.</td>
    <td>Used to advertise branch and HQ networks across the encrypted overlay.</td>
  </tr>
  <tr>
    <td><b>Dual-Hub Design</b></td>
    <td>Provides redundancy and failover.</td>
    <td>Used to maintain inter-branch connectivity if one HQ hub fails.</td>
  </tr>
</table>

![DMVPN Validation](images/dmvpn-validation.png)

---

## IDS/IPS Deployment

A Cisco IOS IPS device was deployed inline to inspect traffic and detect malicious activity before it reached internal network segments.

<table>
  <tr>
    <th>Threat Type</th>
    <th>IPS Response</th>
    <th>Security Purpose</th>
  </tr>
  <tr>
    <td><b>Port scans</b></td>
    <td>Generate alerts.</td>
    <td>Helps identify reconnaissance attempts against internal systems.</td>
  </tr>
  <tr>
    <td><b>TCP NULL scans</b></td>
    <td>Alert and deny packets inline.</td>
    <td>Blocks suspicious scan traffic commonly used for stealthy reconnaissance.</td>
  </tr>
  <tr>
    <td><b>TCP SYN/FIN scans</b></td>
    <td>Alert and deny packets inline.</td>
    <td>Detects abnormal TCP flag combinations used in scanning activity.</td>
  </tr>
  <tr>
    <td><b>Reconnaissance traffic</b></td>
    <td>Detect suspicious scan behavior.</td>
    <td>Provides early visibility into possible attacker enumeration activity.</td>
  </tr>
  <tr>
    <td><b>Policy violations</b></td>
    <td>Log and alert for SOC visibility.</td>
    <td>Supports monitoring, investigation, and incident response workflows.</td>
  </tr>
</table>

The IPS validation included scan activity, alert generation, and packet drop evidence.

![IPS Alerts](images/ips-alerts.png)

---

## Firewall High Availability

Cisco ASA firewalls were configured using Active/Active failover and multi-context mode. The firewalls controlled traffic between the Outside, Inside, DMZ, and RND zones.

<table>
  <tr>
    <th>Firewall Feature</th>
    <th>Purpose</th>
    <th>Project Usage</th>
  </tr>
  <tr>
    <td><b>Active/Active Failover</b></td>
    <td>Provides high availability.</td>
    <td>Ensures firewall services remain available during failover events.</td>
  </tr>
  <tr>
    <td><b>Multi-Context Mode</b></td>
    <td>Separates firewall contexts and policies.</td>
    <td>Allows different firewall contexts to enforce separate security policies.</td>
  </tr>
  <tr>
    <td><b>Security Zones</b></td>
    <td>Controls traffic between Outside, Inside, DMZ, and RND.</td>
    <td>Creates clear security boundaries between trusted, untrusted, and service zones.</td>
  </tr>
  <tr>
    <td><b>Static NAT</b></td>
    <td>Publishes selected DMZ services.</td>
    <td>Allows controlled external access to selected DMZ-hosted services.</td>
  </tr>
  <tr>
    <td><b>Dynamic PAT</b></td>
    <td>Allows internal users to access outside networks.</td>
    <td>Provides outbound internet access for internal users using translated addresses.</td>
  </tr>
  <tr>
    <td><b>ACLs</b></td>
    <td>Controls allowed and denied traffic.</td>
    <td>Enforces traffic filtering between firewall zones and interfaces.</td>
  </tr>
  <tr>
    <td><b>Object Groups</b></td>
    <td>Simplifies firewall policy management.</td>
    <td>Makes firewall rules easier to manage by grouping hosts, networks, and services.</td>
  </tr>
</table>

Failover was tested by shutting down the active firewall and confirming that the standby firewall took over successfully.

![ASA Failover](images/asa-failover.png)

---

## AAA and RBAC

AAA and RBAC were implemented to control administrative access using centralized authentication and role-based permissions.

<table>
  <tr>
    <th>Role</th>
    <th>Access Level</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><b>AdminView</b></td>
    <td>Full administrative access.</td>
    <td>Used for administrators who require full device configuration privileges.</td>
  </tr>
  <tr>
    <td><b>AuditView</b></td>
    <td>Read-only auditing access.</td>
    <td>Used for users who need to review configurations and outputs without making changes.</td>
  </tr>
  <tr>
    <td><b>UserView</b></td>
    <td>Limited user-level access.</td>
    <td>Used for restricted users with minimal command permissions.</td>
  </tr>
</table>

This ensures that each user only receives the permissions required for their role.

![AAA RBAC Validation](images/aaa-rbac-validation.png)

---

## Validation Summary

<table>
  <tr>
    <th>Validation Area</th>
    <th>Result</th>
    <th>What Was Confirmed</th>
  </tr>
  <tr>
    <td><b>VLAN segmentation</b></td>
    <td>✅ Verified</td>
    <td>Departments were separated into their assigned VLANs and subnets.</td>
  </tr>
  <tr>
    <td><b>Port security</b></td>
    <td>✅ Verified</td>
    <td>Unauthorized MAC/device behavior was restricted on access ports.</td>
  </tr>
  <tr>
    <td><b>DHCP Snooping</b></td>
    <td>✅ Verified</td>
    <td>Trusted and untrusted DHCP behavior was validated.</td>
  </tr>
  <tr>
    <td><b>Dynamic ARP Inspection</b></td>
    <td>✅ Verified</td>
    <td>ARP spoofing protection was enabled and validated.</td>
  </tr>
  <tr>
    <td><b>BPDU Guard</b></td>
    <td>✅ Verified</td>
    <td>Access ports were protected from unexpected BPDU packets.</td>
  </tr>
  <tr>
    <td><b>Root Guard</b></td>
    <td>✅ Verified</td>
    <td>STP root manipulation protection was confirmed.</td>
  </tr>
  <tr>
    <td><b>DMVPN connectivity</b></td>
    <td>✅ Verified</td>
    <td>Branch routers successfully communicated through the DMVPN overlay.</td>
  </tr>
  <tr>
    <td><b>NHRP registration</b></td>
    <td>✅ Verified</td>
    <td>Spokes registered successfully with the DMVPN hubs.</td>
  </tr>
  <tr>
    <td><b>IPS alerts</b></td>
    <td>✅ Verified</td>
    <td>Scan activity generated IPS alerts.</td>
  </tr>
  <tr>
    <td><b>IPS packet drops</b></td>
    <td>✅ Verified</td>
    <td>Malicious or suspicious traffic was denied inline.</td>
  </tr>
  <tr>
    <td><b>ASA failover</b></td>
    <td>✅ Verified</td>
    <td>Firewall role switchover occurred successfully after forced failover.</td>
  </tr>
  <tr>
    <td><b>NAT and ACL enforcement</b></td>
    <td>✅ Verified</td>
    <td>Traffic translation and filtering policies worked as expected.</td>
  </tr>
  <tr>
    <td><b>AAA/RBAC login tests</b></td>
    <td>✅ Verified</td>
    <td>User roles received the correct access level during login testing.</td>
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
