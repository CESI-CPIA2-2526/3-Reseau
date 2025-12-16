# Lab 01: Basic LAN Configuration - Solution Guide

## Answers to Lab Questions

### Question 1: Why do we use a straight-through cable instead of a crossover cable?

**Answer:** We use a straight-through cable because we are connecting **different types of devices** (PC to Switch).

- **Straight-through:** Used to connect devices of different types (PC-Switch, Switch-Router)
- **Crossover:** Used to connect devices of the same type (PC-PC, Switch-Switch, Router-Router)

Modern devices have Auto-MDIX which automatically detects and adjusts, but understanding the difference is essential.

---

### Question 2: What is the network address and broadcast address for this subnet?

**Answer:**
- **Network Address:** `192.168.10.0`
- **Broadcast Address:** `192.168.10.255`
- **Usable Host Range:** `192.168.10.1` to `192.168.10.254`

**Calculation:**
- Subnet Mask: `255.255.255.0` = `/24`
- This means the first 24 bits are the network portion
- Last 8 bits are for hosts: 2^8 - 2 = 254 usable addresses

---

### Question 3: What does the TTL value in the ping reply represent?

**Answer:** **TTL (Time To Live)** is a field in the IP header that prevents packets from circulating indefinitely in case of routing loops.

- Each router that forwards the packet decrements the TTL by 1
- If TTL reaches 0, the packet is discarded
- In this lab, you should see `TTL=128` (Windows default) or `TTL=64` (Linux/Cisco default)
- Since the PCs are on the same LAN (no router involved), the TTL value doesn't change

---

### Question 4: What layer of the OSI model does ARP operate at?

**Answer:** **Layer 2 (Data Link Layer)**, though it bridges Layer 2 and Layer 3.

- ARP resolves Layer 3 addresses (IP) into Layer 2 addresses (MAC)
- It operates at Layer 2 because it deals with MAC addresses
- The ARP request is broadcast at Layer 2 (FF:FF:FF:FF:FF:FF)

---

### Question 5: How many hops does the ICMP packet take from PC0 to PC1?

**Answer:** **1 hop** (just the switch).

However, technically, a "hop" refers to passing through a **router** (Layer 3 device). Since we only have a switch (Layer 2 device), some would argue there are **0 hops** in the routing sense.

In Packet Tracer Simulation Mode, you'll see:
1. PC0 sends the packet
2. Switch0 forwards it
3. PC1 receives it

---

### Question 6: At Layer 2, what source and destination MAC addresses are shown?

**Answer:**
- **Source MAC:** The MAC address of **PC0's FastEthernet0 interface**
- **Destination MAC:** The MAC address of **PC1's FastEthernet0 interface**

You can find these by clicking on each PC → **Config** tab → **FastEthernet0** → **MAC Address**.

Example (yours will differ):
- Source: `0001.42A3.6B7C`
- Destination: `00D0.D3F2.8A1E`

---

### Question 7: How many MAC addresses are in the switch's table? Why?

**Answer:** **2 MAC addresses** (one for PC0 and one for PC1).

**Explanation:**
- When PC0 sent the first frame, the switch learned PC0's MAC address on port Fa0/1
- When PC1 replied, the switch learned PC1's MAC address on port Fa0/2
- The switch builds this table dynamically by inspecting the **source MAC address** of incoming frames

**Sample Output:**
```
Switch#show mac address-table

          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0001.42a3.6b7c    DYNAMIC     Fa0/1
   1    00d0.d3f2.8a1e    DYNAMIC     Fa0/2
```

---

## Challenge Exercise Solution

**Challenge Question:** If you ping from PC0 to PC2, how many devices will learn the MAC address of PC0?

**Answer:** **Both the switch and PC2** will learn PC0's MAC address.

