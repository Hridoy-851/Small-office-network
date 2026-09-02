# Small Office Network — Cisco Packet Tracer

## Project Overview

This project is a small office network built and configured using **Cisco Packet Tracer**.

The project started with a basic switched network and was progressively expanded to include VLANs, trunking, and inter-VLAN routing using a Cisco router.

The main goal is to practice fundamental networking concepts and Cisco device configuration as part of my **CCNA and Junior Network Engineer learning journey**.

---

## Network Topology

Current topology:

```text
                    ┌──────────────┐
                    │   Router     │
                    │    G0/0      │
                    └──────┬───────┘
                           │
                        Trunk
                           │
                    ┌──────┴───────┐
                    │     SW1      │
                    │    Switch    │
                    └───┬──────┬───┘
                        │      │
                     Fa0/1   Fa0/2
                        │      │
                       PC0    PC1
                    VLAN 10  VLAN 20
```

---

## Devices Used

* 1 × Cisco Router
* 1 × Cisco Switch
* 2 × PCs
* Cisco Packet Tracer

---

## IP Addressing

| Device | IP Address      | Subnet Mask     | VLAN    | Default Gateway |
| ------ | --------------- | --------------- | ------- | --------------- |
| PC0    | `192.168.10.10` | `255.255.255.0` | VLAN 10 | `192.168.10.1`  |
| PC1    | `192.168.20.10` | `255.255.255.0` | VLAN 20 | `192.168.20.1`  |

### Router

| Interface | VLAN    | IP Address        |
| --------- | ------- | ----------------- |
| G0/0.10   | VLAN 10 | `192.168.10.1/24` |
| G0/0.20   | VLAN 20 | `192.168.20.1/24` |

---

## VLAN Configuration

Two VLANs were created on the switch:

| VLAN ID | Name       | Assigned Port | Device |
| ------- | ---------- | ------------- | ------ |
| 10      | USERS      | Fa0/1         | PC0    |
| 20      | MANAGEMENT | Fa0/2         | PC1    |

### Access Ports

* `Fa0/1` → VLAN 10 → PC0
* `Fa0/2` → VLAN 20 → PC1

The ports were configured as access ports because each port connects to an end device belonging to a single VLAN.

---

## Trunk Configuration

The connection between the switch and router uses:

```text
SW1 Fa0/3 → Router G0/0
```

`Fa0/3` was configured as an **802.1Q trunk**.

The trunk allows multiple VLANs to travel between the switch and router.

Verified VLANs on the trunk:

```text
1, 10, 20
```

---

## Inter-VLAN Routing

Because PC0 and PC1 belong to different VLANs, they cannot communicate directly through Layer 2 switching.

A Cisco router was configured using **Router-on-a-Stick** to provide communication between the VLANs.

### Router Subinterfaces

#### VLAN 10

```text
interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
```

#### VLAN 20

```text
interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

The router acts as the default gateway for each VLAN.

---

## Verification and Testing

The following commands were used to verify the configuration.

### Check VLANs

```text
show vlan brief
```

This verified that:

* `Fa0/1` belongs to VLAN 10
* `Fa0/2` belongs to VLAN 20

### Check Trunk

```text
show interfaces trunk
```

The output confirmed:

```text
Fa0/3       802.1q       trunking
```

and VLANs 10 and 20 were active on the trunk.

### Connectivity Test

PC0:

```text
192.168.10.10
```

successfully pinged PC1:

```text
192.168.20.10
```

This confirmed that **inter-VLAN routing was working correctly**.

---

## Networking Concepts Practiced

Through this project, I practiced:

* IPv4 addressing
* Subnet masks
* Default gateways
* MAC address learning
* MAC address tables
* ARP
* Ethernet switching
* VLANs
* VLAN 1
* Access ports
* Trunk ports
* IEEE 802.1Q
* Router subinterfaces
* Router-on-a-Stick
* Inter-VLAN routing
* Basic network troubleshooting
* Connectivity testing with `ping`
* Cisco IOS commands

---

## Troubleshooting Practice

During the project, communication initially failed after placing the PCs into different VLANs.

The issue was investigated by checking:

1. VLAN assignments
2. IP addressing
3. Default gateways
4. Switch port configuration
5. Trunk configuration
6. Router subinterfaces

After configuring the router and trunk correctly, communication between VLAN 10 and VLAN 20 was successfully established.

This helped demonstrate the difference between **Layer 2 switching** and **Layer 3 routing**.

---

## Key Learning

### Before VLANs

Both PCs were in the same VLAN and subnet:

```text
PC0 ─── Switch ─── PC1
        VLAN 1

Ping → Successful
```

### After VLANs

The PCs were separated:

```text
PC0 ─── VLAN 10
          │
        Switch
          │
PC1 ─── VLAN 20

Ping → Failed
```

### After Inter-VLAN Routing

A router was introduced:

```text
PC0
192.168.10.10
     │
 VLAN 10
     │
    SW1
     │
   Trunk
     │
   Router
     │
 VLAN 20
     │
    SW1
     │
PC1
192.168.20.10

Ping → Successful
```

This demonstrates that communication between different VLANs requires **Layer 3 routing**.

---

## Technologies and Tools

* Cisco Packet Tracer
* Cisco IOS
* IPv4
* Ethernet
* VLAN
* 802.1Q
* Inter-VLAN Routing

---

## Learning Progress

* [x] Basic LAN topology
* [x] IPv4 addressing
* [x] Subnet masks
* [x] Basic switching
* [x] MAC address learning
* [x] MAC address table
* [x] ARP
* [x] VLAN fundamentals
* [x] VLAN 10 configuration
* [x] VLAN 20 configuration
* [x] Access ports
* [x] Trunk ports
* [x] 802.1Q
* [x] Router subinterfaces
* [x] Router-on-a-Stick
* [x] Inter-VLAN routing
* [x] Basic troubleshooting
* [ ] DHCP
* [ ] Static routing
* [ ] OSPF
* [ ] ACLs
* [ ] NAT
* [ ] Network security fundamentals

---

## Project File

The Packet Tracer topology is available in:

```text
small-office-network.pkt
```

This project will be continuously improved as I progress through my **CCNA and Junior Network Engineer learning roadmap**.
