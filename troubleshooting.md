# Network Troubleshooting

## Overview

This document describes the troubleshooting procedures used for the Secure Enterprise Network project built using Cisco Packet Tracer.

The purpose is to identify, diagnose, and resolve common network connectivity and configuration issues involving VLANs, trunking, inter-VLAN routing, OSPF, DHCP, ACLs, and SSH.

## 1. VLAN Troubleshooting

### Common Issue

Devices may be unable to communicate because they are assigned to the wrong VLAN or the required VLAN has not been created.

### Verification Command

Run on SW1:

```cisco
show vlan brief
```

### Expected Configuration

| VLAN ID | VLAN Name | Assigned Ports |
|---|---|---|
| 10 | EMPLOYEES | Fa0/1–Fa0/4 |
| 20 | SERVERS | Fa0/5–Fa0/6 |
| 30 | MANAGEMENT | Fa0/7–Fa0/8 |

### Possible Causes

- VLAN has not been created.
- Switch port is assigned to the wrong VLAN.
- Device is connected to an incorrect switch port.

### Troubleshooting Steps

1. Check the VLAN list using `show vlan brief`.
2. Confirm that VLANs 10, 20, and 30 exist.
3. Check that each switch port is assigned to the correct VLAN.
4. Correct any incorrect VLAN assignments.

## 2. Trunk Configuration Troubleshooting

### Common Issue

Devices in different VLANs may experience connectivity problems if the trunk link between SW1 and R2 is not configured correctly.

### Verification Command

Run on SW1:

```cisco
show interfaces trunk
```

### Expected Configuration

- Interface: GigabitEthernet0/1
- Mode: Trunk
- VLANs: 10, 20, 30

### Possible Causes

- Trunk mode is not enabled.
- Incorrect cable connection.
- VLANs are not allowed on the trunk.

### Troubleshooting Steps

1. Check the trunk status using `show interfaces trunk`.
2. Confirm that GigabitEthernet0/1 connects to R2.
3. Check the interface configuration.
4. Correct the trunk configuration if necessary.

Example configuration:

```cisco
configure terminal
interface GigabitEthernet0/1
 switchport mode trunk
 no shutdown
end
```

## 3. Inter-VLAN Routing Troubleshooting

### Common Issue

Devices in different VLANs cannot communicate with each other.

### Verification Commands

Run on R2:

```cisco
show ip interface brief
```

Check the router subinterfaces:

```cisco
show running-config
```

### Expected Gateway Addresses

| Interface | IP Address | VLAN |
|---|---|---|
| G0/1.10 | 192.168.10.1 | 10 |
| G0/1.20 | 192.168.20.1 | 20 |
| G0/1.30 | 192.168.30.1 | 30 |

### Possible Causes

- Router subinterfaces are incorrectly configured.
- Incorrect VLAN ID in the encapsulation configuration.
- Physical router interface is shut down.
- Incorrect default gateway on end devices.

### Troubleshooting Steps

1. Check that the physical interface G0/1 is enabled.
2. Verify the IP addresses of all three subinterfaces.
3. Check the dot1Q VLAN IDs.
4. Confirm that end devices use the correct default gateway.

## 4. OSPF Troubleshooting

### Common Issue

R1 and R2 may fail to exchange routing information if OSPF is incorrectly configured.

### Verification Commands

Run on R1 and R2:

```cisco
show ip ospf neighbor
```

Check the routing table:

```cisco
show ip route
```

Check OSPF configuration:

```cisco
show running-config
```

### Expected Configuration

| Device | Router ID | OSPF Area |
|---|---|---|
| R1 | 1.1.1.1 | Area 0 |
| R2 | 2.2.2.2 | Area 0 |

The R1-R2 connection uses:

- R1: 192.168.99.1/30
- R2: 192.168.99.2/30

### Possible Causes

- Incorrect OSPF network statement.
- Incorrect router ID.
- R1-R2 link is down.
- OSPF is configured on the wrong interface.

### Troubleshooting Steps

1. Check the R1-R2 connection using `ping`.
2. Verify the interface IP addresses.
3. Check the OSPF neighbour table.
4. Confirm that both routers use OSPF area 0.
5. Check the routing table for OSPF routes.

