# Secure Enterprise Network Infrastructure Project

## Project Overview

This repository explains the implementation of a secure enterprise network infrastructure using a Defense-in-Depth approach. The project includes VLAN segmentation, Layer 2 and Layer 3 security hardening, secure inter-branch connectivity using DMVPN with IPsec, IDS/IPS deployment, ASA firewall high availability, NAT, ACLs, and AAA/RBAC access control.

The full PDF report is not included in this repository. Instead, this README provides a clear explanation of the project with selected screenshots showing the main implementation and validation steps.

## Topology

```text
                         +----------------+
                         |      ISP       |
                         +----------------+
                           /      |      \
                          /       |       \
                    +--------+ +--------+ +--------+
                    | Dubai  | | Riyadh | | Doha   |
                    | Spoke  | | Spoke  | | Spoke  |
                    +--------+ +--------+ +--------+
                         \        |        /
                          \       |       /
                       ===== DMVPN/IPsec =====
                            /          \
                    +----------+    +----------+
                    | HQ-Hub1  |    | HQ-Hub2  |
                    +----------+    +----------+
                            \        /
                          +------------+
                          | Core Layer |
                          +------------+
                                |
                          +------------+
                          | IOS IPS    |
                          +------------+
                                |
                       +------------------+
                       | ASA Firewalls    |
                       | Active/Active    |
                       +------------------+
                         /       |       \
                      DMZ       RND     Inside
                       |         |        |
                 Web/Email     R&D   MLS1/MLS2
                                      |
                              Access Switches
                                      |
                  +---------+---------+---------+---------+
                  | VLAN 10 | VLAN 20 | VLAN 30 | VLAN 99 |
                  |Marketing|  Sales  |   HR    |  Mgmt   |
                  +---------+---------+---------+---------+
