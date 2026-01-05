# IP Addressing Quick Reference Guide

This document provides comprehensive reference tables for IPv4 and IPv6 addressing, subnet masks, and CIDR notation.

---

## IPv4 Subnet Mask Reference Table

### CIDR Notation and Subnet Masks

| CIDR | Subnet Mask | Wildcard Mask | Binary Notation | Network Bits | Host Bits | Total IPs | Usable Hosts |
|:-----|:------------|:--------------|:----------------|:-------------|:----------|:----------|:-------------|
| /32 | 255.255.255.255 | 0.0.0.0 | 11111111.11111111.11111111.11111111 | 32 | 0 | 1 | 1 (host route) |
| /31 | 255.255.255.254 | 0.0.0.1 | 11111111.11111111.11111111.11111110 | 31 | 1 | 2 | 2 (point-to-point) |
| /30 | 255.255.255.252 | 0.0.0.3 | 11111111.11111111.11111111.11111100 | 30 | 2 | 4 | 2 |
| /29 | 255.255.255.248 | 0.0.0.7 | 11111111.11111111.11111111.11111000 | 29 | 3 | 8 | 6 |
| /28 | 255.255.255.240 | 0.0.0.15 | 11111111.11111111.11111111.11110000 | 28 | 4 | 16 | 14 |
| /27 | 255.255.255.224 | 0.0.0.31 | 11111111.11111111.11111111.11100000 | 27 | 5 | 32 | 30 |
| /26 | 255.255.255.192 | 0.0.0.63 | 11111111.11111111.11111111.11000000 | 26 | 6 | 64 | 62 |
| /25 | 255.255.255.128 | 0.0.0.127 | 11111111.11111111.11111111.10000000 | 25 | 7 | 128 | 126 |
| /24 | 255.255.255.0 | 0.0.0.255 | 11111111.11111111.11111111.00000000 | 24 | 8 | 256 | 254 |
| /23 | 255.255.254.0 | 0.0.1.255 | 11111111.11111111.11111110.00000000 | 23 | 9 | 512 | 510 |
| /22 | 255.255.252.0 | 0.0.3.255 | 11111111.11111111.11111100.00000000 | 22 | 10 | 1,024 | 1,022 |
| /21 | 255.255.248.0 | 0.0.7.255 | 11111111.11111111.11111000.00000000 | 21 | 11 | 2,048 | 2,046 |
| /20 | 255.255.240.0 | 0.0.15.255 | 11111111.11111111.11110000.00000000 | 20 | 12 | 4,096 | 4,094 |
| /19 | 255.255.224.0 | 0.0.31.255 | 11111111.11111111.11100000.00000000 | 19 | 13 | 8,192 | 8,190 |
| /18 | 255.255.192.0 | 0.0.63.255 | 11111111.11111111.11000000.00000000 | 18 | 14 | 16,384 | 16,382 |
| /17 | 255.255.128.0 | 0.0.127.255 | 11111111.11111111.10000000.00000000 | 17 | 15 | 32,768 | 32,766 |
| /16 | 255.255.0.0 | 0.0.255.255 | 11111111.11111111.00000000.00000000 | 16 | 16 | 65,536 | 65,534 |
| /15 | 255.254.0.0 | 0.1.255.255 | 11111111.11111110.00000000.00000000 | 15 | 17 | 131,072 | 131,070 |
| /14 | 255.252.0.0 | 0.3.255.255 | 11111111.11111100.00000000.00000000 | 14 | 18 | 262,144 | 262,142 |
| /13 | 255.248.0.0 | 0.7.255.255 | 11111111.11111000.00000000.00000000 | 13 | 19 | 524,288 | 524,286 |
| /12 | 255.240.0.0 | 0.15.255.255 | 11111111.11110000.00000000.00000000 | 12 | 20 | 1,048,576 | 1,048,574 |
| /11 | 255.224.0.0 | 0.31.255.255 | 11111111.11100000.00000000.00000000 | 11 | 21 | 2,097,152 | 2,097,150 |
| /10 | 255.192.0.0 | 0.63.255.255 | 11111111.11000000.00000000.00000000 | 10 | 22 | 4,194,304 | 4,194,302 |
| /9 | 255.128.0.0 | 0.127.255.255 | 11111111.10000000.00000000.00000000 | 9 | 23 | 8,388,608 | 8,388,606 |
| /8 | 255.0.0.0 | 0.255.255.255 | 11111111.00000000.00000000.00000000 | 8 | 24 | 16,777,216 | 16,777,214 |

