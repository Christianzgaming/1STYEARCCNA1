# Cisco Packet Tracer — Topology 2 Configuration Guide

> **Topology:** 10.10.x.x IPv4 networks with IPv6 addressing  
> **Goal:** Configure the `Floor14` router, the accessible `Room-146` switch, and four PCs. Complete the addressing table and verify connectivity.

---

## Table of Contents

1. [Addressing Table — Default Gateways](#1-addressing-table--default-gateways)
2. [Configure the Floor14 Router](#2-configure-the-floor14-router)
3. [Configure the Room-146 Switch](#3-configure-the-room-146-switch)
4. [Configure the PCs](#4-configure-the-pcs)
5. [Verify Connectivity and Score](#5-verify-connectivity-and-score)
6. [Troubleshooting Checklist](#6-troubleshooting-checklist)
7. [Quick Reference Tables](#7-quick-reference-tables)

---

## 1. Addressing Table — Default Gateways

Complete the missing **Default Gateway** values in the activity's addressing table:

| Device / Interface | Default Gateway |
|---|---|
| Room-145 switch — VLAN 1 | `10.10.10.1` |
| Room-146 switch — VLAN 1 | `10.10.11.1` |

> **Note:** The Room-145 switch is not accessible in this activity, so do not attempt to configure it. The table entry above is the gateway value to record.

---

## 2. Configure the Floor14 Router

### Step 1 — Open the CLI

1. Click the **Floor14** router.
2. Select the **CLI** tab.
3. Press **Enter** until the router prompt appears.
4. Enter the following commands on the router.

### Step 2 — Enter the complete configuration

```cisco
enable
configure terminal

! Basic security and hostname
hostname Floor14
enable secret class
service password-encryption
banner motd #Authorized Access Only#

! Console password
line console 0
 password cisco
 login
 exit

! VTY password
line vty 0 4
 password cisco
 login
 exit

! G0/0 — Room-145 / left-side network
interface g0/0
 description Connection to Room-145
 ip address 10.10.10.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:100::1/64
 ipv6 address FE80::2 link-local
 no shutdown
 exit

! G0/1 — Room-146 / right-side network
interface g0/1
 description Connection to Room-146
 ip address 10.10.11.1 255.255.255.0
 ipv6 address 2001:DB8:ACAD:200::1/64
 ipv6 address FE80::3 link-local
 no shutdown
 exit

! Enable IPv6 routing
ipv6 unicast-routing

! Finish and save
end
write memory
```

### Step 3 — Verify router interfaces

Run:

```cisco
show ip interface brief
show ipv6 interface brief
show running-config
```

Check that `G0/0` uses `10.10.10.1/24`, global IPv6 `2001:DB8:ACAD:100::1/64`, and link-local `FE80::2`. Check that `G0/1` uses `10.10.11.1/24`, global IPv6 `2001:DB8:ACAD:200::1/64`, and link-local `FE80::3`. Both interfaces should have `no shutdown`, and `ipv6 unicast-routing` should be configured.

---

## 3. Configure the Room-146 Switch

> Configure **Room-146 only**. The Room-145 switch is not accessible in this activity.

### Step 1 — Open the CLI

1. Click the **Room-146** switch.
2. Select the **CLI** tab.
3. Press **Enter** until the switch prompt appears.

### Step 2 — Enter the complete configuration

```cisco
enable
configure terminal

! Basic security and hostname
hostname Room-146
enable secret class
service password-encryption
banner motd #Authorized Access Only#

! Console password
line console 0
 password cisco
 login
 exit

! VTY password
line vty 0 4
 password cisco
 login
 exit

! VLAN 1 management interface
interface vlan 1
 description Management Interface
 ip address 10.10.11.100 255.255.255.0
 no shutdown
 exit

! Default gateway for switch management
ip default-gateway 10.10.11.1

! Finish and save
end
write memory
```

### Step 3 — Verify the switch

Run:

```cisco
show ip interface brief
show running-config
show vlan brief
```

Confirm that the hostname is `Room-146`, VLAN 1 has IP `10.10.11.100` with mask `255.255.255.0`, and the default gateway is `10.10.11.1`. VLAN 1 may remain down until an active switch port in VLAN 1 is connected; if so, check the connected ports and cabling.

---

## 4. Configure the PCs

> **Important:** PCs are configured in **Desktop → IP Configuration**, not in the router or switch CLI.

### How to configure each PC

1. Click the PC.
2. Open the **Desktop** tab.
3. Select **IP Configuration**.
4. Enter the IPv4 address, subnet mask, and default gateway.
5. Enter the IPv6 address and set the prefix length to `64`.
6. Enter the IPv6 gateway shown for that PC.
7. Repeat for all four PCs.

### Manager-A — Left side / Room-145

| Setting | Value |
|---|---|
| IPv4 Address | `10.10.10.101` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.10.10.1` |
| IPv6 Address | `2001:DB8:ACAD:100::50` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::2` |

### Reception-A — Left side / Room-145

| Setting | Value |
|---|---|
| IPv4 Address | `10.10.10.102` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.10.10.1` |
| IPv6 Address | `2001:DB8:ACAD:100::60` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::2` |

### Manager-B — Right side / Room-146

| Setting | Value |
|---|---|
| IPv4 Address | `10.10.11.101` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.10.11.1` |
| IPv6 Address | `2001:DB8:ACAD:200::50` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::3` |

### Reception-B — Right side / Room-146

| Setting | Value |
|---|---|
| IPv4 Address | `10.10.11.102` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.10.11.1` |
| IPv6 Address | `2001:DB8:ACAD:200::60` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::3` |

### PC addressing overview

| PC | IPv4 Address | IPv4 Gateway | IPv6 Address | IPv6 Gateway |
|---|---|---|---|---|
| Manager-A | `10.10.10.101/24` | `10.10.10.1` | `2001:DB8:ACAD:100::50/64` | `FE80::2` |
| Reception-A | `10.10.10.102/24` | `10.10.10.1` | `2001:DB8:ACAD:100::60/64` | `FE80::2` |
| Manager-B | `10.10.11.101/24` | `10.10.11.1` | `2001:DB8:ACAD:200::50/64` | `FE80::3` |
| Reception-B | `10.10.11.102/24` | `10.10.11.1` | `2001:DB8:ACAD:200::60/64` | `FE80::3` |

---

## 5. Verify Connectivity and Score

### Step 1 — Test IPv4

On each PC, open **Desktop → Command Prompt**.

From `Manager-A`, test its router gateway:

```text
ping 10.10.10.1
```

Test another PC on the same network:

```text
ping 10.10.10.102
```

Then test a PC on the other network:

```text
ping 10.10.11.101
```

### Step 2 — Test IPv6

From `Manager-A`, try:

```text
ping 2001:DB8:ACAD:100::1
ping 2001:DB8:ACAD:200::50
```

If the first ping times out, wait briefly and try again. Confirm the IPv6 addresses, prefix length, gateways, router interface status, and cabling.

### Step 3 — Save and check the activity

1. Confirm `write memory` was run on both the router and switch.
2. Save the Packet Tracer file using **File → Save**.
3. Click **Check Results**.
4. Review incomplete assessment items and correct the listed settings.

> **Score note:** The target is **100%**, but the exact result depends on the assessment rules in your `.pka` file and whether it includes requirements beyond those listed here.

---

## 6. Troubleshooting Checklist

- [ ] Commands were entered on the correct device.
- [ ] Router hostname is `Floor14`.
- [ ] `G0/0` uses `10.10.10.1/24` and `2001:DB8:ACAD:100::1/64`.
- [ ] `G0/0` link-local address is `FE80::2`.
- [ ] `G0/1` uses `10.10.11.1/24` and `2001:DB8:ACAD:200::1/64`.
- [ ] `G0/1` link-local address is `FE80::3`.
- [ ] `ipv6 unicast-routing` is enabled.
- [ ] Room-146 switch management address is `10.10.11.100/24`.
- [ ] Room-146 switch default gateway is `10.10.11.1`.
- [ ] All PCs have the correct IPv4 addresses, masks, and gateways.
- [ ] All PCs have the correct IPv6 addresses, prefix length `64`, and gateways.
- [ ] Router interfaces are enabled with `no shutdown`.
- [ ] Cables and ports are correct, and links are active.
- [ ] Router and switch configurations were saved with `write memory`.
- [ ] **Check Results** was reviewed for extra assessment requirements.

---

## 7. Quick Reference Tables

### Router interfaces

| Interface | Network | IPv4 Address | IPv6 Global Address | IPv6 Link-Local |
|---|---|---|---|---|
| `G0/0` | Room-145 / left | `10.10.10.1/24` | `2001:DB8:ACAD:100::1/64` | `FE80::2` |
| `G0/1` | Room-146 / right | `10.10.11.1/24` | `2001:DB8:ACAD:200::1/64` | `FE80::3` |

### Switch management

| Setting | Value |
|---|---|
| Hostname | `Room-146` |
| VLAN 1 management IP | `10.10.11.100/24` |
| Default gateway | `10.10.11.1` |
| Enable secret | `class` |
| Console / VTY password | `cisco` |
| MOTD banner | `Authorized Access Only!` |

### Final reminders

- Use the **CLI** tab for the router and switch.
- Use **Desktop → IP Configuration** for each PC.
- Pay special attention to link-local gateways: `FE80::2` on the left-side network and `FE80::3` on the right-side network.
- Save device configurations, then confirm the actual result with **Check Results**.
