# Day 06 - IPv4 Addressing and Router Interface Configuration

## CCNA 200-301 Journey

This lab is part of my **CCNA 200-301 study journey** using **Jeremy's IT Lab**.

In this lab, I practiced configuring IPv4 addresses on Cisco router interfaces, enabling router interfaces, adding interface descriptions, configuring end devices, and testing connectivity between different IP networks.

---

##  Lab Objective

The objective of this lab was to configure **R1** so that it could provide connectivity between three different IPv4 networks.

The main tasks were:

- Configure the router hostname
- View router interfaces and their current status
- Configure IPv4 addresses on router interfaces
- Configure interface descriptions
- Enable router interfaces
- Verify interface configuration
- Examine the running configuration
- Configure IPv4 settings on PCs
- Test connectivity using `ping`

---

##  Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- IPv4
- ICMP / Ping
- Jeremy's IT Lab
- Git
- GitHub

---

#  Network Topology

The topology contained:

- **R1** - Cisco Router
- **SW1** - Cisco 2960 Switch
- **SW2** - Cisco 2960 Switch
- **SW3** - Cisco 2960 Switch
- **PC1**
- **PC2**
- **PC3**

R1 connected the three separate IPv4 networks.

---

#  Network Addressing

The three networks used in the lab were:

| Network | PC Address | Router Interface | Router IP |
|---|---|---|---|
| `15.0.0.0/8` | `15.0.0.1` | G0/0 | `15.255.255.254` |
| `182.98.0.0/16` | `182.98.0.1` | G0/1 | `182.98.255.254` |
| `201.191.20.0/24` | PC3 on this network | G0/2 | `201.191.20.254` |

This lab demonstrated how different subnet masks determine the network portion and host portion of an IPv4 address.

---

#  1. Configure R1 Hostname

I entered global configuration mode and changed the router hostname to **R1**.

```text
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)#
```

Configuring the hostname makes the router easier to identify when working from the Cisco IOS CLI.

---

#  2. Check Router Interfaces

Before configuring the interfaces, I checked their current IP addresses and operational status.

```text
show ip interface brief
```

From configuration mode, I used:

```text
do show ip interface brief
```

Initially, the GigabitEthernet interfaces were:

```text
unassigned
administratively down
down
```

This showed that the interfaces did not yet have IPv4 addresses and were administratively disabled.

---

#  3. Configure GigabitEthernet0/0

GigabitEthernet0/0 connects R1 to the `15.0.0.0/8` network.

I configured:

```text
R1(config)# interface g0/0
R1(config-if)# ip address 15.255.255.254 255.0.0.0
R1(config-if)# description ## To SW1 ##
R1(config-if)# no shutdown
```

The `/8` prefix corresponds to:

```text
255.0.0.0
```

After `no shutdown`, the interface changed to an operational state.

---

#  4. Configure GigabitEthernet0/1

GigabitEthernet0/1 connects R1 to the `182.98.0.0/16` network.

```text
R1(config)# interface g0/1
R1(config-if)# ip address 182.98.255.254 255.255.0.0
R1(config-if)# description ## To SW2 ##
R1(config-if)# no shutdown
```

The `/16` prefix corresponds to:

```text
255.255.0.0
```

---

#  5. Configure GigabitEthernet0/2

GigabitEthernet0/2 connects R1 to the `201.191.20.0/24` network.

```text
R1(config)# interface g0/2
R1(config-if)# ip address 201.191.20.254 255.255.255.0
R1(config-if)# description ## To SW3 ##
R1(config-if)# no shutdown
```

The `/24` prefix corresponds to:

```text
255.255.255.0
```

---

#  6. Router Interface Configuration

The completed router configuration included:

```text
interface GigabitEthernet0/0
 description ## To SW1 ##
 ip address 15.255.255.254 255.0.0.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 description ## To SW2 ##
 ip address 182.98.255.254 255.255.0.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/2
 description ## To SW3 ##
 ip address 201.191.20.254 255.255.255.0
 duplex auto
 speed auto
```

This confirmed that all three router interfaces had been assigned the appropriate IPv4 addresses.

---

#  7. Verify the Configuration

After configuring the interfaces, I verified them using:

```text
show ip interface brief
```

I also examined the running configuration using:

```text
show running-config
```

These commands allowed me to confirm:

- Interface IP addresses
- Interface status
- Interface descriptions
- Subnet masks
- Configuration changes