## 5. DHCP Troubleshooting

### Common Issue

Employee PCs may fail to obtain IP addresses automatically.

### Verification Commands

Run on R2:

```cisco
show ip dhcp binding
show ip dhcp pool
```

On an employee PC, open Desktop > IP Configuration and check whether DHCP is selected.

### Expected DHCP Configuration

| Setting | Value |
|---|---|
| Network | 192.168.10.0/24 |
| Default Gateway | 192.168.10.1 |
| DNS Server | 8.8.8.8 |

### Possible Causes

- DHCP pool is incorrectly configured.
- DHCP service is unavailable.
- PC is connected to the wrong VLAN.
- Router subinterface is down.

### Troubleshooting Steps

1. Check the DHCP pool on R2.
2. Verify that the PC is connected to a VLAN 10 switch port.
3. Confirm that R2 G0/1.10 is operational.
4. Renew or reselect DHCP in the PC's IP Configuration window.

## 6. ACL Troubleshooting

### Common Issue

Network traffic may be blocked because of an incorrect ACL rule or incorrect interface application.

### Verification Commands

Run on R2:

```cisco
show access-lists
```

Check ACL application:

```cisco
show ip interface gigabitEthernet 0/1.10
```

### Expected ACL Configuration

```cisco
ip access-list extended EMPLOYEE-RESTRICTION
 deny ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255
 permit ip any any
```

The ACL should be applied inbound on R2 G0/1.10.

### Expected Behaviour

| Source | Destination | Expected Result |
|---|---|---|
| PC1 (VLAN 10) | PC5 (VLAN 30) | Blocked |
| PC1 (VLAN 10) | Server1 (VLAN 20) | Permitted by ACL |

### Troubleshooting Steps

1. Check the ACL rules using `show access-lists`.
2. Confirm that the ACL is applied inbound on G0/1.10.
3. Verify the source and destination network addresses.
4. Test connectivity using `ping`.
5. Check ACL match counters to see whether traffic matches the rules.

## 7. SSH Troubleshooting

### Common Issue

Administrators may be unable to connect remotely to R2 or SW1 using SSH.

### Verification Commands

Run on R2 and SW1:

```cisco
show ip ssh
show running-config
```

### Expected SSH Configuration

- SSH version 2 enabled.
- Domain name configured.
- Local username configured.
- RSA keys generated.
- VTY lines configured with local login.
- VTY access restricted to SSH.

### SSH Connection Tests

From PC5 in VLAN 30:

Connect to R2:

```bash
ssh -l admin 192.168.30.1
```

Connect to SW1:

```bash
ssh -l admin 192.168.30.2
```

### Possible Causes

- SSH has not been enabled.
- RSA keys have not been generated.
- Incorrect username or password.
- Incorrect management IP address.
- VTY lines are not configured for SSH.
- Management VLAN connectivity is unavailable.

### Troubleshooting Steps

1. Check SSH status using `show ip ssh`.
2. Verify the local username configuration.
3. Confirm that RSA keys have been generated.
4. Check the VTY line configuration.
5. Test connectivity to the management IP using `ping`.
6. Attempt the SSH connection again.

## 8. General Network Troubleshooting Commands

The following commands are useful for diagnosing network problems.

| Command | Purpose |
|---|---|
| `show ip interface brief` | Checks interface status and IP addresses |
| `show vlan brief` | Displays VLAN configuration |
| `show interfaces trunk` | Checks trunk connections |
| `show ip route` | Displays the routing table |
| `show ip ospf neighbor` | Checks OSPF neighbours |
| `show access-lists` | Displays ACL configuration |
| `show ip ssh` | Checks SSH status |
| `ping` | Tests network connectivity |
| `traceroute` | Identifies the network path |

## 9. Conclusion

Troubleshooting is an important part of maintaining a reliable and secure enterprise network.

This project demonstrates how network administrators can use Cisco IOS commands to identify and diagnose common network issues involving VLANs, trunking, inter-VLAN routing, OSPF, DHCP, ACLs, and SSH.

These troubleshooting procedures help develop practical networking skills and demonstrate the ability to diagnose and resolve network configuration problems using Cisco Packet Tracer.
