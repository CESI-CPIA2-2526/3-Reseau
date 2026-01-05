# IP Addressing: IPv4 and IPv6

## Introduction

**IP (Internet Protocol)** is a Layer 3 (Network Layer) protocol responsible for addressing and routing packets of data across networks. IP provides the foundation for internetworking by enabling devices to identify and communicate with each other across different networks.

There are two versions of IP in use today:
- **IPv4 (Internet Protocol version 4):** The traditional addressing system, still widely used but running out of addresses.
- **IPv6 (Internet Protocol version 6):** The next-generation protocol designed to solve IPv4's address exhaustion problem.

Both protocols serve the same fundamental purpose: uniquely identifying devices and routing data between them. However, they differ significantly in structure, capacity, and features.

## Learning Objectives

By the end of this module, you will be able to:

- Explain the purpose and structure of IP addresses.
- Understand IPv4 address classes and subnet masks.
- Convert between binary and dotted-decimal notation.
- Describe the differences between IPv4 and IPv6.
- Identify the structure and types of IPv6 addresses.
- Explain why the industry is transitioning from IPv4 to IPv6.

---

## Part 1: IPv4 (Internet Protocol version 4)

### What is IPv4?

IPv4 is a 32-bit addressing scheme that provides approximately **4.3 billion** unique addresses. Each IPv4 address is written in **dotted-decimal notation**, divided into four 8-bit sections (octets).

**Example:**
```
192.168.1.10
```

In binary:
```
11000000.10101000.00000001.00001010
```

### IPv4 Address Structure

| Component | Size | Description |
|:----------|:-----|:------------|
| **Network Portion** | Variable | Identifies the network the device belongs to. |
| **Host Portion** | Variable | Identifies the specific device within that network. |

The boundary between the network and host portions is determined by the **subnet mask**.

### Subnet Mask

A **subnet mask** is a 32-bit number that divides an IP address into network and host portions.

**Example:**
```
IP Address:    192.168.1.10
Subnet Mask:   255.255.255.0
```

In binary:
```
IP Address:    11000000.10101000.00000001.00001010
Subnet Mask:   11111111.11111111.11111111.00000000
                ↑ Network (24 bits)      ↑ Host (8 bits)
```

The subnet mask has:
- **1s** where the network bits are located.
- **0s** where the host bits are located.

This is also written in **CIDR notation**: `192.168.1.10/24` (where /24 means 24 network bits).

### IPv4 Address Classes

IPv4 addresses were originally divided into five classes (A, B, C, D, E). Classes A, B, and C are used for normal host addressing.

| Class | First Octet Range | Default Subnet Mask | Network/Host Bits | Total Networks | Hosts per Network |
|:------|:------------------|:--------------------|:------------------|:---------------|:------------------|
| **A** | 1 - 126 | 255.0.0.0 (/8) | 8/24 | 128 | 16,777,214 |
| **B** | 128 - 191 | 255.255.0.0 (/16) | 16/16 | 16,384 | 65,534 |
| **C** | 192 - 223 | 255.255.255.0 (/24) | 24/8 | 2,097,152 | 254 |
| **D** | 224 - 239 | (Multicast) | - | - | - |
| **E** | 240 - 255 | (Reserved) | - | - | - |

**Note:** 127.x.x.x is reserved for **loopback** (testing on local machine, e.g., 127.0.0.1).

### Special IPv4 Addresses

| Address Type | Example | Description |
|:-------------|:--------|:------------|
| **Network Address** | 192.168.1.0 | First address in a subnet (all host bits are 0). |
| **Broadcast Address** | 192.168.1.255 | Last address in a subnet (all host bits are 1). |
| **Private Addresses** | 10.0.0.0/8<br>172.16.0.0/12<br>192.168.0.0/16 | Reserved for internal networks (not routable on the internet). |
| **Loopback** | 127.0.0.1 | Used for testing network software on the local machine. |
| **APIPA** | 169.254.x.x | Auto-assigned when DHCP fails. |

