# Troubleshooting

This document records the main troubleshooting process performed during the implementation of the Small Office Network.

---

## Issue 1 — SSH Authentication Failure

### Symptom

SSH connectivity to the switch management IP was reachable, but authentication using the configured `admin` account was unsuccessful.

The command used from a network device was:

```text
ssh -l admin 192.168.20.2
```

The login returned:

```text
% Login invalid
```

---

### Investigation

The issue was investigated systematically rather than assuming the problem was network connectivity.

#### Step 1 — Verify Management Connectivity

The switch management SVI was configured as:

```text
192.168.20.2/24
```

The default gateway was:

```text
192.168.20.1
```

Connectivity was confirmed with:

```text
ping 192.168.20.2
```

The ping was successful.

**Conclusion:** The management network was reachable.

---

### Step 2 — Verify SSH Version

Command:

```cisco
show ip ssh
```

Output confirmed:

```text
SSH Enabled - version 2.0
```

**Conclusion:** SSH version was correctly configured.

---

### Step 3 — Verify VTY Configuration

The VTY lines were configured for local authentication and SSH only:

```cisco
line vty 0 4
 login local
 transport input ssh

line vty 5 15
 login local
 transport input ssh
```

**Conclusion:** VTY configuration was appropriate for SSH access.

---

### Step 4 — Isolate Authentication

A temporary local user was created specifically to test SSH authentication.

The temporary account successfully connected through SSH.

This confirmed that:

* Network connectivity was working.
* The management SVI was working.
* SSH was enabled.
* SSH version 2 was working.
* VTY configuration was working.
* Local authentication was functioning.

The temporary test account was removed after verification.

---

### Resolution

The investigation isolated the issue to the original `admin` account rather than the network or SSH service.

The SSH functionality itself was successfully verified.

---

## Troubleshooting Lesson

This issue demonstrated the importance of troubleshooting network problems layer by layer.

Instead of immediately changing multiple configurations, the investigation separated:

```text
Connectivity
     ↓
Management IP
     ↓
SSH Service
     ↓
VTY Configuration
     ↓
Authentication
     ↓
User Account
```

This approach prevents unnecessary configuration changes and helps identify the actual source of a problem.

---

## Issue 2 — Inter-VLAN Connectivity Verification

### Objective

Verify communication between VLAN 10 and VLAN 20.

### Tests

From VLAN 10:

```text
ping 192.168.20.10
```

Result:

```text
Successful
```

From VLAN 20:

```text
ping 192.168.10.10
```

Result:

```text
Successful
```

### Conclusion

Router-on-a-stick inter-VLAN routing was functioning correctly.

---

## Issue 3 — Management Connectivity Verification

The switch management interface was tested from the router and VLAN 10 PC.

Router:

```text
ping 192.168.20.2
```

Result:

```text
Successful
```

VLAN 10 PC:

```text
ping 192.168.20.2
```

Result:

```text
Successful
```

### Conclusion

The SW1 management SVI and default gateway configuration were functioning correctly.

---

## Verification Commands Used

The following commands were used during troubleshooting and final verification:

```cisco
show ip route
show ip ssh
show port-security
show running-config
ping
ipconfig
copy running-config startup-config
```

---

## Troubleshooting Approach

The general troubleshooting process used in this project was:

1. Identify the symptom.
2. Verify physical/logical connectivity.
3. Check IP addressing.
4. Check VLAN membership.
5. Check trunking.
6. Check routing.
7. Check the relevant service.
8. Isolate authentication or configuration issues.
9. Test the suspected cause.
10. Verify the final result.

---

## Final Result

All core network functions were successfully verified.

**Troubleshooting and verification: COMPLETE ✅**
