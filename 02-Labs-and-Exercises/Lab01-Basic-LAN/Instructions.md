# Lab 01: Basic LAN Configuration

## Objectives

By the end of this lab, you will be able to:

- Build a simple LAN topology in Cisco Packet Tracer
- Configure IP addressing on end devices
- Verify connectivity using ping and ARP
- Use Simulation Mode to visualize Layer 2 and Layer 3 operations
- Understand the role of switches in a LAN environment

## Topology

```
PC0 (192.168.10.10/24) ---\
                           \
                            Switch0 (2960)
                           /
PC1 (192.168.10.11/24) ---/
```

## Equipment List

- 2x PC-PT (End Devices)
- 1x Switch 2960 (Network Device)
- 2x Copper Straight-Through Cables

## Estimated Time

30 minutes

---

## Part 1: Build the Physical Topology

### Step 1: Place Devices

1. Open Cisco Packet Tracer
2. From the **End Devices** section, drag two **PC-PT** devices onto the workspace
3. From the **Network Devices** section, select **Switches** and drag one **2960** switch onto the workspace
4. Arrange the devices in a logical layout

### Step 2: Cable the Devices

1. Click the **Connections** icon (Lightning Bolt)
2. Select the **Copper Straight-Through** cable (solid black line)
3. Connect **PC0** FastEthernet0 to **Switch0** FastEthernet0/1
4. Connect **PC1** FastEthernet0 to **Switch0** FastEthernet0/2

**Question 1:** Why do we use a straight-through cable instead of a crossover cable?

> **Wait for the switch ports to turn green.** This indicates the Spanning Tree Protocol (STP) has converged. You can speed this up by clicking the Fast Forward Time button (>>).

---

## Part 2: Configure IP Addressing

### Step 3: Configure PC0

1. Click on **PC0**
2. Navigate to the **Desktop** tab
3. Click **IP Configuration**
4. Enter the following information:
   - **IPv4 Address:** `192.168.10.10`
   - **Subnet Mask:** `255.255.255.0`
   - **Default Gateway:** `192.168.10.1` (we don't have a router yet, but this is good practice)

### Step 4: Configure PC1

1. Click on **PC1**
2. Navigate to the **Desktop** tab
3. Click **IP Configuration**
4. Enter the following information:
   - **IPv4 Address:** `192.168.10.11`
   - **Subnet Mask:** `255.255.255.0`
   - **Default Gateway:** `192.168.10.1`

**Question 2:** What is the network address and broadcast address for this subnet?

---

## Part 3: Verify Connectivity

### Step 5: Test with Ping

1. Click on **PC0**
2. Go to the **Desktop** tab and open **Command Prompt**
3. Type the following command:
   ```bash
   ping 192.168.10.11
   ```
4. You should see replies from PC1

**Question 3:** What does the TTL value in the ping reply represent?

### Step 6: View ARP Table

1. In the Command Prompt on PC0, type:
   ```bash
   arp -a
   ```
2. Observe the MAC address of PC1

**Question 4:** What layer of the OSI model does ARP operate at?

---

## Part 4: Use Simulation Mode

### Step 7: Visualize Packet Flow

1. Switch to **Simulation Mode** (bottom right of the screen)
2. Click **Edit Filters** and select only **ICMP** and **ARP**
3. Click the **Add Simple PDU** tool (envelope icon)
4. Click **PC0** as the source and **PC1** as the destination
5. Press **Play** or **Auto Capture/Play** in the Simulation Panel

**Question 5:** How many hops does the ICMP packet take from PC0 to PC1?

### Step 8: Inspect PDU Information

1. Click on the packet envelope when it reaches the **Switch**
2. Open the **PDU Information** window
3. Examine the **OSI Model** tab

**Question 6:** At Layer 2, what source and destination MAC addresses are shown?

---

## Part 5: Switch MAC Address Table

### Step 9: View the Switch's CAM Table

1. Click on **Switch0**
2. Go to the **CLI** tab
3. Press **Enter** to access the command line
4. Type:
   ```
   enable
   show mac address-table
   ```

**Question 7:** How many MAC addresses are in the table? Why?

---

## Verification Checklist

- [ ] All devices are properly cabled with green link lights
- [ ] PC0 can successfully ping PC1
- [ ] ARP table shows the MAC address of PC1
- [ ] Simulation mode shows packet flow through the switch
- [ ] Switch CAM table contains both PC MAC addresses

---

## Challenge Exercise (Optional)

Add a third PC (PC2) with IP address `192.168.10.12/24` to the network. Verify that all three PCs can communicate with each other.

**Challenge Question:** If you ping from PC0 to PC2, how many devices will learn the MAC address of PC0?

---

## Lab Questions Summary

1. Why do we use a straight-through cable instead of a crossover cable?
2. What is the network address and broadcast address for this subnet?
3. What does the TTL value in the ping reply represent?
4. What layer of the OSI model does ARP operate at?
5. How many hops does the ICMP packet take from PC0 to PC1?
6. At Layer 2, what source and destination MAC addresses are shown?
7. How many MAC addresses are in the switch's table? Why?

---

## Keywords

- **LAN (Local Area Network):** A network that connects devices in a limited area
- **Switch:** A Layer 2 device that forwards frames based on MAC addresses
- **ARP (Address Resolution Protocol):** Maps IP addresses to MAC addresses
- **CAM Table (Content Addressable Memory):** The switch's MAC address table
- **STP (Spanning Tree Protocol):** Prevents Layer 2 loops

---

## Next Steps

Once you complete this lab, proceed to **Lab 02: VLAN Configuration** to learn how to segment a LAN into multiple broadcast domains.
