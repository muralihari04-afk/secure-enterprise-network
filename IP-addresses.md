# IP Addressing Documentation

## 1. Overview

This document describes the IP addressing scheme used in the Secure Enterprise Network project.

The network uses private IPv4 addresses to organise devices into separate VLANs. Each VLAN has its own subnet and default gateway to support network communication and segmentation.

## 2. VLAN IP Addressing

| VLAN | Department | Network Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| VLAN 10 | Employees | 192.168.10.0/24 | 255.255.255.0 | 192.168.10.1 |
| VLAN 20 | Servers | 192.168.20.0/24 | 255.255.255.0 | 192.168.20.1 |
| VLAN 30 | Management | 192.168.30.0/24 | 255.255.255.0 | 192.168.30.1 |

## 3. Router IP Addressing

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R1 | GigabitEthernet 0/0 | 192.168.99.1 | 255.255.255.252 |
| R2 | GigabitEthernet 0/0 | 192.168.99.2 | 255.255.255.252 |
| R2 | GigabitEthernet 0/1.10 | 192.168.10.1 | 255.255.255.0 |
| R2 | GigabitEthernet 0/1.20 | 192.168.20.1 | 255.255.255.0 |
| R2 | GigabitEthernet 0/1.30 | 192.168.30.1 | 255.255.255.0 |

## 4. End Device IP Addressing

| Device | VLAN | IP Address | Default Gateway |
|---|---|---|---|
| PC1 | 10 | DHCP | 192.168.10.1 |
| PC2 | 10 | DHCP | 192.168.10.1 |
| PC3 | 10 | DHCP | 192.168.10.1 |
| PC4 | 10 | DHCP | 192.168.10.1 |
| Server1 | 20 | 192.168.20.10 | 192.168.20.1 |
| Server2 | 20 | 192.168.20.11 | 192.168.20.1 |
| PC5 | 30 | 192.168.30.10 | 192.168.30.1 |
| PC6 | 30 | 192.168.30.11 | 192.168.30.1 |

## 5. Switch Management IP Address

The switch uses a management IP address on VLAN 30.

| Device | Interface | IP Address | Default Gateway |
|---|---|---|---|
| SW1 | VLAN 30 | 192.168.30.2 | 192.168.30.1 |

## 6. Subnetting Explanation

The network uses a /24 subnet mask (255.255.255.0) for the three VLANs.

Each /24 subnet provides:

- 256 total IP addresses.
- 254 usable host addresses.
- 1 network address.
- 1 broadcast address.

The R1–R2 connection uses a /30 subnet mask (255.255.255.252), which provides two usable host addresses for the point-to-point connection.

## 7. DHCP Address Allocation

R2 provides DHCP services for VLAN 10 (Employees).

The DHCP pool automatically assigns IP addresses to PC1, PC2, PC3 and PC4.

The address range 192.168.10.1–192.168.10.20 is excluded from DHCP allocation to reserve addresses for network infrastructure and other static assignments.

## 8. Conclusion

The IP addressing scheme separates employees, servers and management devices into different subnets. This provides an organised network structure and supports inter-VLAN routing, access control and network administration.
