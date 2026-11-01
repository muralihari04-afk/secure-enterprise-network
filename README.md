# Secure Enterprise Network

## Overview

This project demonstrates the design, configuration, and troubleshooting of a small enterprise network using Cisco Packet Tracer.

The network was designed to demonstrate practical networking and security concepts including VLANs, inter-VLAN routing, DHCP, OSPF, ACLs, SSH, NAT, and network troubleshooting.

## Network Topology

![Network Diagram](diagrams/network-diagram.png)

## Technologies and Concepts

- Cisco Packet Tracer
- VLANs
- Inter-VLAN Routing
- DHCP
- OSPF
- NAT
- Extended ACLs
- SSH
- IP Addressing
- Network Troubleshooting
- OSI Model
- Network Security

## Network Design

| VLAN | Purpose | Network |
|---|---|---|
| VLAN 10 | Employees | 192.168.10.0/24 |
| VLAN 20 | Servers | 192.168.20.0/24 |
| VLAN 30 | Management | 192.168.30.0/24 |

## Devices

- 2 × Cisco Routers
- 1 × Cisco Switch
- 6 × PCs
- 2 × Servers


## Routing

OSPF is used to provide dynamic routing between the routers.

## Security

The network includes:

- VLAN segmentation
- Extended ACLs
- SSH for secure device administration
- Restricted access to the Management VLAN

## DHCP

The router provides DHCP services for the employee network.

## Troubleshooting

Several network problems were intentionally introduced and resolved, including:

1. Incorrect default gateway
2. Incorrect VLAN assignment
3. Trunk configuration problem
4. OSPF neighbor/routing problem
5. ACL-related connectivity restriction
6. DHCP configuration problem

See [`documentation/troubleshooting.md`](documentation/troubleshooting.md).

## Verification

The following Cisco commands were used to verify the network:

```text
show ip interface brief
show ip route
show vlan brief
show interfaces trunk
show ip ospf neighbor
show ip protocols
show access-lists
show ip dhcp binding
ping
traceroute
```

## Project Files

- `packet-tracer/` — Cisco Packet Tracer implementation
- `diagrams/` — Network architecture diagrams
- `configurations/` — Router and switch configurations
- `documentation/` — Technical documentation
- `screenshots/` — Configuration and testing evidence

## Learning Outcomes

This project demonstrates practical experience with network configuration, routing, network segmentation, security controls, and systematic troubleshooting.
