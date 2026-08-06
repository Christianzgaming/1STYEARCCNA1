# CCNA 1 Packet Tracer Guide

> **Module 2 - Basic Switch Configuration**
>
> Ang guide na ito ay naglalaman ng step-by-step commands at configurations para sa mga Packet Tracer activities. Sundin lamang ang bawat section ayon sa activity.

---

# 2.5.5 Packet Tracer - Configure Initial Switch Settings

## Objective

I-configure ang initial settings ng dalawang switches (**S1** at **S2**) gamit ang CLI.

---

## S1 Configuration

```text
enable
configure terminal
hostname S1
line console 0
password letmein
login
exit
enable password c1$c0
enable secret itsasecret
service password-encryption
banner motd "This is a secure system. Authorized Access Only!"
end
show running-config
copy running-config startup-config
```

---

## S2 Configuration

```text
enable
configure terminal
hostname S2
line console 0
password letmein
login
exit
enable password c1$c0
enable secret itsasecret
service password-encryption
banner motd "This is a secure system. Authorized Access Only!"
end
show running-config
copy running-config startup-config
```

---

## Verification

Verify the configuration using:

```text
show running-config
```

Save the configuration:

```text
copy running-config startup-config
```

---

# 2.7.6 Packet Tracer - Implement Basic Connectivity

## Objective

I-configure ang dalawang switches at dalawang PCs upang magkaroon ng basic network connectivity.

---

# S1 Configuration

```text
enable
configure terminal

hostname S1

line console 0
password cisco
login
exit

enable secret class

banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#

interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
exit

end

show ip interface brief

show running-config

copy running-config startup-config
```

### Save Configuration

Kapag lumabas ang prompt:

```text
Destination filename [startup-config]?
```

Pindutin lamang ang:

```text
Enter
```

---

# S2 Configuration

```text
enable

configure terminal

hostname S2

line console 0
password cisco
login
exit

enable secret class

banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#

interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
exit

end

show ip interface brief

show running-config

copy running-config startup-config
```

### Save Configuration

Kapag lumabas ang prompt:

```text
Destination filename [startup-config]?
```

Pindutin lamang ang:

```text
Enter
```

---

## PC Configuration

### PC1

| Setting | Value |
|---------|-------|
| **IP Address** | `192.168.1.1` |
| **Subnet Mask** | `255.255.255.0` |

---

### PC2

| Setting | Value |
|---------|-------|
| **IP Address** | `192.168.1.2` |
| **Subnet Mask** | `255.255.255.0` |

---

## Verification Commands

Check VLAN interface:

```text
show ip interface brief
```

Check running configuration:

```text
show running-config
```

Save configuration:

```text
copy running-config startup-config
```

---

# 2.9.1 Packet Tracer - Basic Switch and End Device Configuration

## Objective

I-configure ang dalawang access switches at dalawang end devices upang magkaroon ng basic network connectivity.

---

# Step 1 - Configure ASW-1

### Connect to ASW-1 using the Console Cable

```bash
enable
configure terminal
hostname ASW-1
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.10 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

# Step 2 - Configure ASW-2

### Connect to ASW-2 using the Console Cable

```bash
enable
configure terminal
hostname ASW-2
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.15 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

# Step 3 - Configure the PCs

## User-01

| Setting | Value |
|---------|-------|
| **IP Address** | `128.107.20.25` |
| **Subnet Mask** | `255.255.255.0` |
| **Default Gateway** | `128.107.20.1` |

---

## User-02

| Setting | Value |
|---------|-------|
| **IP Address** | `128.107.20.30` |
| **Subnet Mask** | `255.255.255.0` |
| **Default Gateway** | `128.107.20.1` |

---

# Step 4 - Verify Connectivity

From **User-01**, open the **Command Prompt** and enter:

```bash
ping 128.107.20.30
```

### Expected Result

The ping replies should be **successful**.

---

# Step 5 - Check Results

1. Click **Check Results** in Packet Tracer.
2. Verify that all requirements are completed.
3. Make sure the score reaches **100%** before submitting the activity.

---

## Verification Commands

### Display Interface Status

