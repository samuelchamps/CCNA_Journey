# Day 06 - Ethernet LAN Switching

## CCNA 200-301 Journey

This lab is part of my **CCNA 200-301 study journey** using **Jeremy's IT Lab**.

Day 6 focused on **Ethernet LAN Switching**, particularly how switches learn MAC addresses, build their MAC address tables, forward Ethernet frames, and handle network traffic.

---

## Lab Objective

The objective of this lab was to understand how Ethernet switches dynamically learn MAC addresses and use their MAC address tables to forward traffic.

The lab involved:

- Examining an initially empty MAC address table
- Generating network traffic using `ping`
- Observing traffic using Packet Tracer Simulation Mode
- Understanding how switches learn source MAC addresses
- Viewing dynamically learned MAC addresses
- Identifying the switch interfaces associated with learned MAC addresses
- Clearing dynamic MAC address entries

---

## Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- Packet Tracer Simulation Mode
- ICMP / Ping
- Jeremy's IT Lab
- Git
- GitHub

---

## Network Topology

The network consisted of:

- **PC1** - 192.168.1.1
- **PC2** - 192.168.1.2
- **PC3** - 192.168.1.3
- **PC4** - 192.168.1.4
- **SW1** - Cisco 2960 Switch
- **SW2** - Cisco 2960 Switch

The network used:

```text
192.168.1.0/24
```

SW1 and SW2 were connected using their Gigabit Ethernet interfaces.

---

#  MAC Address Learning

Ethernet switches use MAC addresses to determine where Ethernet frames should be forwarded.

A switch builds its MAC address table dynamically by examining the **source MAC address** of frames received on its interfaces.

When a frame enters a switch, the switch learns:

```text
Source MAC Address → Incoming Interface
```

This information is then stored in the MAC address table.

---

#  1. Check the MAC Address Table

Before generating network traffic, I checked the MAC address table on the switch using:

```text
show mac address-table
```

Initially, there were no dynamically learned MAC addresses.

This was because the PCs had not yet generated traffic for the switches to learn from.

---

#  2. Generate Network Traffic

I generated traffic between the PCs using the `ping` command.

For example:

```text
ping 192.168.1.3
```

I also generated traffic between other PCs on the network.

The ping tests returned successful replies with:

```text
Packets: Sent = 4, Received = 4, Lost = 0
```

This confirmed that the PCs could successfully communicate across both switches.

---

# 🔍 3. Observe Traffic in Simulation Mode

I used **Packet Tracer Simulation Mode** to observe how traffic travelled through the network.

For communication between PC1 and PC3, the traffic followed the path:

```text
PC1
 ↓
SW1
 ↓
SW2
 ↓
PC3
```

The return traffic followed:

```text
PC3
 ↓
SW2
 ↓
SW1
 ↓
PC1
```

The Simulation Panel showed ICMP packets moving between the devices.

This helped me visualize how Ethernet switches forward frames through a LAN.

---

#  4. MAC Address Learning

As traffic passed through the switches, each switch examined the source MAC address of the received Ethernet frames.

The switches then dynamically added MAC addresses to their MAC address tables.

For example:

```text
Vlan    Mac Address       Type       Ports
----    -----------       --------   -----
1       0004.9afe.d870    DYNAMIC    Gig0/1
1       00d0.d3ad.9cab    DYNAMIC    Fa0/1
```

The `DYNAMIC` entry indicates that the MAC address was automatically learned by the switch.

---

#  5. How Switches Forward Frames

When a switch receives an Ethernet frame, it checks the destination MAC address against its MAC address table.

If the destination MAC address is known, the switch forwards the frame only through the interface associated with that MAC address.

If the destination MAC address is unknown, the switch floods the frame out all appropriate interfaces except the interface where the frame was received.

This process is known as **unknown unicast flooding**.

---

#  Broadcast Traffic

Broadcast Ethernet frames are forwarded out all switch interfaces in the same VLAN except the interface on which the frame was received.

This is important when protocols such as ARP are used to discover the MAC address associated with an IP address.

---

#  6. Clear Dynamic MAC Addresses

The lab also required clearing dynamically learned MAC addresses from the switches.

The Cisco IOS command is:

```text
clear mac address-table dynamic
```

After clearing the entries, the MAC address table can be checked again using:

```text
show mac address-table
```

New entries will be learned again when network traffic is generated.

> **Packet Tracer Note:** Depending on the switch model and Packet Tracer version, some variations of the MAC address clearing command may not behave exactly like physical Cisco IOS equipment. The important concept is understanding that dynamic MAC entries can be cleared and will be relearned when new frames arrive.

---

#  Important Commands Learned

| Command | Purpose |
|---|---|
| `show mac address-table` | Display the switch MAC address table |
| `clear mac address-table dynamic` | Clear dynamically learned MAC addresses |
| `ping <IP-address>` | Generate traffic and test connectivity |

---

#  What I Learned

From this lab, I learned:

- How Ethernet switches dynamically learn MAC addresses.
- That switches learn MAC addresses from the **source MAC address** of received Ethernet frames.
- How MAC addresses are associated with switch interfaces.
- How to view the MAC address table using Cisco IOS.
- The difference between known and unknown destination MAC addresses.
- How unknown unicast frames are flooded.
- How broadcast traffic is forwarded through a LAN.
- How network traffic causes switches to populate their MAC address tables.
- How ICMP traffic can be observed using Packet Tracer Simulation Mode.
- How to generate traffic using `ping`.
- How dynamic MAC address entries can be cleared and relearned.

---

#  Key Takeaway

A switch does not automatically know where every device on a LAN is located.

Instead, it **learns dynamically**.

When an Ethernet frame enters a switch, the switch examines the:

```text
Source MAC Address
```

and associates it with the:

```text
Incoming Interface
```

The switch stores this information in its MAC address table.

For future frames, the switch checks the destination MAC address against this table to determine where the frame should be forwarded.

This process allows Ethernet switches to forward traffic efficiently instead of sending every frame to every connected device.

---

##  Lab Evidence

During the lab, I captured screenshots showing:

1. The completed network topology
2. Successful ping communication between PCs
3. ICMP traffic moving through SW1 and SW2 in Simulation Mode
4. Dynamically learned entries in the switch MAC address table

---
