# Lab 02: VLAN Configuration and Trunking

## Objectives

By the end of this lab, you will be able to:

- Explain the purpose and benefits of VLANs
- Create and name VLANs on a Cisco switch
- Assign switch ports to specific VLANs
- Configure trunk ports to carry multiple VLANs
- Verify VLAN configuration and connectivity
- Understand VLAN isolation at Layer 2

## Topology

```
PC0 (VLAN 10) ---\                    /--- PC2 (VLAN 10)
                  \                  /
                   Switch0 ======= Switch1
                  /       Trunk     \
PC1 (VLAN 20) ---/                   \--- PC3 (VLAN 20)

VLAN 10: Sales (192.168.10.0/24)
VLAN 20: IT (192.168.20.0/24)
```

## Equipment List

- 4x PC-PT (End Devices)
- 2x Switch 2960 (Network Devices)
- 4x Copper Straight-Through Cables (PCs to Switches)
- 1x Copper Straight-Through Cable (Trunk between switches)

## Estimated Time

45 minutes

---

## Scenario

You are a network administrator for a small company. Management wants to segment the network to separate the **Sales** department from the **IT** department for security and traffic management. You will use **VLANs** to create two logical networks on the same physical infrastructure.

**Requirements:**
- VLAN 10: Sales Department (192.168.10.0/24)
- VLAN 20: IT Department (192.168.20.0/24)
- Sales devices should NOT be able to communicate with IT devices at Layer 2

---

## Part 1: Build the Physical Topology

### Step 1: Place and Cable Devices

1. Place **2 switches** (2960) and **4 PCs** in the workspace
2. Label the PCs appropriately:
   - PC0: Sales-PC1
   - PC1: IT-PC1
   - PC2: Sales-PC2
   - PC3: IT-PC2

3. **Connect devices as follows:**
   - **Switch0 Fa0/1** → PC0 (Sales-PC1)
   - **Switch0 Fa0/2** → PC1 (IT-PC1)
   - **Switch1 Fa0/1** → PC2 (Sales-PC2)
   - **Switch1 Fa0/2** → PC3 (IT-PC2)
   - **Switch0 Fa0/24** → **Switch1 Fa0/24** (Trunk link)

Wait for all ports to turn green.

---

## Part 2: Configure IP Addressing

### Step 2: Configure PCs

| Device | IP Address     | Subnet Mask     | Default Gateway |
| :----- | :------------- | :-------------- | :-------------- |
| PC0    | 192.168.10.10  | 255.255.255.0   | 192.168.10.1    |
| PC1    | 192.168.20.10  | 255.255.255.0   | 192.168.20.1    |
| PC2    | 192.168.10.11  | 255.255.255.0   | 192.168.10.1    |
| PC3    | 192.168.20.11  | 255.255.255.0   | 192.168.20.1    |

Configure each PC using the **Desktop > IP Configuration** method.

**Question 1:** Before configuring VLANs, can PC0 (192.168.10.10) ping PC1 (192.168.20.10)? Why or why not?

---

## Part 3: Create VLANs on Switch0

### Step 3: Access the Switch CLI

1. Click on **Switch0**
2. Go to the **CLI** tab
3. Press **Enter**

### Step 4: Enter Privileged EXEC Mode

```
Switch>enable
Switch#
```

### Step 5: Enter Global Configuration Mode

```
Switch#configure terminal
Switch(config)#
```

### Step 6: Create VLAN 10 (Sales)

```
Switch(config)#vlan 10
Switch(config-vlan)#name Sales
Switch(config-vlan)#exit
```

### Step 7: Create VLAN 20 (IT)

```
Switch(config)#vlan 20
Switch(config-vlan)#name IT
Switch(config-vlan)#exit
```

### Step 8: Assign Ports to VLANs

**Assign Fa0/1 to VLAN 10 (Sales):**
```
Switch(config)#interface fastEthernet 0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit
```

**Assign Fa0/2 to VLAN 20 (IT):**
```
Switch(config)#interface fastEthernet 0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit
```

### Step 9: Configure Trunk Port

The link between Switch0 and Switch1 must carry traffic for both VLANs.

```
Switch(config)#interface fastEthernet 0/24
Switch(config-if)#switchport mode trunk
Switch(config-if)#exit
```

### Step 10: Save Configuration

```
Switch(config)#exit
Switch#write memory
```
or
```
Switch#copy running-config startup-config
```

