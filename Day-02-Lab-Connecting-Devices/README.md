# Day 02 - Connecting Devices

## CCNA 200-301 Journey

This lab is part of my **CCNA 200-301 study journey** using **Jeremy's IT Lab**.

Day 2 focused on **network interfaces, Ethernet cables, and connecting network devices** in Cisco Packet Tracer.

---

##  Lab Objective

The objective of this lab was to practice connecting different network devices using the appropriate interfaces and cable types.

The lab helped me understand how devices are physically connected before higher-level configurations such as IP addressing, VLANs, and routing can take place.

---

##  Tools Used

- Cisco Packet Tracer
- Jeremy's IT Lab
- Git
- GitHub

---

##  Concepts Covered

### Network Interfaces

Network devices communicate through physical or logical interfaces.

Common Ethernet interfaces include:

- FastEthernet
- GigabitEthernet

Examples of Cisco interface names include:

```text
FastEthernet0/1
FastEthernet0/2
GigabitEthernet0/0
GigabitEthernet0/1
🔌 Ethernet Cable Types
Copper Straight-Through Cable

Traditionally, a straight-through cable is used when connecting different types of Ethernet devices.

Examples:

PC -------- Switch
Router ---- Switch
Server ---- Switch
Copper Crossover Cable

Traditionally, a crossover cable is used when connecting similar types of Ethernet devices.

Examples:

Switch ---- Switch
Router ---- Router
PC -------- PC


Auto MDI-X

Modern Ethernet interfaces often support Auto MDI-X.

Auto MDI-X allows a device to automatically detect whether a straight-through or crossover connection is required and adjust the interface accordingly.

Although modern devices can often handle either cable type automatically, understanding the traditional cabling rules is still important for networking fundamentals and the CCNA exam.


Copper Ethernet

Copper Ethernet commonly uses Unshielded Twisted Pair (UTP) cables with RJ-45 connectors.

Common Ethernet standards include:

Standard	Speed
10BASE-T	10 Mbps
100BASE-TX	100 Mbps
1000BASE-T	1 Gbps
10GBASE-T	10 Gbps

Copper Ethernet is commonly used for connecting end devices, switches, routers, and other network equipment over shorter distances.


Fiber-Optic Cabling

Fiber-optic cables transmit data using light signals instead of electrical signals.

Some advantages of fiber include:

Longer transmission distances
Higher bandwidth capabilities
Resistance to electromagnetic interference
Suitable for high-speed network links

Lab Tasks Completed

During this lab, I:

Opened the Day 2 lab in Cisco Packet Tracer
Identified the available interfaces on the network devices
Selected appropriate interfaces for each connection
Connected devices using Ethernet cables
Practiced choosing the correct cable type
Observed interface and link status
Became more familiar with connecting devices in Cisco Packet Tracer

What I Learned

From this lab, I learned that:

Network devices communicate through network interfaces
Interfaces can support different Ethernet speeds
The physical connection must be correct before devices can communicate
Straight-through cables are traditionally used between different device types
Crossover cables are traditionally used between similar device types
Auto MDI-X allows modern Ethernet devices to automatically adjust to the cable type being used
Copper and fiber cables have different characteristics and use cases
Understanding physical connectivity is an important foundation for networking

Key Takeaway

Before configuring IP addresses, VLANs, routing protocols, or other network services, devices must first be properly connected.

Understanding interfaces, Ethernet standards, cable types, and physical connections is an important foundation for the rest of my CCNA journey.

Status

Day 02 Completed ✅