---

## IPv4 Address Classes

| Class | First Octet | First Octet Range | Default Mask | CIDR | Leading Bits | Purpose | Number of Networks | Hosts per Network |
|:------|:------------|:------------------|:-------------|:-----|:-------------|:--------|:-------------------|:------------------|
| **A** | 0xxxxxxx | 1 - 126 | 255.0.0.0 | /8 | 0 | Large networks | 128 (2⁷) | 16,777,214 |
| **B** | 10xxxxxx | 128 - 191 | 255.255.0.0 | /16 | 10 | Medium networks | 16,384 (2¹⁴) | 65,534 |
| **C** | 110xxxxx | 192 - 223 | 255.255.255.0 | /24 | 110 | Small networks | 2,097,152 (2²¹) | 254 |
| **D** | 1110xxxx | 224 - 239 | N/A | N/A | 1110 | Multicast | N/A | N/A |
| **E** | 1111xxxx | 240 - 255 | N/A | N/A | 1111 | Experimental | N/A | N/A |

---

## IPv4 Special Address Ranges

| Address Range | CIDR | Purpose | Routable on Internet |
|:--------------|:-----|:--------|:---------------------|
| 0.0.0.0/8 | /8 | Current network (only valid as source) | No |
| 10.0.0.0/8 | /8 | Private network (Class A) | No |
| 127.0.0.0/8 | /8 | Loopback addresses | No |
| 169.254.0.0/16 | /16 | Link-local (APIPA - Automatic Private IP Addressing) | No |
| 172.16.0.0/12 | /12 | Private network (Class B) | No |
| 192.0.0.0/24 | /24 | IETF Protocol Assignments | No |
| 192.0.2.0/24 | /24 | Documentation and examples (TEST-NET-1) | No |
| 192.168.0.0/16 | /16 | Private network (Class C) | No |
| 198.18.0.0/15 | /15 | Benchmark testing | No |
| 198.51.100.0/24 | /24 | Documentation and examples (TEST-NET-2) | No |
| 203.0.113.0/24 | /24 | Documentation and examples (TEST-NET-3) | No |
| 224.0.0.0/4 | /4 | Multicast (Class D) | Varies |
| 240.0.0.0/4 | /4 | Reserved (Class E) | No |
| 255.255.255.255/32 | /32 | Limited broadcast | No |

---

## IPv6 Address Types and Prefixes

| Address Type | Prefix | Scope | Description | Example |
|:-------------|:-------|:------|:------------|:--------|
| **Unspecified** | ::/128 | - | Equivalent to 0.0.0.0 in IPv4 | :: |
| **Loopback** | ::1/128 | Host | Equivalent to 127.0.0.1 in IPv4 | ::1 |
| **Global Unicast** | 2000::/3 | Global | Routable on the internet (public addresses) | 2001:db8::1 |
| **Link-Local Unicast** | fe80::/10 | Link | Communication within the same network segment | fe80::1 |
| **Unique Local** | fc00::/7 | Organization | Private addresses (typically fd00::/8 used) | fd00::1 |
| **Multicast** | ff00::/8 | Varies | Group communication (replaces broadcast) | ff02::1 |
| **IPv4-Mapped IPv6** | ::ffff:0:0/96 | - | IPv4 address embedded in IPv6 format | ::ffff:192.0.2.1 |
| **6to4** | 2002::/16 | Global | IPv6 over IPv4 tunneling | 2002:c000:0201::1 |
| **Documentation** | 2001:db8::/32 | - | Used in documentation and examples | 2001:db8::1 |

