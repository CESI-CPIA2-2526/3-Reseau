# The OSI Model (Open Systems Interconnection)

## Introduction

The **OSI (Open Systems Interconnection) Model** is a conceptual framework used to describe the functions of a networking system. It divides network communication into seven distinct layers. It was introduced in 1984 by the International Organization for Standardization (**ISO**).

While modern networks run on the **TCP/IP** model, the OSI model remains the universal reference for teaching and troubleshooting network logic.

## Learning Objectives

By the end of this module, you will be able to:

- Describe the seven layers of the OSI model.
- Explain the specific functions and services of each layer.
- Identify the protocols (e.g., IP, TCP, HTTP) and hardware devices (e.g., Routers, Switches) associated with each layer.
- Understand the concept of **Encapsulation**.

## The Seven Layers of the OSI Model

The model is divided into seven layers, numbered 1 through 7, from the bottom (physical hardware) up to the top (software applications). Each layer provides services to the layer directly above it and consumes services from the layer directly below it.

> **Mnemonic to remember the order (Top to Bottom):** > **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
> (Application, Presentation, Session, Transport, Network, Data Link, Physical)

### 1. Physical Layer (Layer 1)

- **PDU (Unit of Data):** Bits
- **Key Function:** Transmission of raw bit streams.

The Physical layer is the lowest layer. It is responsible for the actual physical connection between devices. It defines the hardware elements including:

- **Electrical/Mechanical specifications:** Voltage levels, timing of voltage changes, physical data rates.
- **Physical Topology:** How devices are physically arranged (Bus, Star, Ring).

**Hardware:** Cables (Ethernet, Fiber), Hubs, Repeaters, Network Interface Cards (NICs), Modems.

### 2. Data Link Layer (Layer 2)

- **PDU (Unit of Data):** Frame
- **Key Function:** Node-to-node transfer and error detection.

This layer ensures data transfer between two directly connected nodes. It is responsible for:

- **Physical Addressing:** Using **MAC Addresses** (Media Access Control) to identify devices on the same network segment.
- **Error Detection:** Adding a trailer (FCS) to frames to check if data was corrupted during transmission.
- **Flow Control:** Managing the speed of data transmission between nodes.

**Hardware:** Switches, Bridges.
**Protocols:** Ethernet, 802.11 (Wi-Fi), PPP, STP.

### 3. Network Layer (Layer 3)

- **PDU (Unit of Data):** Packet
- **Key Function:** Routing and Logical Addressing.

The Network layer is responsible for receiving frames from the Data Link layer and delivering them to their intended destinations based on logical addresses.

- **Logical Addressing:** Assigning **IP Addresses** (IPv4, IPv6) to devices.
- **Routing:** Determining the best path for data to travel across different networks (internetworking).

**Hardware:** Routers, Layer 3 Switches.
**Protocols:** IPv4, IPv6, ICMP, OSPF, BGP.

### 4. Transport Layer (Layer 4)

- **PDU (Unit of Data):** Segment (TCP) or Datagram (UDP)
- **Key Function:** End-to-end communication and reliability.

This layer coordinates data transfer between systems and hosts. It ensures that data is transferred completely and correctly (depending on the protocol used).

- **Segmentation:** Breaking large data chunks into smaller segments.
- **Port Addressing:** Identifying the specific service or application (e.g., Port 80 for Web, Port 25 for Email).
- **Protocols:**
  - **TCP (Transmission Control Protocol):** Reliable, connection-oriented (guarantees delivery).
  - **UDP (User Datagram Protocol):** Unreliable, connectionless (faster, used for streaming).

**Hardware:** Firewalls, Load Balancers.

### 5. Session Layer (Layer 5)

- **Key Function:** Session management.

The Session layer controls the dialogues (connections) between computers. It establishes, manages, and terminates the connections between the local and remote application.

- **Synchronization:** It can insert checkpoints into the data stream. If the connection fails, only the data after the last checkpoint needs to be re-transmitted.

**Protocols:** NetBIOS, RPC, PPTP.

### 6. Presentation Layer (Layer 6)

- **Key Function:** Data translation and formatting.

This layer ensures that the data sent from the application layer of one system can be read by the application layer of another system. It acts as the translator of the network.

- **Translation:** Converting data formats (e.g., EBCDIC to ASCII).
- **Encryption/Decryption:** Securing data (e.g., SSL/TLS happens here and at Layer 4).
- **Compression:** Reducing the size of files to be transmitted.

**Formats:** JPEG, GIF, MPEG, ASCII.

### 7. Application Layer (Layer 7)

- **Key Function:** Network services for applications.

This is the layer that the end-user interacts with directly. However, it is not the application itself (like the Chrome browser), but the protocols the application uses to communicate.

- It provides services for file transfers, email, and other network software services.

**Protocols:** HTTP/HTTPS (Web), SMTP (Email), FTP (File Transfer), DNS (Domain Name System), SSH, Telnet.

## Summary Table

| Layer # | Layer Name       | PDU (Data Unit)  | Core Function                       | Examples / Protocols      |
| :------ | :--------------- | :--------------- | :---------------------------------- | :------------------------ |
| **7**   | **Application**  | Data             | User interaction & Network Services | HTTP, DNS, SMTP           |
| **6**   | **Presentation** | Data             | Formatting, Encryption, Compression | JPEG, ASCII, SSL          |
| **5**   | **Session**      | Data             | Session control & Synchronization   | NetBIOS, RPC              |
| **4**   | **Transport**    | Segment/Datagram | End-to-end reliability & Ports      | TCP, UDP, Ports (80, 443) |
| **3**   | **Network**      | Packet           | Routing & Logical Addressing        | IP, ICMP, Routers         |
| **2**   | **Data Link**    | Frame            | Physical Addressing & Switching     | Ethernet, MAC, Switches   |
| **1**   | **Physical**     | Bit              | Binary Transmission & Signaling     | Cables, Hubs, Wi-Fi Radio |