```text
show ip interface brief
```

### Display Running Configuration

```text
show running-config
```

### Save Configuration

```text
copy running-config startup-config
```

---


# 2.7.6 Packet Tracer - Implement Basic Connectivity

## Overview

Sa activity na ito, iko-configure mo ang dalawang Cisco switches (**S1** at **S2**) at dalawang PCs upang magkaroon ng **basic network connectivity**. Kasama rito ang pagse-set ng hostname, console password, enable secret, banner, management IP address, at pag-save ng configuration.

---

## Network Topology

| Device | Management IP | Subnet Mask |
|---------|---------------|-------------|
| **S1** | `192.168.1.253` | `255.255.255.0` |
| **S2** | `192.168.1.254` | `255.255.255.0` |
| **PC1** | `192.168.1.1` | `255.255.255.0` |
| **PC2** | `192.168.1.2` | `255.255.255.0` |

---

# Part 1 - Configure Switch S1

## Step 1 - Enter Privileged EXEC Mode

```text
enable
```

---

## Step 2 - Enter Global Configuration Mode

```text
configure terminal
```

---

## Step 3 - Set the Hostname

```text
hostname S1
```

---

## Step 4 - Configure the Console Password

```text
line console 0
password cisco
login
exit
```

---

## Step 5 - Configure the Enable Secret Password

```text
enable secret class
```

---

## Step 6 - Configure the MOTD Banner

```text
banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#
```

---

## Step 7 - Configure the VLAN 1 Management Interface

```text
interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
exit
```

---

## Step 8 - Exit Configuration Mode

```text
end
```

---

## Step 9 - Verify the Interface Status

```text
show ip interface brief
```

---

## Step 10 - Verify the Running Configuration

```text
show running-config
```

---

## Step 11 - Save the Configuration

```text
copy running-config startup-config
```

Kapag lumabas ang prompt:

```text
Destination filename [startup-config]?
```

Pindutin lamang ang:

```text
Enter
```

---

# Complete CLI Commands - S1

```text
enable

configure terminal

hostname S1

line console 0
password cisco
login
exit

enable secret class

banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#

interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
exit

end

show ip interface brief

show running-config

copy running-config startup-config
```

---

# Part 2 - Configure Switch S2

## Step 1 - Enter Privileged EXEC Mode

```text
enable
```

---

## Step 2 - Enter Global Configuration Mode

```text
configure terminal
```

---

## Step 3 - Set the Hostname

```text
hostname S2
```

---

## Step 4 - Configure the Console Password

```text
line console 0
password cisco
login
exit
```

---

## Step 5 - Configure the Enable Secret Password

```text
enable secret class
```

---

## Step 6 - Configure the MOTD Banner

```text
banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#
```

---

## Step 7 - Configure the VLAN 1 Management Interface

```text
interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
exit
```

---

## Step 8 - Exit Configuration Mode

```text
end
```

---

## Step 9 - Verify the Interface Status

```text
show ip interface brief
```

---

## Step 10 - Verify the Running Configuration

```text
show running-config
```

---

## Step 11 - Save the Configuration

```text
copy running-config startup-config
```

Kapag lumabas ang prompt:

```text
Destination filename [startup-config]?
```

Pindutin lamang ang:

```text
Enter
```

---

# Complete CLI Commands - S2

```text
enable

configure terminal

hostname S2

line console 0
password cisco
login
exit

enable secret class

banner motd #Authorized access only. Violators will be prosecuted to the full extent of the law.#

interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
exit

end

show ip interface brief

show running-config

copy running-config startup-config
```

---

# Part 3 - Configure the PCs

## PC1 Configuration

| Setting | Value |
|---------|-------|
| **IP Address** | `192.168.1.1` |
| **Subnet Mask** | `255.255.255.0` |

---

## PC2 Configuration

| Setting | Value |
|---------|-------|
| **IP Address** | `192.168.1.2` |
| **Subnet Mask** | `255.255.255.0` |

---

# Verification Commands

## Display Interface Status

```text
show ip interface brief
```

---

## Display the Current Configuration

```text
show running-config
```

