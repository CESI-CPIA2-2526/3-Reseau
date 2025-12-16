# Lab 02: VLAN Configuration and Trunking - Solution Guide

## Answers to Lab Questions

### Question 1: Before configuring VLANs, can PC0 (192.168.10.10) ping PC1 (192.168.20.10)? Why or why not?

**Answer:** **No**, PC0 cannot ping PC1 because they are on **different IP subnets**.

**Explanation:**
- PC0 is on network `192.168.10.0/24`
- PC1 is on network `192.168.20.0/24`
- Without a router (Layer 3 device), devices on different subnets cannot communicate
- When PC0 tries to ping 192.168.20.10, it realizes the destination is not on its local network
- PC0 will attempt to send the packet to its default gateway (192.168.10.1), which doesn't exist yet

**Before VLANs:** They can't communicate due to different subnets
**After VLANs:** They STILL can't communicate (different subnets + VLAN isolation)

---

### Question 2: What is the difference between `running-config` and `startup-config`?

**Answer:**

| Configuration    | Description                                                      | Volatility |
| :--------------- | :--------------------------------------------------------------- | :--------- |
| **running-config** | Configuration currently active in RAM                          | Volatile (lost on reboot) |
| **startup-config** | Configuration saved to NVRAM (loaded on boot)                  | Non-volatile (persistent) |

**Key Points:**
- When you make changes via CLI, they are applied to `running-config` immediately
- If you reboot the switch without saving, all changes are lost
- Use `copy running-config startup-config` or `write memory` to save
- Use `show running-config` to see current configuration
- Use `show startup-config` to see saved configuration

**Real-World Scenario:** You configure VLANs on a switch but forget to save. Power outage occurs. All VLAN configurations are lost on reboot.

---

### Question 3: Which VLAN are unused ports assigned to by default?

**Answer:** **VLAN 1** (the default VLAN).

**Explanation:**
- All switch ports are members of VLAN 1 by default
- VLAN 1 cannot be deleted or renamed
- VLAN 1 is the default native VLAN for trunks

**Security Best Practice:** Move unused ports to a dummy VLAN (e.g., VLAN 999) and shut them down to prevent unauthorized access:
```
Switch(config)#interface range fa0/3-23
Switch(config-if-range)#switchport access vlan 999
Switch(config-if-range)#shutdown
```

---

### Question 4: What encapsulation protocol is used for trunking?

**Answer:** **802.1Q** (IEEE standard for VLAN tagging).

**Explanation:**
- 802.1Q inserts a 4-byte VLAN tag into the Ethernet frame header
- The tag contains the VLAN ID (VID)
- Cisco switches use 802.1Q by default
- **Legacy Protocol:** ISL (Inter-Switch Link) was Cisco's proprietary trunking protocol, now deprecated

**Frame Structure with 802.1Q:**
```
[Dest MAC | Source MAC | 802.1Q Tag (4 bytes) | EtherType | Data | FCS]
                        └─ Contains VLAN ID
```

---

### Question 5: Why can't PC0 communicate with PC1, even though they are connected to the same physical switch?

**Answer:** Because they are in **different VLANs**, which creates separate **broadcast domains** at Layer 2.

**Explanation:**
- VLANs provide logical segmentation on a physical switch
- Frames from VLAN 10 cannot cross into VLAN 20 at Layer 2
- The switch's VLAN filtering prevents this traffic
- Even if they were on the same subnet, VLAN isolation would still block communication

**To Enable Communication:** You would need a **Layer 3 device** (router or Layer 3 switch) to perform **inter-VLAN routing**.

---

### Question 6: At what OSI layer does VLAN segmentation occur?

**Answer:** **Layer 2 (Data Link Layer)**.

**Explanation:**
- VLANs operate at Layer 2 because they segment based on switch ports and MAC addresses
- VLAN tags are inserted into Ethernet frames (Layer 2)
- Switches (Layer 2 devices) enforce VLAN isolation
- To cross VLANs, you need Layer 3 routing

**Comparison:**
- **Layer 2 Segmentation:** VLANs (logical separation on same physical infrastructure)
- **Layer 3 Segmentation:** IP Subnets (requires routing to communicate)

---

## Complete Configuration Commands

### Switch0 Configuration

```
! Enter privileged EXEC mode
enable

! Enter global configuration mode
configure terminal

! Create VLANs
vlan 10
 name Sales
 exit

vlan 20
 name IT
 exit

! Configure access ports
interface fastEthernet 0/1
 switchport mode access
 switchport access vlan 10
 exit

interface fastEthernet 0/2
 switchport mode access
 switchport access vlan 20
 exit

! Configure trunk port
interface fastEthernet 0/24
 switchport mode trunk
 exit

! Exit and save
exit
write memory
```

### Switch1 Configuration

```
enable
configure terminal

vlan 10
 name Sales
 exit

vlan 20
 name IT
 exit

interface fastEthernet 0/1
 switchport mode access
 switchport access vlan 10
 exit

interface fastEthernet 0/2
 switchport mode access
 switchport access vlan 20
 exit

interface fastEthernet 0/24
 switchport mode trunk
 exit

exit
write memory
```

---

## Verification Command Outputs

### `show vlan brief` on Switch0

```
Switch#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/3, Fa0/4, Fa0/5, Fa0/6
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Gig0/1, Gig0/2
10   Sales                            active    Fa0/1
20   IT                               active    Fa0/2
```

### `show interfaces trunk` on Switch0

```
Switch#show interfaces trunk

Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/24      1-4094

Port        Vlans allowed and active in management domain
Fa0/24      1,10,20

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/24      1,10,20
```

**Interpretation:**
- Port Fa0/24 is in trunk mode
- Using 802.1Q encapsulation
- Native VLAN is 1
- VLANs 1, 10, and 20 are active and being carried on the trunk

