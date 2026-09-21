# Network Verification

This document records the verification tests performed after implementing the Small Office Network in Cisco Packet Tracer.

---

## 1. Router Routing Table

Command:

```cisco
show ip route
```

Verified directly connected networks:

```text
C 192.168.10.0/24
C 192.168.20.0/24
```

**Result: PASS ✅**

---

## 2. Router → SW1 Management

Command:

```cisco
ping 192.168.20.2
```

**Result: Successful ✅**

The router successfully reached the switch management SVI.

---

## 3. VLAN 10 → VLAN 20

From the VLAN 10 PC:

```text
ping 192.168.20.10
```

**Result: Successful ✅**

This confirms inter-VLAN routing from the USERS VLAN to the MANAGEMENT VLAN.

---

## 4. VLAN 20 → VLAN 10

From the VLAN 20 PC:

```text
ping 192.168.10.10
```

**Result: Successful ✅**

This confirms bidirectional inter-VLAN communication.

---

## 5. VLAN 10 Gateway

From the VLAN 10 PC:

```text
ping 192.168.10.1
```

**Result: Successful ✅**

---

## 6. VLAN 20 Gateway

From the VLAN 20 PC:

```text
ping 192.168.20.1
```

**Result: Successful ✅**

---

## 7. Switch Management Connectivity

From the VLAN 10 PC:

```text
ping 192.168.20.2
```

**Result: Successful ✅**

The switch management SVI was reachable across VLANs.

---

## 8. DHCP Verification

### VLAN 10 — USERS

The VLAN 10 PC successfully received DHCP configuration:

```text
IP Address:      192.168.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

**Result: PASS ✅**

### VLAN 20 — MANAGEMENT

The VLAN 20 PC successfully received DHCP configuration:

```text
IP Address:      192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1
```

**Result: PASS ✅**

---

## 9. SSH Verification

Command:

```cisco
show ip ssh
```

Verified:

```text
SSH Enabled - version 2.0
Authentication timeout: 120 secs
Authentication retries: 3
```

**Result: PASS ✅**

SSH connectivity was also successfully tested during troubleshooting.

---

## 10. Port Security Verification

Command:

```cisco
show port-security
```

Verified:

```text
Fa0/1
Maximum MAC addresses: 1
Current MAC addresses: 1
Security violations: 0
Violation action: Shutdown

Fa0/2
Maximum MAC addresses: 1
Current MAC addresses: 1
Security violations: 0
Violation action: Shutdown
```

**Result: PASS ✅**

---

## 11. Unused Interface Verification

Unused FastEthernet and GigabitEthernet interfaces were administratively shut down.

Verified interfaces include:

```text
Fa0/4–Fa0/24
Gi0/1
Gi0/2
```

**Result: PASS ✅**

---

## 12. Configuration Persistence

Running configurations were saved to startup configuration on both the switch and router.

Command:

```cisco
copy running-config startup-config
```

**Result: PASS ✅**

---

# Final Verification Summary

| Verification          | Result |
| --------------------- | ------ |
| VLAN 10               | PASS ✅ |
| VLAN 20               | PASS ✅ |
| Router-on-a-Stick     | PASS ✅ |
| Inter-VLAN Routing    | PASS ✅ |
| DHCP VLAN 10          | PASS ✅ |
| DHCP VLAN 20          | PASS ✅ |
| Router → SW1          | PASS ✅ |
| VLAN 10 → VLAN 20     | PASS ✅ |
| VLAN 20 → VLAN 10     | PASS ✅ |
| SSH Version 2         | PASS ✅ |
| Port Security         | PASS ✅ |
| Unused Ports Shutdown | PASS ✅ |
| Configuration Saved   | PASS ✅ |

## Project Status

**Technical verification: COMPLETE ✅**