**Question 2:** What is the difference between `running-config` and `startup-config`?

---

## Part 4: Configure Switch1

### Step 11: Repeat VLAN Configuration on Switch1

Repeat Steps 3-10 on **Switch1** with the following port assignments:
- **Fa0/1** → VLAN 10 (for PC2 - Sales-PC2)
- **Fa0/2** → VLAN 20 (for PC3 - IT-PC2)
- **Fa0/24** → Trunk (to Switch0)

**Instructor Tip:** Students should perform this independently to reinforce learning.

---

## Part 5: Verification

### Step 12: Verify VLAN Configuration

On **Switch0**, enter:

```
Switch#show vlan brief
```

**Expected Output:**
```
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/3, Fa0/4, Fa0/5, ...
10   Sales                            active    Fa0/1
20   IT                               active    Fa0/2
```

**Question 3:** Which VLAN are unused ports assigned to by default?

### Step 13: Verify Trunk Configuration

```
Switch#show interfaces trunk
```

**Expected Output:**
```
Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/24      1-4094
```

**Question 4:** What encapsulation protocol is used for trunking?

---

## Part 6: Test Connectivity

### Step 14: Test Intra-VLAN Communication

From **PC0** (VLAN 10), ping **PC2** (also VLAN 10):
```
ping 192.168.10.11
```

**Expected Result:** Success ✅

### Step 15: Test Inter-VLAN Isolation

From **PC0** (VLAN 10), ping **PC1** (VLAN 20):
```
ping 192.168.20.10
```

**Expected Result:** Failure ❌ (Request timed out)

**Question 5:** Why can't PC0 communicate with PC1, even though they are connected to the same physical switch?

---

## Part 7: Simulation Mode Analysis

### Step 16: Visualize VLAN Isolation

1. Switch to **Simulation Mode**
2. Set filters to show only **ICMP**
3. Send a Simple PDU from PC0 to PC1
4. Observe that the packet **does not cross the VLAN boundary**

**Question 6:** At what OSI layer does VLAN segmentation occur?

---

## Verification Checklist

- [ ] VLANs 10 and 20 created on both switches
- [ ] Ports correctly assigned to VLANs
- [ ] Trunk link configured between switches
- [ ] Devices in the same VLAN can communicate
- [ ] Devices in different VLANs cannot communicate
- [ ] Configuration saved to startup-config

---

## Challenge Exercise (Optional)

### Challenge 1: Add a Third VLAN

Create **VLAN 30 (Management)** and assign a new PC (PC4) with IP `192.168.30.10/24` to this VLAN on Switch1.

### Challenge 2: Native VLAN Configuration

Research and configure the **native VLAN** on the trunk to VLAN 99 (instead of the default VLAN 1). Why is this a security best practice?

---

## Lab Questions Summary

1. Before configuring VLANs, can PC0 ping PC1? Why or why not?
2. What is the difference between `running-config` and `startup-config`?
3. Which VLAN are unused ports assigned to by default?
4. What encapsulation protocol is used for trunking?
5. Why can't PC0 communicate with PC1, even though they are on the same physical switch?
6. At what OSI layer does VLAN segmentation occur?

---

## Keywords

- **VLAN (Virtual Local Area Network):** A logical network segment created on a switch
- **Access Port:** A switch port that belongs to a single VLAN
- **Trunk Port:** A switch port that carries traffic for multiple VLANs
- **802.1Q:** The IEEE standard for VLAN tagging on trunk links
- **Native VLAN:** The VLAN that is untagged on a trunk (default is VLAN 1)

---

## Common Switch Commands Reference

| Command                                      | Description                          |
| :------------------------------------------- | :----------------------------------- |
| `show vlan brief`                            | Display VLAN configuration           |
| `show interfaces trunk`                      | Show trunk port status               |
| `show running-config`                        | Display current configuration        |
| `show startup-config`                        | Display saved configuration          |
| `switchport mode access`                     | Set port as access port              |
| `switchport access vlan [number]`            | Assign port to a VLAN                |
| `switchport mode trunk`                      | Set port as trunk port               |
| `copy running-config startup-config`         | Save configuration                   |

---

## Next Steps

Once you complete this lab, you'll understand how VLANs segment broadcast domains at Layer 2. In **Lab 03: Static Routing**, you will learn how to enable communication between VLANs using a router (**inter-VLAN routing**).