- **Switch0:** Learns PC0's MAC via the Ethernet frame's source MAC field
- **PC2:** Learns PC0's MAC via the ARP process (PC2 stores it in its ARP cache)
- **PC1:** Does NOT learn anything (it's not involved in this communication)

---

## Expected Packet Tracer Topology

```
        192.168.10.0/24

   PC0 (.10)
      |
      | Fa0/1
   [Switch0]
      | Fa0/2
      |
   PC1 (.11)
```

---

## Troubleshooting Common Issues

### Problem 1: Ping fails with "Destination host unreachable"

**Possible Causes:**
1. Incorrect IP configuration (wrong subnet)
2. Cable not properly connected
3. Switch ports still in orange (STP not converged)

**Solution:**
- Verify IP addresses with `ipconfig` on the PC
- Check cables are connected (green lights)
- Wait 30 seconds or fast-forward time

---

### Problem 2: ARP table is empty

**Cause:** No communication has occurred yet.

**Solution:** Ping the other PC first. ARP entries are created dynamically.

---

### Problem 3: Switch MAC table shows only 1 entry

**Cause:** Only one PC has sent a frame so far.

**Solution:** Ping from PC0 to PC1. This will cause both PCs to send frames, allowing the switch to learn both MAC addresses.

---

## Advanced Analysis

### Frame Flow Analysis

When PC0 pings PC1 for the first time:

1. **ARP Request (Broadcast):**
   - PC0 doesn't know PC1's MAC address
   - Sends ARP request: "Who has 192.168.10.11? Tell 192.168.10.10"
   - Destination MAC: `FF:FF:FF:FF:FF:FF` (broadcast)
   - Switch floods it out all ports except the incoming port

2. **ARP Reply (Unicast):**
   - PC1 responds: "192.168.10.11 is at [PC1's MAC]"
   - Destination MAC: PC0's MAC (unicast)
   - Switch forwards it only to Fa0/1 (because it learned PC0 is there)

3. **ICMP Echo Request:**
   - PC0 now knows PC1's MAC
   - Sends ICMP Echo Request with PC1's MAC as destination
   - Switch forwards to PC1

4. **ICMP Echo Reply:**
   - PC1 sends Echo Reply back to PC0
   - Switch forwards to PC0

---

## Real-World Application

This lab simulates the most basic network scenario: multiple computers connected to a switch in a home or small office network.

**In the real world:**
- Switches typically have 24 or 48 ports
- Managed switches allow VLAN configuration, port security, and QoS
- Unmanaged switches (like this lab) simply forward frames based on MAC addresses

---

## Grading Rubric

| Criteria                              | Points |
| :------------------------------------ | :----: |
| Correct topology built                |   2    |
| IP addressing configured correctly    |   2    |
| Successful ping between PCs           |   2    |
| Correct answers to Questions 1-7      |   7    |
| Simulation mode analysis completed    |   2    |
| Switch MAC table verified             |   2    |
| Challenge exercise (if attempted)     |   +2   |
| **Total**                             | **15** |

---

## Keywords Recap

| Term         | Definition                                          | OSI Layer |
| :----------- | :-------------------------------------------------- | :-------: |
| **LAN**      | Local Area Network                                  |   N/A     |
| **Switch**   | Forwards frames based on MAC addresses              |   L2      |
| **ARP**      | Maps IP to MAC addresses                            |   L2/L3   |
| **CAM**      | Content Addressable Memory (MAC table)              |   L2      |
| **Ping**     | ICMP Echo Request/Reply (tests connectivity)        |   L3      |
| **TTL**      | Time To Live (prevents infinite routing loops)      |   L3      |
| **Broadcast**| Sent to all devices in the network (FF:FF:FF:FF:FF:FF) |   L2      |

---

## Next Lab Preview

In **Lab 02: VLAN Configuration**, you will learn how to:
- Segment a single physical switch into multiple logical networks
- Configure trunk ports to carry multiple VLANs
- Understand inter-VLAN routing requirements

**Key Concept:** VLANs create separate broadcast domains on the same switch, improving security and reducing unnecessary traffic.