---

#  8. Save the Configuration

After confirming the router configuration, I saved it so that it would remain after a restart.

```text
copy running-config startup-config
```

Alternatively:

```text
write memory
```

This copies the active running configuration into NVRAM as the startup configuration.

---

#  9. Configure the PCs

The PCs were configured with IP addresses belonging to their respective networks.

For example:

### PC1

```text
IP Address: 15.0.0.1
Subnet Mask: 255.0.0.0
Default Gateway: 15.255.255.254
```

### PC2

```text
IP Address: 182.98.0.1
Subnet Mask: 255.255.0.0
Default Gateway: 182.98.255.254
```

The default gateway of each PC is the IP address of the R1 interface connected to that PC's network.

---

#  10. Test Connectivity

After configuring the router and PCs, I tested network connectivity using `ping`.

From the PCs, I sent ICMP Echo Requests to devices on the other networks.

Example:

```text
ping 15.0.0.1
```

and:

```text
ping 182.98.0.1
```

and:

```text
ping 201.191.20.254
```

The successful responses demonstrated that R1 was able to route traffic between the connected IPv4 networks.

---

#  Ping Results

For example, one of the tests returned:

```text
Packets: Sent = 4, Received = 4, Lost = 0
```

which represents:

```text
0% packet loss
```

Another test initially showed one timeout followed by successful replies.

This can occur during the first ping while devices perform ARP resolution before sending the ICMP traffic.

Subsequent communication was successful.

---

#  How the Router Connects the Networks

The three networks are separate IPv4 networks:

```text
15.0.0.0/8
182.98.0.0/16
201.191.20.0/24
```

A host on one network cannot communicate directly with a host on another network using Layer 2 switching alone.

R1 provides Layer 3 connectivity between them.

For example:

```text
PC1
 |
SW1
 |
R1
 |
SW2
 |
PC2
```

When PC1 wants to communicate with PC2, it recognizes that PC2 belongs to a different network.

PC1 therefore forwards the packet to its **default gateway**, which is R1.

R1 examines the destination IPv4 address and forwards the packet through the appropriate interface.

---

#  Important Commands Learned

| Command | Purpose |
|---|---|
| `enable` | Enter privileged EXEC mode |
| `configure terminal` | Enter global configuration mode |
| `hostname R1` | Configure the router hostname |
| `show ip interface brief` | Display interface IP addresses and status |
| `interface g0/0` | Enter interface configuration mode |
| `ip address <IP> <mask>` | Assign an IPv4 address to an interface |
| `description` | Add a description to an interface |
| `no shutdown` | Administratively enable an interface |
| `show running-config` | View the active router configuration |
| `copy running-config startup-config` | Save the router configuration |
| `ping <IP>` | Test IP connectivity |

---

#  What I Learned

From this lab, I learned:

- How to configure IPv4 addresses on Cisco router interfaces.
- How subnet masks correspond to `/8`, `/16`, and `/24` prefix lengths.
- How to use `show ip interface brief` to quickly check router interfaces.
- What `administratively down` means on a Cisco interface.
- How `no shutdown` enables a router interface.
- How to add useful descriptions to router interfaces.
- How to verify configurations using `show` commands.
- How to configure IP addresses and default gateways on end devices.
- How routers provide communication between different IPv4 networks.
- How to test Layer 3 connectivity using `ping`.
- Why the first ping may occasionally time out while ARP information is being learned.
- How to save the running configuration so it persists after a reboot.

---

#  Key Takeaway

The major lesson from this lab was that a router connects **different IP networks**.

Each router interface belongs to a different network and must have an appropriate IP address.

In this topology:

```text
G0/0 → 15.0.0.0/8
G0/1 → 182.98.0.0/16
G0/2 → 201.191.20.0/24
```

The router interface also acts as the **default gateway** for hosts on that network.

Another important lesson was that configuring an IP address alone is not enough on a Cisco router interface.

The interface must also be enabled using:

```text
no shutdown
```

Once the router interfaces and PCs were correctly configured, R1 successfully routed traffic between all three networks.

---

##  Lab Evidence

Screenshots from the completed lab demonstrate:

1. The three-network Packet Tracer topology
2. R1 interface IPv4 configuration
3. Interface descriptions and `no shutdown`
4. The completed running configuration
5. Successful ping tests between the networks

---