---

## Save the Configuration

```text
copy running-config startup-config
```

---

# Expected Results

After completing all configurations:

- ✅ **S1** hostname is configured correctly.
- ✅ **S2** hostname is configured correctly.
- ✅ Console password is set to **cisco**.
- ✅ Enable secret password is **class**.
- ✅ MOTD banner is displayed before login.
- ✅ VLAN 1 on **S1** has IP address **192.168.1.253/24**.
- ✅ VLAN 1 on **S2** has IP address **192.168.1.254/24**.
- ✅ PC1 is configured with **192.168.1.1/24**.
- ✅ PC2 is configured with **192.168.1.2/24**.
- ✅ Running configuration is saved to **startup-config**.

---



# 2.9.1 Packet Tracer - Basic Switch and End Device Configuration

## Overview

Sa activity na ito, iko-configure ang dalawang access switches (**ASW-1** at **ASW-2**) at dalawang end devices (**User-01** at **User-02**). Pagkatapos ng configuration, ibe-verify ang connectivity gamit ang `ping` command.

---

## Network Addressing

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---------|-----------|------------|-------------|-----------------|
| **ASW-1** | VLAN 1 | `128.107.20.10` | `255.255.255.0` | `128.107.20.1` |
| **ASW-2** | VLAN 1 | `128.107.20.15` | `255.255.255.0` | `128.107.20.1` |
| **User-01** | NIC | `128.107.20.25` | `255.255.255.0` | `128.107.20.1` |
| **User-02** | NIC | `128.107.20.30` | `255.255.255.0` | `128.107.20.1` |

---

# Part 1 - Configure ASW-1

## Step 1 - Connect to ASW-1

1. Gumamit ng **Console Cable**.
2. Ikonekta ang **PC** papunta sa **Console Port** ng **ASW-1**.
3. Buksan ang **Terminal**.

---

## Step 2 - Configure the Switch

I-type ang mga sumusunod na commands:

```text
enable
configure terminal
hostname ASW-1
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.10 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

## Explanation

| Command | Description |
|---------|-------------|
| `hostname ASW-1` | Sets the switch hostname. |
| `enable secret C4aJa` | Configures the encrypted privileged EXEC password. |
| `line console 0` | Configures console access. |
| `line vty 0 4` | Configures Telnet/remote access. |
| `service password-encryption` | Encrypts plain-text passwords. |
| `banner motd` | Displays a warning banner before login. |
| `interface vlan 1` | Accesses the management interface. |
| `ip default-gateway` | Sets the default gateway for switch management. |

---

# Part 2 - Configure ASW-2

## Step 1 - Connect to ASW-2

1. Gumamit ng **Console Cable**.
2. Ikonekta ang PC sa **Console Port** ng **ASW-2**.
3. Buksan ang **Terminal**.

---

## Step 2 - Configure the Switch

I-type ang mga sumusunod na commands:

```text
enable
configure terminal
hostname ASW-2
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.15 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

# Part 3 - Configure the PCs

## User-01

Configure the following values:

| Setting | Value |
|---------|-------|
| **IP Address** | `128.107.20.25` |
| **Subnet Mask** | `255.255.255.0` |
| **Default Gateway** | `128.107.20.1` |

---

## User-02

Configure the following values:

| Setting | Value |
|---------|-------|
| **IP Address** | `128.107.20.30` |
| **Subnet Mask** | `255.255.255.0` |
| **Default Gateway** | `128.107.20.1` |

---

# Part 4 - Verify Connectivity

Mula sa **User-01**, buksan ang **Command Prompt** at i-type ang:

```text
ping 128.107.20.30
```

### Expected Result

```text
Reply from 128.107.20.30:
bytes=32 time<1ms TTL=128
```

Kung successful ang replies, tama ang configuration ng network.

---

# Part 5 - Save the Configuration

Kung hindi mo pa ito nagagawa, i-save ang configuration ng bawat switch.

```text
copy running-config startup-config
```

Kapag lumabas ang prompt:

```text
Destination filename [startup-config]?
```

Pindutin lamang ang:

```text
Enter
```

---

# Verification Commands

