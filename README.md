# Secure Enterprise Network

## Project Overview

This project demonstrates the design, configuration, and troubleshooting of a small enterprise network using Cisco Packet Tracer.

The network is designed to simulate an enterprise environment with separate employee, server, and management networks.

It implements VLAN segmentation, inter-VLAN routing, DHCP, OSPF, Access Control Lists (ACLs), and Secure Shell (SSH) to demonstrate practical networking and security concepts.

## Network Topology

<img width="705" height="502" alt="Screenshot 2026-11-01 at 11 33 43 AM" src="https://github.com/user-attachments/assets/cc947bbd-50c8-4ee3-a74c-b554ac355249" />


## Network Infrastructure

| Device | Model | Quantity |
|---|---|---|
| Router | Cisco 2911 | 2 |
| Switch | Cisco 2960 | 1 |
| PCs | End Devices | 6 |
| Servers | Server | 2 |

## Network Design

The network is divided into three VLANs to separate different groups of devices.

| VLAN ID | VLAN Name | Network Address | Default Gateway |
|---|---|---|---|
| 10 | EMPLOYEES | 192.168.10.0/24 | 192.168.10.1 |
| 20 | SERVERS | 192.168.20.0/24 | 192.168.20.1 |
| 30 | MANAGEMENT | 192.168.30.0/24 | 192.168.30.1 |

### Device Connections

- R1 connects to R2 through a point-to-point network.
- R2 connects to SW1 using a trunk link.
- SW1 distributes devices into their respective VLANs.
- Router subinterfaces provide inter-VLAN routing.

## Technologies and Concepts

| Technology | Description |
|---|---|
| Cisco Packet Tracer | Network simulation and configuration |
| VLANs | Logical network segmentation |
| Inter-VLAN Routing | Communication between VLANs |
| OSPF | Dynamic routing between routers |
| DHCP | Automatic IP address assignment |
| Extended ACL | Traffic filtering between network segments |
| SSH | Secure remote device administration |
| Cisco IOS | Router and switch configuration |

## Security Implementation

### 1. VLAN Segmentation

Separate employee workstations, servers, and management devices into different VLANs.

### 2. Access Control List (ACL)

An Extended ACL is configured on R2 to block IP traffic from the employee network (VLAN 10) to the management network (VLAN 30).

### 3. Secure Shell (SSH)

SSH version 2 is configured on R2 and SW1 to provide encrypted remote administration.

## Network Configuration

The project includes the following device configuration files:

- `R1-config.txt`
- `R2-config.txt`
- `SW1-config.txt`

## Project Documentation

Detailed documentation is available below:

| Documentation | Description |
|---|---|
| [IP Addressing](docs/IP-addressing.md) | IP addressing scheme and default gateways |
| [VLAN Design](docs/VLAN-design.md) | VLAN configuration and switch port assignments |
| [Security Controls](docs/security-controls.md) | VLAN segmentation, ACLs, and SSH |
| [Troubleshooting](docs/troubleshooting.md) | Network troubleshooting commands and procedures |

## Screenshots and Verification

Screenshots of network configurations and verification results are stored in the `screenshots/` directory.

Examples include:

- VLAN verification
- Trunk configuration
- ACL verification
- SSH connection testing
- OSPF neighbour verification
- Routing table verification
- DHCP verification
- Network connectivity testing

## Packet Tracer Project

The Cisco Packet Tracer project file is located in:

`packet-tracer/secure-enterprise-network.pkt`

## Learning Outcomes

Through this project, I developed practical skills in:

- Designing and configuring an enterprise network.
- Implementing VLANs and inter-VLAN routing.
- Configuring OSPF for dynamic routing.
- Implementing DHCP for automatic IP address assignment.
- Applying Extended ACLs to control network traffic.
- Configuring SSH for secure remote administration.
- Troubleshooting network connectivity and configuration issues.
- Documenting network infrastructure and configurations.

## Conclusion

This project demonstrates practical experience in enterprise networking, network segmentation, routing, access control, and troubleshooting using Cisco Packet Tracer.

It provides a foundation for further learning in network engineering and cybersecurity.