---

## IPv6 Multicast Address Scopes

| Scope | Prefix | Description | Example |
|:------|:-------|:------------|:--------|
| **Interface-Local** | ff01::/16 | Packets stay on the local interface | ff01::1 |
| **Link-Local** | ff02::/16 | Packets stay on the local network segment | ff02::1 (all nodes) |
| **Site-Local** | ff05::/16 | Packets stay within the organization | ff05::2 |
| **Organization-Local** | ff08::/16 | Multiple sites within an organization | ff08::1 |
| **Global** | ff0e::/16 | Internet-wide multicast | ff0e::1 |

### Common IPv6 Multicast Addresses

| Address | Description |
|:--------|:------------|
| ff02::1 | All nodes on the link-local segment |
| ff02::2 | All routers on the link-local segment |
| ff02::5 | All OSPF routers |
| ff02::6 | All OSPF designated routers |
| ff02::9 | All RIP routers |
| ff02::a | All EIGRP routers |
| ff02::d | All PIM routers |
| ff02::1:2 | All DHCP agents (servers and relays) |

---

## IPv6 Prefix Length Reference

| Prefix | Number of Subnets | Addresses per Subnet | Common Use |
|:-------|:------------------|:---------------------|:-----------|
| /128 | 1 | 1 (host address) | Single host route |
| /127 | 2 | 2 | Point-to-point links |
| /126 | 4 | 4 | Point-to-point links (legacy) |
| /124 | 16 | 16 | Very small subnet |
| /120 | 256 | 256 | Small subnet |
| /112 | 65,536 | 65,536 | Medium subnet |
| /64 | 18,446,744,073,709,551,616 | 18.4 quintillion | **Standard subnet** (SLAAC) |
| /56 | 256 subnets | 256 x /64 subnets | Typical home/small business allocation |
| /48 | 65,536 subnets | 65,536 x /64 subnets | Typical site/organization allocation |
| /32 | 4,294,967,296 subnets | 4.3 billion x /64 subnets | ISP allocation |

**Note:** /64 is the recommended prefix length for IPv6 subnets. It allows for SLAAC (Stateless Address Autoconfiguration) and provides enough addresses for any practical need.

---

## IPv4 vs IPv6 Comparison

| Feature | IPv4 | IPv6 |
|:--------|:-----|:-----|
| **Address Length** | 32 bits | 128 bits |
| **Address Format** | Dotted-decimal (192.168.1.1) | Hexadecimal colon notation (2001:db8::1) |
| **Total Addresses** | ~4.3 billion (2³²) | ~340 undecillion (2¹²⁸) |
| **Address Representation** | 4 octets (8 bits each) | 8 hextets (16 bits each) |
| **Typical Subnet** | /24 (254 hosts) | /64 (18.4 quintillion addresses) |
| **Private Address Ranges** | 10.0.0.0/8<br>172.16.0.0/12<br>192.168.0.0/16 | fc00::/7 (typically fd00::/8) |
| **Loopback** | 127.0.0.1 | ::1 |
| **Unspecified** | 0.0.0.0 | :: |
| **Broadcast** | 255.255.255.255 (and subnet broadcasts) | Not used (multicast instead) |
| **Multicast Range** | 224.0.0.0/4 (Class D) | ff00::/8 |
| **Auto-configuration** | DHCP | SLAAC + DHCPv6 |
| **Address Assignment** | Manual, DHCP | SLAAC, DHCPv6, Manual |

---

## Subnetting Quick Calculation Guide

### The Powers of 2 Table (Essential for Subnetting)

| Exponent | Value | Subnet Mask Octet | CIDR Block Size |
|:---------|:------|:------------------|:----------------|
| 2⁰ | 1 | - | /32 |
| 2¹ | 2 | 128 | /31 |
| 2² | 4 | 192 | /30 |
| 2³ | 8 | 224 | /29 |
| 2⁴ | 16 | 240 | /28 |
| 2⁵ | 32 | 224 | /27 |
| 2⁶ | 64 | 192 | /26 |
| 2⁷ | 128 | 128 | /25 |
| 2⁸ | 256 | 0 | /24 |