## Check the Interface Status

```text
show ip interface brief
```

---

## Display the Current Configuration

```text
show running-config
```

---

## Save the Configuration

```text
copy running-config startup-config
```

---

# Complete CLI Commands - ASW-1

```text
enable
configure terminal
hostname ASW-1
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.10 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

# Complete CLI Commands - ASW-2

```text
enable
configure terminal
hostname ASW-2
enable secret C4aJa
line console 0
password R4Xe3
login
exit
line vty 0 4
password R4Xe3
login
exit
service password-encryption
banner motd #Unauthorized Access is Prohibited#
interface vlan 1
ip address 128.107.20.15 255.255.255.0
no shutdown
exit
ip default-gateway 128.107.20.1
end
copy running-config startup-config
```

---

# Activity Checklist

- ✅ Configure **ASW-1**
- ✅ Configure **ASW-2**
- ✅ Configure **User-01**
- ✅ Configure **User-02**
- ✅ Verify connectivity using `ping`
- ✅ Save the running configuration
- ✅ Click **Check Results** and verify that the activity is **100% complete**



# 4.6.5 Packet Tracer - Connect a Wired and Wireless LAN

## Overview

Sa activity na ito, gagawa tayo ng wired at wireless network connection gamit ang iba't ibang uri ng cables at devices sa Cisco Packet Tracer.

Kasama sa activity ang:

- Pagkonekta ng Cloud sa Router0
- Pagkonekta ng Cable Modem
- Pagkonekta ng Routers
- Pagkonekta ng Switches
- Pagkonekta ng Wireless Router
- Pag-test ng network connectivity
- Pagsuri ng physical topology

---

# Part 1 - Connect to the Cloud

---

# Step 1: Connect the Cloud to Router0

## Cable Used

```
Copper Straight-Through
```

## Connection

| Device | Port |
|---|---|
| Router0 | F0/0 |
| Cloud | Eth6 |

## Steps

1. Sa ibaba ng Packet Tracer, i-click ang **Connections** (orange lightning icon).
2. Piliin ang **Copper Straight-Through** cable.
3. I-click ang **Router0**.
4. Piliin ang **F0/0** port.
5. I-click ang **Cloud**.
6. Piliin ang **Eth6** port.
7. Hintaying maging **green** ang link lights.

---

# Step 2: Connect the Cloud to Cable Modem

## Cable Used

```
Coaxial Cable
```

## Connection

| Device | Port |
|---|---|
| Cloud | Coax7 |
| Cable Modem | Port0 |

## Steps

1. Piliin ang **Coaxial** cable.
2. I-click ang **Cloud**.
3. Piliin ang **Coax7**.
4. I-click ang **Cable Modem**.
5. Piliin ang **Port0**.
6. Hintaying maging **green** ang connection.

---

# Part 2 - Connect Router0

---

# Step 1: Connect Router0 to Router1

## Cable Used

```
Serial DCE
```

## Connection

| Device | Port |
|---|---|
| Router0 | Serial0/0/0 |
| Router1 | Serial0/0 |

## Steps

1. Piliin ang **Serial DCE** cable.
2. I-click ang **Router0**.
3. Piliin ang **Serial0/0/0**.
4. I-click ang **Router1**.
5. Piliin ang **Serial0/0**.
6. Hintaying maging green ang link.

---

# Step 2: Connect Router0 to netacad.pka

## Cable Used

```
Copper Cross-Over
```

## Connection

| Device | Port |
|---|---|
| Router0 | F0/1 |
| netacad.pka | F0 |

## Steps

1. Piliin ang **Copper Cross-Over** cable.
2. I-click ang **Router0**.
3. Piliin ang **F0/1**.
4. I-click ang **netacad.pka**.
5. Piliin ang **F0**.
6. Hintaying maging green ang connection.

---

# Step 3: Connect Router0 to Configuration Terminal

## Cable Used

```
Console Cable
```

## Connection

| Device | Port |
|---|---|
| Router0 | Console |
| Configuration Terminal | RS232 |

## Steps

1. Piliin ang **Console** cable.
2. I-click ang **Router0**.
3. Piliin ang **Console** port.
4. I-click ang **Configuration Terminal**.
5. Piliin ang **RS232** port.

> Note:
>
> Normal lamang na **black** ang cable dahil console connection ito at hindi network connection.

---

# Part 3 - Connect Remaining Devices

---

# Step 1: Connect Router1 to Switch

## Cable Used

```
Copper Straight-Through
```

> Note:
>
> Depende sa Packet Tracer version, maaaring gumana rin ang Multi Fiber connection.

## Connection

| Device | Port |
|---|---|
| Router1 | F1/0 |
| Switch | F0/1 |

---

# Step 2: Connect Cable Modem to Wireless Router

## Cable Used

```
Copper Straight-Through
```

## Connection

| Device | Port |
|---|---|
| Cable Modem | Port1 |
| WirelessRouter | Internet |

---

# Step 3: Connect Wireless Router to Family PC

## Cable Used

```
Copper Straight-Through
```

## Connection

| Device | Port |
|---|---|
| WirelessRouter | Ethernet 1 |
| Family PC | F0 |

---

# Part 4 - Verify Connections

---

# Step 1: Test Family PC Connection to netacad.pka

## Steps

1. I-click ang **Family PC**.
2. Pumunta sa **Desktop** tab.
3. Buksan ang **Command Prompt**.
4. I-type:

```text
ping netacad.pka
```

## Expected Result

Dapat magkaroon ng:

```
Successful replies
```

---

## Web Browser Test

1. Buksan ang **Web Browser**.
2. Ilagay ang address:

```text
http://netacad.pka
```

3. I-click ang **Go**.

## Expected Result

Dapat lumabas ang webpage.

---

# Step 2: Ping the Switch from Home PC

## Steps

1. I-click ang **Home PC**.
2. Pumunta sa **Desktop**.
3. Buksan ang **Command Prompt**.
4. I-type:

```text
ping 172.16.0.2
```

## Expected Result

Dapat magkaroon ng successful replies.

---

# Step 3: Access Router0 from Configuration Terminal

## Steps

1. I-click ang **Configuration Terminal**.
2. Pumunta sa **Desktop** tab.
3. Piliin ang **Terminal**.
4. I-click ang **OK** gamit ang default settings.
5. Pindutin ang **Enter** hanggang lumabas ang:

```text
Router>
```

6. I-type:

```text
enable
show ip interface brief
```

## Expected Result

Ang connected interfaces ay dapat:

```
up/up
```

---

# Part 5 - Examine the Physical Topology

---

# Step 1: Examine the Cloud

## Steps

1. Pindutin:

```
Shift + P
```

at

```
Shift + L
```

2. Lumipat sa **Physical Workspace**.
3. I-click ang **Home City**.
4. I-click ang **Cloud**.

---

## Question

### Ilang wires ang nakakonekta sa switch sa blue rack?

### Answer:

```
2 wires
```

Connected wires:

- Eth6
- Coax7

---

# Step 2: Examine the Primary Network

## Steps

1. I-click ang **Primary Network**.
2. I-hover ang mouse sa mga cables.

---

## Question

### Ano ang nasa table sa kanan ng blue rack?

### Answer:

```
Configuration Terminal
(RS232 Terminal)
```

---

# Step 3: Examine the Secondary Network

## Steps

1. I-click ang **Secondary Network**.
2. I-hover ang mouse sa orange cables.

---

## Question

### Bakit may dalawang orange cables na nakakonekta sa bawat device?

### Answer:

Ang orange cables ay **fiber optic cables**.

Dalawa ang ginagamit dahil:

- Isang cable para sa **Transmit (TX)**
- Isang cable para sa **Receive (RX)**

Ginagamit ito para sa:

```
Full-Duplex Communication
```

---

# Step 4: Examine the Home Network

## Steps

1. I-click ang **Home Network**.

---

## Question

### Bakit walang rack para sa equipment?

### Answer:

Dahil ito ay isang **home network**.

Ang mga devices ay karaniwang inilalagay sa:

- Mesa
- Desk
- Sahig

Hindi tulad ng enterprise network na gumagamit ng server racks.

---

# Activity Complete ✅

## Summary

Natapos ang mga sumusunod:

✅ Cloud connections  
✅ Router connections  
✅ Switch connections  
✅ Wireless router setup  
✅ PC connectivity testing  
✅ Physical topology examination  




# 4.7.1 Packet Tracer - Connect the Physical Layer

## Overview

Sa activity na ito, pag-aaralan at ikokonekta ang iba't ibang physical components ng isang network gamit ang Cisco Packet Tracer.

Kasama rito ang:

- Pagkilala sa physical characteristics ng networking devices
- Pagkilala sa management ports at interfaces
- Pag-install ng expansion modules
- Pagpili ng tamang cable types
- Pagkonekta ng wired at wireless devices
- Pag-verify ng network connectivity

---

# Part 1 - Identify Physical Characteristics of Internetworking Devices

---

# Step 1: Identify the Management Ports of a Cisco Router

## A. Open the East Router

1. I-click ang **East Router**.
2. Siguraduhin na nasa **Physical tab**.

---

## B. Identify the Management Ports

### Question:

**Which management ports are available?**

### Answer:

```
Console and AUX (Auxiliary) ports
```

---

## C. Identify LAN and WAN Interfaces

### Question:

**Which LAN and WAN interfaces are available on the East router and how many are there?**

### Answer:

### LAN Interfaces:

```
GigabitEthernet0/0
GigabitEthernet0/1
```

Total:

```
2 LAN Interfaces
```

---

### WAN Interfaces:

```
Serial0/0/0
Serial0/0/1
```

Total:

```
2 WAN Interfaces
```

---

## D. Check Physical Interfaces Using CLI

1. Pumunta sa **CLI tab**.
2. Pindutin ang **Enter**.
3. I-type:

```text
East> enable

