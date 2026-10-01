# SETB_CCNA1_Mid-1.pka — Step-by-Step Guide

## 1. Cable Types na Gagamitin

> ⚠️ **Important:** Huwag gamitin ang **Automatically Choose Connection Type** (kidlat ⚡). Piliin ang specific cable ayon sa Cabling Table.

---

### 1.1 Console Connection

**Cable:** 🔵 **Console Cable** (Asul / Light Blue)

| Mula sa | Port | Papunta sa | Port |
|---|---|---|---|
| PC0 | RS 232 | SW-CCS-01 | Console |
| PC2 | RS 232 | SW-CCS-02 | Console |
| PC4 | RS 232 | SW-CCS-03 | Console |

#### Procedure

1. Click **Connections ⚡**.
2. Piliin ang **Console** cable.
3. Click **PC0** → **RS 232**.
4. Click **SW-CCS-01** → **Console**.
5. Ulitin para sa **PC2 → SW-CCS-02** at **PC4 → SW-CCS-03**.

---

### 1.2 Switch-to-Switch Connection

**Cable:** ⚫ **Copper Cross-Over Cable** (Itim / Dashed)

| Mula sa | Port | Papunta sa | Port |
|---|---|---|---|
| SW-CCS-01 | FastEthernet0/1 | SW-CCS-02 | FastEthernet0/1 |
| SW-CCS-02 | FastEthernet0/2 | SW-CCS-03 | FastEthernet0/1 |

#### Procedure

1. Click **Connections ⚡**.
2. Piliin ang **Copper Cross-Over**.
3. Click **SW-CCS-01** → **FastEthernet0/1**.
4. Click **SW-CCS-02** → **FastEthernet0/1**.
5. Para sa second connection:
   - Click **SW-CCS-02** → **FastEthernet0/2**.
   - Click **SW-CCS-03** → **FastEthernet0/1**.

---

### 1.3 PC-to-Switch Data Connection

**Cable:** ⚫ **Copper Straight-Through Cable** (Itim / Solid)

| Mula sa | Port | Papunta sa | Port |
|---|---|---|---|
| PC0 | FastEthernet | SW-CCS-01 | FastEthernet0/10 |
| PC1 | FastEthernet | SW-CCS-01 | FastEthernet0/11 |
| PC2 | FastEthernet | SW-CCS-02 | FastEthernet0/12 |
| PC3 | FastEthernet | SW-CCS-02 | FastEthernet0/13 |
| PC4 | FastEthernet | SW-CCS-03 | FastEthernet0/14 |
| PC5 | FastEthernet | SW-CCS-03 | FastEthernet0/15 |

#### Procedure

1. Click **Connections ⚡**.
2. Piliin ang **Copper Straight-Through**.
3. Click **PC0** → **FastEthernet**.
4. Click **SW-CCS-01** → **FastEthernet0/10**.
5. Ulitin ang parehong procedure ayon sa table sa itaas.

---

## 2. Cable Summary

| Connection | Specific Cable | Kulay / Itsura |
|---|---|---|
| PC → Switch (Console) | **Console Cable** | 🔵 Asul / Light Blue |
| Switch → Switch | **Copper Cross-Over** | ⚫ Itim / Dashed |
| PC → Switch (Data) | **Copper Straight-Through** | ⚫ Itim / Solid |

### Packet Tracer Reminders

1. ❌ Huwag piliin ang **Automatically Choose Connection Type**.
2. ✅ Piliin ang exact cable:
   - **Console**
   - **Copper Cross-Over**
   - **Copper Straight-Through**
3. ✅ Piliin ang tamang port ayon sa table.
4. 🟢 Ang green link indicator ay karaniwang nangangahulugang active ang link.
5. 🔴 Kung red/down ang link, i-check ang cable type, port, interface status, at device connection.

---

# 3. Console Terminal Access

Kung walang prompt sa Terminal:

1. Siguraduhing nakakabit ang **Console Cable**.
2. PC0: **RS 232** → SW-CCS-01: **Console**.
3. PC2: **RS 232** → SW-CCS-02: **Console**.
4. PC4: **RS 232** → SW-CCS-03: **Console**.
5. Sa PC, pumunta sa **Desktop → Terminal**.
6. Dapat lumabas ang switch prompt:

```text
Switch>
```

---

# 4. Configure SW-CCS-01

**Gawin sa Terminal ng PC0.**

I-type ang commands **isa-isa** at pindutin ang **Enter** pagkatapos ng bawat command.

```cisco
enable
configure terminal
hostname SW-CCS-01

line console 0
password SetBCcs01
login
exit

enable secret class01SetB

line vty 0 15
password vtypass01SetB
login
exit

service password-encryption

banner motd # SET B Midterm Exam #

interface vlan 1
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

Kapag lumabas ang:

```text
Destination filename [startup-config]?
```

Pindutin ang **Enter**.

---

# 5. Configure SW-CCS-02

**Gawin sa Terminal ng PC2.**

```cisco
enable
configure terminal
hostname SW-CCS-02

line console 0
password SetBCcs02
login
exit

enable secret class02SetB

line vty 0 15
password vtypass02SetB
login
exit

service password-encryption

banner motd # SET B Welcome #

interface vlan 1
ip address 192.168.3.2 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

Kapag lumabas ang:

```text
Destination filename [startup-config]?
```

Pindutin ang **Enter**.

---

# 6. Configure SW-CCS-03

**Gawin sa Terminal ng PC4.**

```cisco
enable
configure terminal
hostname SW-CCS-03

line console 0
password SetBCcs03
login
exit

enable secret class03SetB

line vty 0 15
password vtypass03SetB
login
exit

service password-encryption

banner motd # SET B Administrator #

interface vlan 1
ip address 192.168.3.3 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

Kapag lumabas ang:

```text
Destination filename [startup-config]?
```

Pindutin ang **Enter**.

---

# 7. Command Explanation

| Command | Function |
|---|---|
| `enable` | Pumapasok sa privileged EXEC mode (`Switch#`). |
| `configure terminal` | Pumapasok sa global configuration mode. |
| `hostname SW-CCS-01` | Binabago ang hostname ng switch. |
| `line console 0` | Kino-configure ang console line. |
| `password SetBCcs01` | Nagtatakda ng console password. |
| `login` | Pinapagana ang password authentication sa console. |
| `exit` | Bumabalik sa previous configuration mode. |
| `enable secret class01SetB` | Nagtatakda ng privileged EXEC password. |
| `line vty 0 15` | Kino-configure ang VTY lines para sa remote access. |
| `password vtypass01SetB` | Nagtatakda ng VTY password. |
| `service password-encryption` | Ini-encrypt ang configured plain-text passwords. |
| `banner motd #...#` | Nagtatakda ng Message of the Day banner. |
| `interface vlan 1` | Pinipili ang VLAN 1 management interface. |
| `ip address ...` | Nagtatakda ng IP address at subnet mask. |
| `no shutdown` | Ina-activate ang interface. |
| `end` | Bumabalik sa privileged EXEC mode. |
| `copy running-config startup-config` | Sine-save ang running configuration sa startup configuration. |

---

# 8. Important Typing Reminders

1. **Case-sensitive ang passwords.**
   - `SetBCS01` ay iba sa `setbcs01`.
   - `class01SetB` ay iba sa `Class01SetB`.

2. Sa `banner motd`, ang `#` ay delimiter:

```cisco
banner motd # SET B Midterm Exam #
```

3. Kung kailangan mong bumalik agad sa privileged EXEC mode:

```text
Ctrl+Z
```

4. Pagkatapos ng configuration, siguraduhing na-save ito:

```cisco
copy running-config startup-config
```

---

# 9. Verification / Testing

## Test 1 — Ping Test

Sa **PC0 → Desktop → Command Prompt**:

```text
ping 192.168.3.1
ping 192.168.3.2
ping 192.168.3.3
```

Ang `192.168.3.1` ay SW-CCS-01, `192.168.3.2` ay SW-CCS-02, at `192.168.3.3` ay SW-CCS-03.

> ⚠️ **Tandaan:** Para maging successful ang ping, kailangan ding tama ang PC IP configuration at active ang network path.

---

## Test 2 — Banner Test

Sa switch console:

1. Mag-logout o magsara ng Terminal session.
2. Buksan muli ang Terminal.
3. Dapat makita ang configured MOTD banner.

