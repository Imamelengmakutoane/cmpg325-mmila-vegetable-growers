# CMPG 325 Network Project

## Mmila Vegetable Growers (Mahikeng)

![Project Status](https://img.shields.io/badge/status-Milestone%201-blue)
![Course](https://img.shields.io/badge/course-CMPG%20325-green)
![Cisco Packet Tracer](https://img.shields.io/badge/tool-Cisco%20Packet%20Tracer-orange)

## Student Information

| Field | Details |
|---|---|
| Student | Makutoane, AI |
| Student Number | 42510716 |
| Course | CMPG 325 - Computer Networks |
| Institution | North-West University |
| Project ID | CMPG325-2026-041 |
| Client ID | CLI-041 |
| Client | Mmila Vegetable Growers |
| Location | Mahikeng |
| Industry | Agriculture |

## Project Overview

This repository contains the design proposal, topology diagrams, IP addressing plan, Cisco Packet Tracer implementation, and supporting documentation for a computer network designed for Mmila Vegetable Growers in Mahikeng.

The proposed network is intended to provide reliable wired and wireless connectivity for the organisation’s staff and network devices. The design also considers the client’s heritage-listed building, anticipated user growth, and the requirement to implement and demonstrate a Wireless LAN.

## Client Requirements

The proposed network must satisfy the following requirements:

- Provide reliable connectivity for wired and wireless devices.
- Enable communication between relevant devices, including PCs, laptops, servers, and the network printer.
- Support essential network services such as DHCP.
- Use the assigned IPv4 addressing block `192.168.27.0/24`.
- Respect the heritage-listed building constraint by avoiding new cabling through external walls.
- Implement a Wireless LAN with access-point integration and adequate coverage.
- Accommodate a 25% increase in users without renumbering existing devices or subnets.
- Provide a working and testable Cisco Packet Tracer implementation.
- Document the network design, addressing plan, configuration, testing, and design decisions.

## Proposed Network Design

### Physical Topology

The proposed physical topology is an extended star topology with a hybrid wireless element.

The central network devices consist of:

- One router, labelled `R1`.
- One core switch, labelled `SW-Core`.
- One access switch, labelled `SW-Access`.
- One wireless access point, labelled `AP1`.
- Two servers, labelled `Server1` and `Server2`.
- Wired desktop computers.
- One network printer.
- Wireless laptops.

The router connects to the core switch. The core switch connects to the access switch, servers, and wireless access point. Wired computers and the printer connect to the access switch, while wireless laptops connect to `AP1` without physical cabling.

All proposed network cabling is kept inside the building. Wireless connectivity is used to extend network access while respecting the heritage-listed building restriction.

### Logical Topology

The logical topology separates network traffic into VLANs according to device function. This improves organisation, manageability, and future scalability.

The proposed VLANs are:

| VLAN ID | VLAN Name | Purpose | Subnet |
|---:|---|---|---|
| 10 | INFRA | Infrastructure management | `192.168.27.0/27` |
| 20 | SERVER | Servers and critical services | `192.168.27.32/27` |
| 30 | WIRED | Wired PCs and printer | `192.168.27.64/26` |
| 40 | WIRELESS | Wireless clients | `192.168.27.128/26` |
| 50 | FUTURE | Reserved expansion network | `192.168.27.192/26` |

Router `R1` provides the default gateway for the network segments and performs inter-VLAN routing. The logical topology diagram shows which devices belong to each VLAN and how traffic is routed between the logical networks.

## IP Addressing Plan

The assigned address block is:

```text
Network:          192.168.27.0/24
Subnet mask:      255.255.255.0
Usable addresses: 192.168.27.1 - 192.168.27.254
Broadcast:        192.168.27.255
Total usable:     254 addresses
```

### Addressing Summary

| VLAN / Subnet | Network | Mask | Gateway | Static Addresses | DHCP Pool | Reserved or Future Use |
|---|---|---|---|---|---|---|
| INFRA (10) | `192.168.27.0/27` | `255.255.255.224` | `192.168.27.1` | R1: `.1`, SW-Core: `.2`, AP1: `.3` | Not used | `.4-.30` |
| SERVER (20) | `192.168.27.32/27` | `255.255.255.224` | `192.168.27.34` | Server1: `.33`, Server2: `.35` | Not used | `.36-.62` |
| WIRED (30) | `192.168.27.64/26` | `255.255.255.192` | `192.168.27.65` | Printer: `.66` | `.70-.120` | `.121-.126` |
| WIRELESS (40) | `192.168.27.128/26` | `255.255.255.192` | `192.168.27.129` | None required | `.135-.180` | `.130-.134` and `.181-.190` |
| FUTURE (50) | `192.168.27.192/26` | `255.255.255.192` | `192.168.27.193` | None currently | Not used | `.194-.254` |

The server subnet uses static addresses because servers should remain consistently reachable. Wired and wireless end-user devices use DHCP to simplify configuration and administration.

## Growth Accommodation

For the purpose of this design, I assume an initial deployment of approximately **21 user-type devices**, consisting of:

- Approximately 10-11 wired devices, including desktop computers and a printer.
- Approximately 8 wireless devices, including laptops or mobile devices.
- 2 servers.

The projected 25% growth is calculated as follows:

```text
21 × 1.25 = 26.25
```

The network should therefore support approximately **26-27 user-type devices** after growth.

The proposed addressing plan accommodates this requirement because:

- The wired subnet provides 62 usable addresses.
- The wireless subnet provides 62 usable addresses.
- The server subnet provides 30 usable addresses.
- The future subnet provides an additional 62 usable addresses.
- Existing subnets and device addresses do not need to be changed as new users are added.

## Wireless LAN

The wireless LAN is an important part of the design because it addresses both the client’s connectivity requirement and the heritage-building constraint.

The proposed wireless implementation includes:

- Access point `AP1` connected to the network switch using internal Ethernet cabling.
- A dedicated wireless VLAN, VLAN 40.
- An SSID for Mmila Vegetable Growers staff.
- Wireless security using an appropriate authentication method.
- DHCP for wireless clients.
- Central access-point placement to provide adequate coverage within the office.
- Connectivity testing between wireless clients, the gateway, servers, and other permitted devices.