East# show ip interface brief
```

---

### Question:

**How many physical interfaces are listed?**

### Answer:

```
6 physical interfaces
```

Interfaces:

- GigabitEthernet0/0
- GigabitEthernet0/1
- Serial0/0/0
- Serial0/0/1
- FastEthernet0/1/0
- FastEthernet0/1/1
- FastEthernet0/1/2
- FastEthernet0/1/3

---

## E. Check Interface Bandwidth

### GigabitEthernet Interface

Command:

```text
East# show interface gigabitethernet 0/0
```

### Question:

**What is the default bandwidth of this interface?**

### Answer:

```
100000 Kbps
(100 Mbps)
```

---

### Serial Interface

Command:

```text
East# show interface serial 0/0/0
```

### Question:

**What is the default bandwidth of this interface?**

### Answer:

```
1544 Kbps
(1.544 Mbps)
```

---

# Step 2 - Identify Module Expansion Slots

## East Router

### Question:

**How many expansion slots are available for adding modules?**

### Answer:

```
2 expansion slots
```

---

## Switch2

### Question:

**How many expansion slots are available?**

### Answer:

```
5 expansion slots
```

---

# Part 2 - Select Correct Modules for Connectivity

---

# Step 1: Determine Which Modules Provide Required Connectivity

---

## A. East Router Module

### Question:

**You need to connect PCs 1, 2, and 3 to the East router, but you do not have enough money to buy a new switch. Which module can be used?**

### Answer:

```
HWIC-4ESW
```

Description:

```
4-port Ethernet Switch Module
```

---

### Question:

**How many hosts can be connected using this module?**

### Answer:

```
4 hosts
```

---

## B. Switch2 Module

### Question:

**Which module can be inserted to provide Gigabit optical connection to Switch3?**

### Answer:

```
GLC-LH-SMD
```

Description:

```
Gigabit Ethernet SFP Module
(for fiber connection)
```

---

# Step 2 - Add Correct Modules and Power Up Devices

---

# A. Install HWIC-4ESW on East Router

Steps:

1. I-click ang **East Router**.
2. Pumunta sa **Physical tab**.
3. Hanapin ang **HWIC-4ESW** module.
4. I-off muna ang power ng router.
5. I-drag ang module papunta sa empty slot.
6. I-on muli ang power.

---

> Note:
>
> Kung maling module ang nailagay:
>
> I-drag ito pababa sa picture nito sa bottom-right corner para alisin.

---

# B. Install GLC-LH-SMD on Switch2

Steps:

1. I-click ang **Switch2**.
2. Pumunta sa **Physical tab**.
3. I-off ang power.
4. Hanapin ang **GLC-LH-SMD** module.
5. I-drag ito sa empty slot sa pinakakanan.
6. I-on muli ang power.

---

# C. Verify Module Location

Command:

```text
show ip interface brief
```

### Question:

**Saang slot nailagay ang module?**

### Answer:

```
GigabitEthernet5/1
```

---

# Part 3 - Connect Devices

## Connection Table

| Device 1 | Interface 1 | Cable Type | Device 2 | Interface 2 |
|---|---|---|---|---|
| East | GigabitEthernet0/0 | Copper Straight-Through | Switch1 | GigabitEthernet0/1 |
| East | GigabitEthernet0/1 | Copper Straight-Through | Switch4 | GigabitEthernet0/1 |
| East | FastEthernet0/1/0 | Copper Straight-Through | PC1 | FastEthernet0 |
| East | FastEthernet0/1/1 | Copper Straight-Through | PC2 | FastEthernet0 |
| East | FastEthernet0/1/2 | Copper Straight-Through | PC3 | FastEthernet0 |
| Switch1 | FastEthernet0/1 | Copper Straight-Through | PC4 | FastEthernet0 |
| Switch1 | FastEthernet0/2 | Copper Straight-Through | PC5 | FastEthernet0 |
| Switch1 | FastEthernet0/3 | Copper Straight-Through | PC6 | FastEthernet0 |
| Switch4 | GigabitEthernet0/2 | Copper Cross-Over | Switch3 | GigabitEthernet3/1 |
| Switch3 | GigabitEthernet5/1 | Fiber | Switch2 | GigabitEthernet5/1 |
| Switch2 | FastEthernet0/1 | Copper Straight-Through | PC7 | FastEthernet0 |
| Switch2 | FastEthernet1/1 | Copper Straight-Through | PC8 | FastEthernet0 |
| Switch2 | FastEthernet2/1 | Copper Straight-Through | PC9 | FastEthernet0 |
| Switch2 | Gigabit3/1 | Copper Straight-Through | AccessPoint | Port 0 |
| East | Serial0/0/0 | Serial DCE | West | Serial0/0/0 |

---

# Detailed Connection Steps

---

## 1. East ↔ Switch1

Cable:

```
Copper Straight-Through
```

Connection:

```
East GigabitEthernet0/0
        |
