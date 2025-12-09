# TCP (Transmission Control Protocol)

## Introduction

**TCP (Transmission Control Protocol)** is a Layer 4 (Transport Layer) protocol in the OSI model. It operates on top of the IP (Internet Protocol) to ensure data is transported reliably across a network.

Unlike **UDP** (User Datagram Protocol), which is faster but unreliable, TCP prioritizes accuracy and order. It is the backbone of the modern internet, used by applications where data loss is unacceptable (like web browsing or email).

## Learning Objectives

By the end of this module, you will be able to:

- Describe the key characteristics of TCP (Reliability, Flow Control).
- Analyze the fields of the TCP Header.
- Explain the **Three-Way Handshake** (Connection Establishment).
- Identify common applications that rely on TCP.

## Key Characteristics

1.  **Connection-Oriented:** Before data is sent, a logical connection must be established between the sender and receiver.
2.  **Reliable Delivery:** TCP guarantees that data sent is received. If data is lost, it is retransmitted.
3.  **Ordered Data Transfer:** TCP uses **Sequence Numbers** to ensure packets are reassembled in the correct order, even if they arrive out of order.
4.  **Flow Control:** Using the **Window Size**, TCP manages the data rate so the sender does not overwhelm the receiver.
5.  **Congestion Control:** TCP detects network congestion and slows down transmission to prevent packet loss.
6.  **Full Duplex:** Data can flow in both directions simultaneously once the connection is established.

## TCP Header Format

TCP encapsulates data into **Segments**. Each segment has a header containing control information.


### Header Fields Breakdown

| Field                           | Size     | Description                                                                                                                           |
| :------------------------------ | :------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **Source Port**                 | 16 bits  | The port number of the sender.                                                                                                        |
| **Destination Port**            | 16 bits  | The port number of the receiver.                                                                                                      |
| **Sequence Number**             | 32 bits  | If the SYN flag is set, this is the initial sequence number. Otherwise, it is the accumulated sequence number of the first data byte. |
| **Acknowledgment Number**       | 32 bits  | The value of the _next_ sequence number the sender is expecting to receive.                                                           |
| **Header Length (Data Offset)** | 4 bits   | The size of the TCP header (in 32-bit words). Indicates where the data begins.                                                        |
| **Reserved**                    | 3 bits   | For future use (must be zero).                                                                                                        |
| **Control Flags**               | 9 bits   | (See detailed flags below).                                                                                                           |
| **Window Size**                 | 16 bits  | The number of bytes the sender is willing to accept (Flow Control).                                                                   |
| **Checksum**                    | 16 bits  | Used for error-checking the header and data.                                                                                          |
| **Urgent Pointer**              | 16 bits  | Indicates the end of urgent data (if URG flag is set).                                                                                |
| **Options**                     | Variable | Optional settings (e.g., Maximum Segment Size).                                                                                       |

### TCP Flags (Control Bits)

The flags indicate the state or specific function of the segment.

- **SYN (Synchronize):** Used to initiate a connection.
- **ACK (Acknowledgment):** Confirms receipt of data. All packets after the initial SYN have this flag set.
- **FIN (Finish):** Request to terminate the connection gracefully.
- **RST (Reset):** Abruptly resets a connection (usually due to an error).
- **PSH (Push):** Tells the receiver to pass the data to the application immediately (don't buffer it).
- **URG (Urgent):** Indicates the data contained is urgent.
- **ECE (ECN-Echo):** Indicates the network is congested (Explicit Congestion Notification).
- **CWR (Congestion Window Reduced):** Confirmation that the sender reduced its sending rate.

## How TCP Works

### 1. Encapsulation Process

When an application sends data:

1.  **Transport Layer:** TCP adds the TCP Header (creating a **Segment**).
2.  **Network Layer:** IP adds the IP Header (creating a **Packet**).
3.  **Data Link Layer:** Ethernet adds the MAC Header/Trailer (creating a **Frame**).
4.  **Physical Layer:** The frame is converted to bits and transmitted.

### 2. Connection Establishment (The Three-Way Handshake)

Before data transfer, the client and server must sync.

1.  **SYN:** The Client sends a segment with `SYN=1` and a random Sequence Number (Seq=x).
2.  **SYN-ACK:** The Server receives it, sends back `SYN=1`, `ACK=1`. It Acknowledges the client (Ack=x+1) and generates its own Sequence Number (Seq=y).
3.  **ACK:** The Client receives the SYN-ACK and sends a final `ACK=1` (Ack=y+1). The connection is now **ESTABLISHED**.

### 3. Data Transfer & Termination

- **Data Transfer:** Uses Sequence and Acknowledgment numbers to track bytes.
- **Termination:** Uses a four-step process involving **FIN** and **ACK** flags to close the connection from both sides.

## Common Applications

Because of its reliability, TCP is used for protocols where data integrity is critical:

- **Web Browsing:** HTTP (Port 80), HTTPS (Port 443)
- **File Transfer:** FTP (Port 20/21)
- **Email:** SMTP (Port 25), IMAP (Port 143)
- **Remote Access:** SSH (Port 22), Telnet (Port 23)
