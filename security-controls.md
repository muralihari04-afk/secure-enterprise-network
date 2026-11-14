# Security Controls

## Overview

This document describes the security controls implemented in the Secure Enterprise Network project using Cisco Packet Tracer.

The network uses VLAN segmentation, Access Control Lists (ACLs), and Secure Shell (SSH) to improve network security and control access between different network segments.

## 1. VLAN Segmentation

VLANs are used to separate devices into different logical network segments.

This helps reduce unnecessary communication between departments and provides better network organisation.

### VLAN Configuration

| VLAN ID | VLAN Name | Network Address | Purpose |
|---|---|---|---|
| 10 | EMPLOYEES | 192.168.10.0/24 | Employee workstations |
| 20 | SERVERS | 192.168.20.0/24 | Company servers |
| 30 | MANAGEMENT | 192.168.30.0/24 | Network administration devices |

### Security Benefits

- Separates employees, servers, and management devices.
- Reduces unnecessary communication between network segments.
- Allows traffic between VLANs to be controlled using ACLs.
- Improves network organisation and access management.

## 2. Access Control List (ACL)

An Extended ACL is configured on Router R2 to restrict communication from the employee network to the management network.

### ACL Configuration

The ACL named `EMPLOYEE-RESTRICTION` contains the following rules:

```cisco
ip access-list extended EMPLOYEE-RESTRICTION
 deny ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255
 permit ip any any
```
### SSH Configuration on R2 and SW1

SSH is configured on Router R2 and Switch SW1 to provide secure remote administration.

The following configuration is applied to both devices.

```cisco
ip domain-name company.local
username admin secret <LAB_PASSWORD>
crypto key generate rsa
ip ssh version 2

line vty 0 15
 login local
 transport input ssh