Switch1 GigabitEthernet0/1
```

---

## 2. East ↔ Switch4

Cable:

```
Copper Straight-Through
```

Connection:

```
East GigabitEthernet0/1
        |
Switch4 GigabitEthernet0/1
```

---

## 3. East ↔ PC1

Cable:

```
Copper Straight-Through
```

Connection:

```
East FastEthernet0/1/0
        |
PC1 FastEthernet0
```

---

## 4. East ↔ PC2

Cable:

```
Copper Straight-Through
```

Connection:

```
East FastEthernet0/1/1
        |
PC2 FastEthernet0
```

---

## 5. East ↔ PC3

Cable:

```
Copper Straight-Through
```

Connection:

```
East FastEthernet0/1/2
        |
PC3 FastEthernet0
```

---

## 6. Switch1 ↔ PC4

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch1 FastEthernet0/1
        |
PC4 FastEthernet0
```

---

## 7. Switch1 ↔ PC5

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch1 FastEthernet0/2
        |
PC5 FastEthernet0
```

---

## 8. Switch1 ↔ PC6

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch1 FastEthernet0/3
        |
PC6 FastEthernet0
```

---

## 9. Switch4 ↔ Switch3

Cable:

```
Copper Cross-Over
```

Connection:

```
Switch4 GigabitEthernet0/2
        |
Switch3 GigabitEthernet3/1
```