---

## Connectivity Test Results

### Test 1: Intra-VLAN Communication (Should Work)

**From PC0 (192.168.10.10) to PC2 (192.168.10.11):**
```
C:\>ping 192.168.10.11

Pinging 192.168.10.11 with 32 bytes of data:

Reply from 192.168.10.11: bytes=32 time=1ms TTL=128
Reply from 192.168.10.11: bytes=32 time<1ms TTL=128
Reply from 192.168.10.11: bytes=32 time<1ms TTL=128
Reply from 192.168.10.11: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.10.11:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

✅ **Success** - Both PCs are in VLAN 10

---

### Test 2: Inter-VLAN Communication (Should Fail)

**From PC0 (192.168.10.10) to PC1 (192.168.20.10):**
```
C:\>ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

❌ **Failed** - PCs are in different VLANs (10 and 20)

---

## Challenge Exercise Solutions

### Challenge 1: Add a Third VLAN

**Switch1 Configuration:**
```
configure terminal

! Create VLAN 30
vlan 30
 name Management
 exit

! Assign port to VLAN 30
interface fastEthernet 0/3
 switchport mode access
 switchport access vlan 30
 exit

exit
write memory
```

**PC4 Configuration:**
- IP Address: `192.168.30.10`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.30.1`

**Verification:**
- PC4 can communicate with other devices in VLAN 30 (if any)
- PC4 cannot communicate with devices in VLAN 10 or 20

---

### Challenge 2: Native VLAN Configuration

**Why Change Native VLAN?**
- **Security:** VLAN 1 is well-known and often targeted in VLAN hopping attacks
- **Best Practice:** Use an unused VLAN (e.g., 99 or 999) as the native VLAN

**Configuration on Both Switches:**
```
configure terminal

! Create VLAN 99
vlan 99
 name Native
 exit

! Configure native VLAN on trunk
interface fastEthernet 0/24
 switchport trunk native vlan 99
 exit

exit
write memory
```

**Verification:**
```
Switch#show interfaces trunk

Port        Mode         Encapsulation  Status        Native vlan
Fa0/24      on           802.1q         trunking      99
```

**Important:** Both ends of the trunk must have the same native VLAN, or you'll get a "native VLAN mismatch" error.

---

## Troubleshooting Common Issues

### Problem 1: Devices in the same VLAN can't communicate

**Possible Causes:**
1. Port not assigned to the correct VLAN
2. Trunk not configured between switches
3. VLANs not created on both switches

**Diagnostic Commands:**
```
show vlan brief
show interfaces trunk
show interfaces fastEthernet 0/1 switchport
```

**Solution:** Verify VLAN assignments and trunk configuration.

---

### Problem 2: Native VLAN mismatch error

**Error Message:**
```
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on Fa0/24 (99), with Switch1 Fa0/24 (1)
```

**Cause:** The native VLAN is different on each end of the trunk.

**Solution:** Configure the same native VLAN on both switches:
```
interface fastEthernet 0/24
 switchport trunk native vlan 99
```

---

### Problem 3: Trunk not forming

**Symptoms:**
- `show interfaces trunk` shows no trunks
- Inter-switch VLAN communication fails

**Possible Causes:**
1. Wrong cable type (use straight-through, not crossover, if switches have Auto-MDIX)
2. Port not configured as trunk
3. Trunk allowed VLANs list doesn't include the VLAN

**Solution:**
```
interface fastEthernet 0/24
 switchport mode trunk
 switchport trunk allowed vlan all
```

---

## Real-World Application

### Use Cases for VLANs

1. **Departmental Segmentation:** Sales, IT, HR on separate VLANs
2. **Guest Networks:** Isolate guest Wi-Fi from corporate network
3. **Voice over IP (VoIP):** Separate voice traffic (VLAN 100) from data
4. **Security Zones:** Servers in DMZ VLAN, workstations in another
5. **Broadcast Domain Control:** Reduce broadcast traffic in large networks

### VLAN Design Best Practices

- **VLAN 1:** Don't use for user data; reserve for management or disable
- **Native VLAN:** Use a dedicated VLAN (not VLAN 1) and don't assign any ports to it
- **Management VLAN:** Create a separate VLAN for switch management interfaces
- **Naming:** Use descriptive names (Sales, IT) instead of generic names
- **Documentation:** Maintain a VLAN database with VLAN IDs, names, and IP subnets

---

## Grading Rubric

| Criteria                                      | Points |
| :-------------------------------------------- | :----: |
| Correct topology built with proper cabling    |   2    |
| VLANs created on both switches                |   2    |
| Ports correctly assigned to VLANs             |   3    |
| Trunk configured between switches             |   3    |
| Intra-VLAN communication successful           |   2    |
| Inter-VLAN communication properly blocked     |   2    |
| Correct answers to Questions 1-6              |   6    |
| Configuration saved on both switches          |   2    |
| Challenge exercises (if attempted)            |  +3    |
| **Total**                                     | **20** |

---

## Key Takeaways

1. **VLANs** create logical segmentation on physical switches (Layer 2)
2. **Access ports** belong to a single VLAN
3. **Trunk ports** carry traffic for multiple VLANs using 802.1Q tagging
4. Devices in different VLANs cannot communicate without a **router**
5. Always **save your configuration** to avoid losing changes on reboot

---

## Next Lab Preview

In **Lab 03: Static Routing**, you will:
- Configure a router to enable inter-VLAN routing
- Implement Router-on-a-Stick (ROAS) with subinterfaces
- Understand routing tables and static routes
- Enable communication between VLAN 10 and VLAN 20

**Key Concept:** VLANs segment at Layer 2; **routing** is required for Layer 3 communication between VLANs.