### IPv4 Subnet Calculation Formula

- **Network Address:** First address in the subnet (all host bits = 0)
- **Broadcast Address:** Last address in the subnet (all host bits = 1)
- **First Usable Host:** Network Address + 1
- **Last Usable Host:** Broadcast Address - 1
- **Total Hosts:** 2^(host bits)
- **Usable Hosts:** 2^(host bits) - 2 (minus network and broadcast addresses)
- **Number of Subnets:** 2^(borrowed bits)

**Exception:** /31 networks have 2 usable hosts (no network or broadcast address reserved) and /32 represents a single host.

---

## Common Subnetting Scenarios

### Home/Small Office

| Network Type | IPv4 Example | IPv6 Example | Typical Size |
|:-------------|:-------------|:-------------|:-------------|
| Home Network | 192.168.1.0/24 | 2001:db8:1::/64 | /24 or /64 |
| Small Office | 192.168.0.0/23 | 2001:db8::/56 | /23 to /22 or /56 |

### Enterprise Networks

| Network Type | IPv4 Example | IPv6 Example | Typical Size |
|:-------------|:-------------|:-------------|:-------------|
| Point-to-Point Link | 10.0.0.0/30 | 2001:db8:1::/127 | /30 or /127 |
| VLAN | 10.1.10.0/24 | 2001:db8:1:10::/64 | /24 or /64 |
| Data Center | 10.0.0.0/16 | 2001:db8::/48 | /16 to /12 or /48 |
| Campus | 10.0.0.0/8 | 2001:db8::/32 | /8 or /32 |

---

## Binary to Decimal Conversion Table

| Binary | Decimal | Binary | Decimal |
|:-------|:--------|:-------|:--------|
| 00000000 | 0 | 10000000 | 128 |
| 00000001 | 1 | 10000001 | 129 |
| 00000010 | 2 | 11000000 | 192 |
| 00000100 | 4 | 11100000 | 224 |
| 00001000 | 8 | 11110000 | 240 |
| 00010000 | 16 | 11111000 | 248 |
| 00100000 | 32 | 11111100 | 252 |
| 01000000 | 64 | 11111110 | 254 |
| 01111111 | 127 | 11111111 | 255 |

### Octet Position Values (IPv4)

| Bit Position | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|:-------------|:----|:---|:---|:---|:--|:--|:--|:--|
| **Binary Example** | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| **Decimal Result** | 128 + 64 = **192** |

---

## Hexadecimal Reference (for IPv6)

| Hex | Decimal | Binary | Hex | Decimal | Binary |
|:----|:--------|:-------|:----|:--------|:-------|
| 0 | 0 | 0000 | 8 | 8 | 1000 |
| 1 | 1 | 0001 | 9 | 9 | 1001 |
| 2 | 2 | 0010 | A | 10 | 1010 |
| 3 | 3 | 0011 | B | 11 | 1011 |
| 4 | 4 | 0100 | C | 12 | 1100 |
| 5 | 5 | 0101 | D | 13 | 1101 |
| 6 | 6 | 0110 | E | 14 | 1110 |
| 7 | 7 | 0111 | F | 15 | 1111 |

---

## Key Formulas and Rules

### IPv4 Formulas
```
Total IP Addresses = 2^(32 - prefix length)
Usable Hosts = 2^(32 - prefix length) - 2
Number of Subnets = 2^(borrowed bits)
Subnet Increment = 256 - subnet mask octet value
```

### IPv6 Formulas
```
Total Addresses = 2^(128 - prefix length)
Number of /64 subnets = 2^(64 - prefix length)
```

### IPv6 Address Shortening Rules
1. Leading zeros in each hextet can be omitted
2. Consecutive hextets of all zeros can be replaced with `::`
3. The `::` notation can only be used once per address

**Example:**
```
Full:       2001:0db8:0000:0000:0000:0000:0000:0001
Shortened:  2001:db8::1
```