---

## 10. Switch3 ↔ Switch2

Cable:

```
Fiber
```

Connection:

```
Switch3 GigabitEthernet5/1
        |
Switch2 GigabitEthernet5/1
```

---

## 11. Switch2 ↔ PC7

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch2 FastEthernet0/1
        |
PC7 FastEthernet0
```

---

## 12. Switch2 ↔ PC8

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch2 FastEthernet1/1
        |
PC8 FastEthernet0
```

---

## 13. Switch2 ↔ PC9

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch2 FastEthernet2/1
        |
PC9 FastEthernet0
```

---

## 14. Switch2 ↔ Access Point

Cable:

```
Copper Straight-Through
```

Connection:

```
Switch2 Gigabit3/1
        |
AccessPoint Port 0
```

---

## 15. East ↔ West Serial Connection

Cable:

```
Serial DCE
```

Important:

1. I-click muna ang **East**.
2. Piliin ang **Serial0/0/0**.
3. Ikonekta sa **West Serial0/0/0**.

> Ang East ang DCE side.

---

# Part 4 - Check Connectivity

## Step 1: Check East Interface Status

Command:

```text
East> enable

East# show ip interface brief
```

---

## Expected Output

| Interface | IP Address | Status | Protocol |
|---|---|---|---|
| GigabitEthernet0/0 | 172.30.1.1 | up | up |
| GigabitEthernet0/1 | 172.31.1.1 | up | up |
| Serial0/0/0 | 10.10.10.1 | up | up |
| Serial0/0/1 | unassigned | down | down |
| FastEthernet0/1/0 | unassigned | up | up |
| FastEthernet0/1/1 | unassigned | up | up |
| FastEthernet0/1/2 | unassigned | up | up |
| FastEthernet0/1/3 | unassigned | up | down |
| VLAN1 | 172.29.1.1 | up | up |

---

# Step 2 - Connect Wireless Devices

## Configure Laptop

Steps:

1. I-click ang **Laptop**.
2. Pumunta sa **Config tab**.
3. Piliin ang **Wireless0**.
4. I-on ang **Port Status**.
5. Hintayin ang wireless connection.

---

## Verify Web Access

1. Pumunta sa **Desktop tab**.
2. Buksan ang **Web Browser**.
3. I-type:

```text
www.cisco.pka
```

Expected:

```
Cisco Packet Tracer page
```

---

## Configure TabletPC

Steps:

1. I-click ang **TabletPC**.
2. Pumunta sa **Config tab**.
3. Piliin ang **Wireless0**.
4. I-on ang Port Status.
5. Hintayin ang connection.

---

# Step 3 - Change TabletPC Access Method

## Disable Wireless

1. TabletPC → Config
2. Wireless0
3. Alisin ang check sa Port Status.

---

## Enable Cellular Connection

1. Piliin ang:

```
3G/4G Cell1
```

2. I-on ang Port Status.

---

## Verify Connection

Buksan ang browser at pumunta sa:

```text
www.cisco.pka
```

Dapat gumana gamit ang cellular connection.

> Note:
>
> Huwag sabay i-enable ang Wireless0 at 3G/4G Cell1 upang maiwasan ang connection confusion.

---

# Step 4 - Check Other PCs

Lahat ng PCs ay dapat magkaroon ng:

- Website access
- Network connectivity
- Communication sa ibang devices

---

# Activity Complete ✅

---

# Summary of Answers

| Question | Answer |
|---|---|
| Available management ports on East router | Console and AUX |
| LAN interfaces | Gig0/0 and Gig0/1 |
| WAN interfaces | Serial0/0/0 and Serial0/0/1 |
| Number of physical interfaces | 6 physical interfaces |
| Default bandwidth GigabitEthernet0/0 | 100000 Kbps (100 Mbps) |
| Default bandwidth Serial0/0/0 | 1544 Kbps (1.544 Mbps) |
| East router expansion slots | 2 slots |
| Switch2 expansion slots | 5 slots |
| Module for connecting 3 PCs to East | HWIC-4ESW |
| Number of hosts supported | 4 hosts |
| Module for Gigabit optical connection | GLC-LH-SMD |
| Switch2 module slot | GigabitEthernet5/1 |

