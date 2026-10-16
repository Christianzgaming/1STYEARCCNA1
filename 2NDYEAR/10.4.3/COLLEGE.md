# Cisco Packet Tracer — Topology 3 COLLEGE Configuration Guide
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/45eb8681-92c4-4a06-a89b-59dfb986524a" />

> **Topology:** 128.107.x.x IPv4 networks with IPv6 addressing  
> **Goal:** Configure the `College` router, the accessible `Class-B` switch, and four PCs. Complete the addressing table and verify connectivity.

---

## Table of Contents

1. [Addressing Table — Default Gateways](#1-addressing-table--default-gateways)
2. [Configure the College Router](#2-configure-the-college-router)
3. [Configure the Class-B Switch](#3-configure-the-class-b-switch)
4. [Configure the PCs](#4-configure-the-pcs)
5. [Verify Connectivity and Score](#5-verify-connectivity-and-score)
6. [Troubleshooting Checklist](#6-troubleshooting-checklist)
7. [Quick Reference Tables](#7-quick-reference-tables)

---

## 1. Addressing Table — Default Gateways

Complete the missing **Default Gateway** values in the activity's addressing table:

| Device / Interface | Default Gateway |
|---|---|
| Class-A switch — VLAN 1 | `128.107.20.1` |
| Class-B switch — VLAN 1 | `128.107.30.1` |

> **Note:** The Class-A switch is not accessible in this activity, so do not attempt to configure it. The table entry above is the gateway value to record.

---

## 2. Configure the College Router

### Step 1 — Open the CLI

1. Click the **College** router.
2. Select the **CLI** tab.
3. Press **Enter** until the router prompt appears.
4. Enter the following commands on the router.

### Step 2 — Enter the complete configuration

```cisco
enable
configure terminal

! Basic security and hostname
hostname College
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

! G0/0 — Class-A / left-side network
interface g0/0
 description Connection to Class-A
 ip address 128.107.20.1 255.255.255.0
 ipv6 address 2001:DB8:A::1/64
 ipv6 address FE80::1 link-local
 no shutdown
 exit

! G0/1 — Class-B / right-side network
interface g0/1
 description Connection to Class-B
 ip address 128.107.30.1 255.255.255.0
 ipv6 address 2001:DB8:B::1/64
 ipv6 address FE80::1 link-local
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

Check that `G0/0` uses `128.107.20.1/24`, global IPv6 `2001:DB8:A::1/64`, and link-local `FE80::1`. Check that `G0/1` uses `128.107.30.1/24`, global IPv6 `2001:DB8:B::1/64`, and link-local `FE80::1`. Both interfaces should have `no shutdown`, and `ipv6 unicast-routing` should be configured.

---

## 3. Configure the Class-B Switch

> Configure **Class-B only**. The Class-A switch is not accessible in this activity.

### Step 1 — Open the CLI

1. Click the **Class-B** switch.
2. Select the **CLI** tab.
3. Press **Enter** until the switch prompt appears.

### Step 2 — Enter the complete configuration

```cisco
enable
configure terminal

! Basic security and hostname
hostname Class-B
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
 ip address 128.107.30.15 255.255.255.0
 no shutdown
 exit

! Default gateway for switch management
ip default-gateway 128.107.30.1

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

Confirm that the hostname is `Class-B`, VLAN 1 has IP `128.107.30.15` with mask `255.255.255.0`, and the default gateway is `128.107.30.1`. VLAN 1 may remain down until an active switch port in VLAN 1 is connected; if so, check the connected ports and cabling.

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

### Student-1 — Left side / Class-A

| Setting | Value |
|---|---|
| IPv4 Address | `128.107.20.25` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `128.107.20.1` |
| IPv6 Address | `2001:DB8:A::25` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::1` |

### Student-2 — Left side / Class-A

| Setting | Value |
|---|---|
| IPv4 Address | `128.107.20.30` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `128.107.20.1` |
| IPv6 Address | `2001:DB8:A::30` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::1` |

### Student-3 — Right side / Class-B

| Setting | Value |
|---|---|
| IPv4 Address | `128.107.30.25` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `128.107.30.1` |
| IPv6 Address | `2001:DB8:B::25` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::1` |

### Student-4 — Right side / Class-B

| Setting | Value |
|---|---|
| IPv4 Address | `128.107.30.30` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `128.107.30.1` |
| IPv6 Address | `2001:DB8:B::30` |
| IPv6 Prefix Length | `64` |
| IPv6 Gateway | `FE80::1` |

### PC addressing overview

| PC | IPv4 Address | IPv4 Gateway | IPv6 Address | IPv6 Gateway |
|---|---|---|---|---|
| Student-1 | `128.107.20.25/24` | `128.107.20.1` | `2001:DB8:A::25/64` | `FE80::1` |
| Student-2 | `128.107.20.30/24` | `128.107.20.1` | `2001:DB8:A::30/64` | `FE80::1` |
| Student-3 | `128.107.30.25/24` | `128.107.30.1` | `2001:DB8:B::25/64` | `FE80::1` |
| Student-4 | `128.107.30.30/24` | `128.107.30.1` | `2001:DB8:B::30/64` | `FE80::1` |

---

## 5. Verify Connectivity and Score

### Step 1 — Test IPv4

On each PC, open **Desktop → Command Prompt**.

From `Student-1`, test its router gateway:

```text
ping 128.107.20.1
```

Test another PC on the same network:

```text
ping 128.107.20.30
```

Then test a PC on the other network:

```text
ping 128.107.30.25
```

### Step 2 — Test IPv6

From `Student-1`, try:

```text
ping 2001:DB8:A::1
ping 2001:DB8:B::25
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
- [ ] Router hostname is `College`.
- [ ] `G0/0` uses `128.107.20.1/24` and `2001:DB8:A::1/64`.
- [ ] `G0/0` link-local address is `FE80::1`.
- [ ] `G0/1` uses `128.107.30.1/24` and `2001:DB8:B::1/64`.
- [ ] `G0/1` link-local address is `FE80::1`.
- [ ] `ipv6 unicast-routing` is enabled.
- [ ] Class-B switch management address is `128.107.30.15/24`.
- [ ] Class-B switch default gateway is `128.107.30.1`.
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
| `G0/0` | Class-A / left | `128.107.20.1/24` | `2001:DB8:A::1/64` | `FE80::1` |
| `G0/1` | Class-B / right | `128.107.30.1/24` | `2001:DB8:B::1/64` | `FE80::1` |

### Switch management

| Setting | Value |
|---|---|
| Hostname | `Class-B` |
| VLAN 1 management IP | `128.107.30.15/24` |
| Default gateway | `128.107.30.1` |
| Enable secret | `class` |
| Console / VTY password | `cisco` |
| MOTD banner | `Authorized Access Only!` |

### Final reminders

- Use the **CLI** tab for the router and switch.
- Use **Desktop → IP Configuration** for each PC.
- Pay special attention to link-local gateways: both sides use `FE80::1`.
- Save device configurations, then confirm the actual result with **Check Results**.