### IPv4 Header Format

The IPv4 header contains essential information for routing and delivering packets.

| Field | Size | Description |
|:------|:-----|:------------|
| **Version** | 4 bits | IP version (4 for IPv4). |
| **Header Length (IHL)** | 4 bits | Length of the header in 32-bit words. |
| **Type of Service (ToS)** | 8 bits | Quality of Service (priority/delay). |
| **Total Length** | 16 bits | Total size of the packet (header + data). |
| **Identification** | 16 bits | Identifies fragments of a packet. |
| **Flags** | 3 bits | Controls fragmentation (Don't Fragment, More Fragments). |
| **Fragment Offset** | 13 bits | Position of the fragment in the original packet. |
| **Time to Live (TTL)** | 8 bits | Maximum number of hops before the packet is discarded. |
| **Protocol** | 8 bits | Upper-layer protocol (e.g., TCP=6, UDP=17, ICMP=1). |
| **Header Checksum** | 16 bits | Error-checking for the header. |
| **Source IP Address** | 32 bits | IP address of the sender. |
| **Destination IP Address** | 32 bits | IP address of the receiver. |
| **Options** | Variable | Optional fields (rarely used). |

### IPv4 Limitations

1. **Address Exhaustion:** Only ~4.3 billion addresses are available. With billions of devices online, IPv4 addresses are running out.
2. **Complex NAT (Network Address Translation):** Private networks share public IPs, adding complexity.
3. **No Built-in Security:** IPsec is optional.
4. **No Auto-configuration:** Requires manual configuration or DHCP.

---

## Part 2: IPv6 (Internet Protocol version 6)

### What is IPv6?

IPv6 is a **128-bit** addressing scheme designed to replace IPv4. It provides approximately **340 undecillion** (3.4 × 10³⁸) unique addresses—enough to assign an IP to every atom on Earth's surface.

**Example:**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

### IPv6 Address Structure

IPv6 addresses are written in **hexadecimal** and divided into **eight 16-bit blocks**, separated by colons.

**Full Format:**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

**Shortening Rules:**
1. **Leading zeros** in a block can be omitted:
   ```
   2001:db8:85a3:0:0:8a2e:370:7334
   ```

2. **Consecutive blocks of zeros** can be replaced with `::` (only once per address):
   ```
   2001:db8:85a3::8a2e:370:7334
   ```

**Loopback Address:**
```
::1  (equivalent to 127.0.0.1 in IPv4)
```

**Unspecified Address:**
```
::  (equivalent to 0.0.0.0 in IPv4)
```

### IPv6 Address Types

| Type | Description | Example |
|:-----|:------------|:--------|
| **Unicast** | Identifies a single interface. Packet is delivered to one device. | 2001:db8::1 |
| **Multicast** | Identifies a group of interfaces. Packet is delivered to all members of the group. | ff00::/8 |
| **Anycast** | Assigned to multiple devices. Packet is delivered to the nearest one (routing determines proximity). | Same format as unicast |

**Note:** IPv6 does **not** use broadcast. It uses **multicast** instead.

### IPv6 Unicast Address Scopes

| Scope | Prefix | Description |
|:------|:-------|:------------|
| **Global Unicast** | 2000::/3 | Routable on the internet (equivalent to public IPv4 addresses). |
| **Link-Local** | fe80::/10 | Used for communication within a single network segment (not routable). Auto-configured. |
| **Unique Local** | fc00::/7 (typically fd00::/8) | Private addresses (equivalent to 10.x.x.x, 192.168.x.x in IPv4). |
| **Loopback** | ::1/128 | Local testing (equivalent to 127.0.0.1). |

### IPv6 Header Format

The IPv6 header is **simpler and more efficient** than IPv4.

| Field | Size | Description |
|:------|:-----|:------------|
| **Version** | 4 bits | IP version (6 for IPv6). |
| **Traffic Class** | 8 bits | Similar to ToS in IPv4 (QoS). |
| **Flow Label** | 20 bits | Identifies packets belonging to the same flow (for QoS). |
| **Payload Length** | 16 bits | Size of the data (excluding header). |
| **Next Header** | 8 bits | Identifies the next extension header or upper-layer protocol (e.g., TCP, UDP). |
| **Hop Limit** | 8 bits | Equivalent to TTL in IPv4. |
| **Source Address** | 128 bits | IPv6 address of the sender. |
| **Destination Address** | 128 bits | IPv6 address of the receiver. |

**Key Differences from IPv4:**
- **No Header Checksum:** Relies on upper-layer protocols for error checking.
- **No Fragmentation Fields:** Routers do not fragment packets; this is handled by the source.
- **Extension Headers:** Optional features (like fragmentation) are handled via extension headers, making the base header simpler.

### IPv6 Advantages Over IPv4

| Feature | IPv4 | IPv6 |
|:--------|:-----|:-----|
| **Address Space** | 32-bit (~4.3 billion) | 128-bit (~340 undecillion) |
| **Address Configuration** | Manual or DHCP | Auto-configuration (SLAAC) + DHCPv6 |
| **Header Complexity** | Complex (variable options) | Simplified (fixed + extensions) |
| **Fragmentation** | By routers | By source only |
| **Security** | IPsec optional | IPsec mandatory (in original design) |
| **Broadcast** | Yes | No (uses multicast) |
| **NAT** | Widely used | Not needed (ample addresses) |

### IPv6 Auto-Configuration (SLAAC)

IPv6 supports **Stateless Address Autoconfiguration (SLAAC)**, allowing devices to automatically generate their own IP addresses without a DHCP server.

**Process:**
1. Device generates a **link-local address** (fe80::/10) using its MAC address.
2. Device sends a **Router Solicitation (RS)** message.
3. Router responds with a **Router Advertisement (RA)** containing the network prefix.
4. Device combines the prefix with its interface identifier to create a **global unicast address**.

---

## IPv4 vs IPv6: Summary Table

| Aspect | IPv4 | IPv6 |
|:-------|:-----|:-----|
| **Address Length** | 32 bits | 128 bits |
| **Address Format** | Dotted-decimal (192.168.1.1) | Hexadecimal (2001:db8::1) |
| **Total Addresses** | ~4.3 billion | ~340 undecillion |
| **Header Size** | 20-60 bytes (variable) | 40 bytes (fixed) |
| **Broadcast** | Yes | No (multicast instead) |
| **Fragmentation** | Routers + source | Source only |
| **Security** | Optional (IPsec) | Built-in (IPsec) |
| **Configuration** | Manual/DHCP | Auto-config (SLAAC) + DHCPv6 |
| **NAT** | Common | Unnecessary |

---

## Transition from IPv4 to IPv6

The internet is gradually transitioning from IPv4 to IPv6. Several mechanisms allow both protocols to coexist:

### 1. **Dual Stack**
Devices run both IPv4 and IPv6 simultaneously. They can communicate using either protocol depending on what the destination supports.

### 2. **Tunneling**
IPv6 packets are encapsulated inside IPv4 packets to traverse IPv4-only networks.

**Common Tunneling Protocols:**
- **6to4**
- **Teredo**
- **ISATAP**

### 3. **Translation (NAT64)**
Allows IPv6-only devices to communicate with IPv4-only devices through a translator.

---

## Practical Examples

### IPv4 Subnetting Example

**Network:** 192.168.1.0/24

| Component | Value |
|:----------|:------|
| Network Address | 192.168.1.0 |
| First Usable Host | 192.168.1.1 |
| Last Usable Host | 192.168.1.254 |
| Broadcast Address | 192.168.1.255 |
| Total Hosts | 254 |

### IPv6 Address Example

**Full Address:**
```
2001:0db8:0000:0042:0000:0000:0000:0001
```

**Shortened:**
```
2001:db8:0:42::1
```

**Breakdown:**
- **2001:db8:0:42** → Network prefix (64 bits)
- **::1** → Interface identifier (64 bits)