Halimbawa sa SW-CCS-01:

```text
SET B Midterm Exam
```

---

## Test 3 — Enable Password Test

Sa switch console:

```cisco
exit
enable
```

**SW-CCS-01**
```text
class01SetB
```

**SW-CCS-02**
```text
class02SetB
```

**SW-CCS-03**
```text
class03SetB
```

---

## Test 4 — Check Running Configuration

Sa privileged EXEC mode:

```cisco
show running-config
```

I-check kung naroon ang:

- [ ] Correct hostname
- [ ] Console password
- [ ] Enable secret
- [ ] VTY password
- [ ] `service password-encryption`
- [ ] MOTD banner
- [ ] VLAN 1 IP address
- [ ] `no shutdown`

---

# 10. Final Configuration Checklist

## Cabling

- [ ] PC0 RS 232 → SW-CCS-01 Console — **Console Cable**
- [ ] PC2 RS 232 → SW-CCS-02 Console — **Console Cable**
- [ ] PC4 RS 232 → SW-CCS-03 Console — **Console Cable**
- [ ] SW-CCS-01 Fa0/1 → SW-CCS-02 Fa0/1 — **Copper Cross-Over**
- [ ] SW-CCS-02 Fa0/2 → SW-CCS-03 Fa0/1 — **Copper Cross-Over**
- [ ] PC0 Fa → SW-CCS-01 Fa0/10 — **Copper Straight-Through**
- [ ] PC1 Fa → SW-CCS-01 Fa0/11 — **Copper Straight-Through**
- [ ] PC2 Fa → SW-CCS-02 Fa0/12 — **Copper Straight-Through**
- [ ] PC3 Fa → SW-CCS-02 Fa0/13 — **Copper Straight-Through**
- [ ] PC4 Fa → SW-CCS-03 Fa0/14 — **Copper Straight-Through**
- [ ] PC5 Fa → SW-CCS-03 Fa0/15 — **Copper Straight-Through**

## Switch Configuration

- [ ] SW-CCS-01 hostname and IP configured
- [ ] SW-CCS-02 hostname and IP configured
- [ ] SW-CCS-03 hostname and IP configured
- [ ] Console passwords configured
- [ ] Enable secrets configured
- [ ] VTY passwords configured
- [ ] Password encryption enabled
- [ ] MOTD banners configured
- [ ] VLAN 1 interfaces configured
- [ ] Configuration saved with `copy running-config startup-config`

---

# 11. Final IP Address Reference

| Device | VLAN 1 IP | Subnet Mask |
|---|---|---|
| SW-CCS-01 | `192.168.3.1` | `255.255.255.0` |
| SW-CCS-02 | `192.168.3.2` | `255.255.255.0` |
| SW-CCS-03 | `192.168.3.3` | `255.255.255.0` |

---

# 12. Quick Command Reference

## SW-CCS-01

```cisco
enable
configure terminal
hostname SW-CCS-01

line console 0
password SetBCcs01
login
exit

enable secret class01SetB

line vty 0 15
password vtypass01SetB
login
exit

service password-encryption
banner motd # SET B Midterm Exam #

interface vlan 1
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

## SW-CCS-02

```cisco
enable
configure terminal
hostname SW-CCS-02

line console 0
password SetBCcs02
login
exit

enable secret class02SetB

line vty 0 15
password vtypass02SetB
login
exit

service password-encryption
banner motd # SET B Welcome #

interface vlan 1
ip address 192.168.3.2 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

## SW-CCS-03

```cisco
enable
configure terminal
hostname SW-CCS-03

line console 0
password SetBCcs03
login
exit

enable secret class03SetB

line vty 0 15
password vtypass03SetB
login
exit

service password-encryption
banner motd # SET B Administrator #

interface vlan 1
ip address 192.168.3.3 255.255.255.0
no shutdown
exit

end
copy running-config startup-config
```

---

## ⚠️ Important Note

This guide organizes the cabling and commands provided for `SETB_CCNA1_Mid-1.pka`.

If the actual Packet Tracer activity contains a different Cabling Table, addressing table, or required configuration, follow the values inside the `.pka` activity itself.
