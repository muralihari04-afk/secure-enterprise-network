# VLAN Design Documentation

## 1. Overview

This document explains the VLAN design and implementation of the Secure Enterprise Network project using Cisco Packet Tracer.

VLANs (Virtual Local Area Networks) are used to logically separate devices into different network segments. This improves network organisation, reduces unnecessary broadcast traffic and allows access between departments to be controlled.

The network uses three VLANs: Employees, Servers and Management.

## 2. VLAN Design

The network is divided into three VLANs based on device roles and responsibilities.

| VLAN ID | VLAN Name | Purpose | Network Address |
|---|---|---|---|
| 10 | EMPLOYEES | Employee workstations | 192.168.10.0/24 |
| 20 | SERVERS | Company servers | 192.168.20.0/24 |
| 30 | MANAGEMENT | Network administration devices | 192.168.30.0/24 |

## 3. Device and Port Assignment

The following table shows how devices are assigned to VLANs on SW1.

| Switch Port | Connected Device | VLAN |
|---|---|---|
| Fa0/1 | PC1 | 10 |
| Fa0/2 | PC2 | 10 |
| Fa0/3 | PC3 | 10 |
| Fa0/4 | PC4 | 10 |
| Fa0/5 | Server1 | 20 |
| Fa0/6 | Server2 | 20 |
| Fa0/7 | PC5 | 30 |
| Fa0/8 | PC6 | 30 |
| Gi0/1 | R2 | Trunk |

## 4. VLAN Configuration

The VLANs were created on Cisco Switch SW1 using the following commands.

### Create VLANs

```cisco
vlan 10
name EMPLOYEES
exit

vlan 20
name SERVERS
exit

vlan 30
name MANAGEMENT
exit
```

### Assign Employee Ports

```cisco
interface range fastEthernet 0/1-4
switchport mode access
switchport access vlan 10
exit
```

### Assign Server Ports

```cisco
interface range fastEthernet 0/5-6
switchport mode access
switchport access vlan 20
exit
```

### Assign Management Ports

```cisco
interface range fastEthernet 0/7-8
switchport mode access
switchport access vlan 30
exit
```

## 5. Trunk Configuration

A trunk connection is configured between SW1 and R2.

The trunk allows traffic from multiple VLANs to travel through a single physical connection using IEEE 802.1Q tagging.

Configuration:

```cisco
interface gigabitEthernet 0/1
description TRUNK-TO-R2
switchport mode trunk
no shutdown
exit
```

## 6. Inter-VLAN Routing

Inter-VLAN routing is implemented on R2 using Router-on-a-Stick.

R2 uses subinterfaces to provide a default gateway for each VLAN.

| Interface | VLAN | IP Address |
|---|---|---|
| G0/1.10 | 10 | 192.168.10.1 |
| G0/1.20 | 20 | 192.168.20.1 |
| G0/1.30 | 30 | 192.168.30.1 |

This allows communication between VLANs through the router, subject to the configured access control rules.

## 7. Security Implementation

VLAN segmentation separates employees, servers and management devices into different broadcast domains.

An extended Access Control List (ACL) is configured on R2 to prevent employee devices in VLAN 10 from directly accessing VLAN 30.

This provides an additional layer of access control between network segments.

## 8. Conclusion

The VLAN design provides logical separation between employees, servers and management devices.

By implementing VLANs and inter-VLAN routing, the network achieves better organisation, controlled communication and a structured enterprise network architecture.

## 9. VLAN Verification Results

The VLAN configuration was verified on SW1 using the following command:

```cisco
show vlan brief
```

The output confirmed that all three VLANs were successfully created and are active.

| VLAN ID | VLAN Name | Assigned Ports | Status |
|---|---|---|---|
| 10 | EMPLOYEES | Fa0/1–Fa0/4 | Active |
| 20 | SERVERS | Fa0/5–Fa0/6 | Active |
| 30 | MANAGEMENT | Fa0/7–Fa0/8 | Active |

### Verification Findings

- VLAN 10 successfully contains PC1–PC4.
- VLAN 20 successfully contains Server1 and Server2.
- VLAN 30 successfully contains PC5 and PC6.
- All three VLANs show an active status.
- Unused ports Fa0/9–Fa0/24 and Gi0/2 remain assigned to the default VLAN 1.

### Verification Command

```cisco
SW1# show vlan brief
```

**Result:** The VLAN creation and access-port assignments were successfully verified on SW1.
