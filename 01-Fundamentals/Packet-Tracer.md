# Introduction to Cisco Packet Tracer (CPT)

## Introduction

**Cisco Packet Tracer** is a powerful network simulation program that allows students to experiment with network behavior. Unlike a physical lab, Packet Tracer allows you to see data freeze in time, inspect the contents of a packet, and watch how it moves through the network layers.

It is the primary tool we will use for all **Labs** and **EI Blancs** (Mock Exams).

## Learning Objectives

By the end of this tutorial, you will be able to:

- Navigate the Packet Tracer interface.
- Select and place network devices (Routers, Switches, PCs).
- Connect devices using the correct cabling types.
- Configure basic IP addressing.
- Use **Simulation Mode** to visualize packet flow.

## 1\. The Interface Overview

When you open Packet Tracer, the interface is divided into several key areas:

1.  **The Workspace (Center):** The large white area where you build your network topology.
2.  **Device Selection Box (Bottom Left):** This is where you choose your hardware.
    - **Top Row:** Device Categories (Network Devices, End Devices, Components, Connections).
    - **Bottom Row:** Specific Models (e.g., Router 2911, Switch 2960).
3.  **The Toolbar (Top):** Standard options (Save, Zoom, Undo) and tools like **Delete (X)**, **Inspect (Magnifying Glass)**, and **Add Simple PDU (Envelope)**.
4.  **Real-time / Simulation Toggle (Bottom Right):** The most powerful feature of CPT. It allows you to switch between normal time and "frame-by-frame" analysis.

## 2\. Building Your First Network

We will build a simple **LAN** (Local Area Network) with two PCs connected by a Switch.

### Step 1: Place End Devices

1.  Go to the **Device Selection Box**.
2.  Click on **End Devices** (PC Icon).
3.  Drag and drop two **"PC-PT"** units into the workspace.

### Step 2: Place Network Device

1.  Click on **Network Devices** (Router Icon) -\> select **Switches** (Switch Icon below).
2.  Drag and drop a **"2960"** Switch between the two PCs.

### Step 3: Cabling

1.  Click on the **Connections** icon (Lightning Bolt).
2.  Select the **Copper Straight-Through** cable (Solid Black Line).
    - _Note: We use Straight-Through because we are connecting different types of devices (PC to Switch)._
3.  Click on **PC0** -\> Select `FastEthernet0`.
4.  Click on **Switch0** -\> Select `FastEthernet0/1`.
5.  Repeat for PC1 (connect to `FastEthernet0/2`).

> **Tip:** You will see orange dots on the switch ports. This is Spanning Tree Protocol (STP) checking for loops. Wait 30 seconds, or press the **"Fast Forward Time"** button ( `>>` ) near the bottom left to turn them green immediately.

## 3\. Basic Configuration

Now that the physical layer is ready, we must configure the Logical Layer (Layer 3).

### Configuring PC0

1.  Click on **PC0**.
2.  Go to the **Desktop** tab -\> Click **IP Configuration**.
3.  Enter the following:
    - **IPv4 Address:** `192.168.1.1`
    - **Subnet Mask:** `255.255.255.0`
    - **Default Gateway:** (Leave blank for now, as we have no router).

### Configuring PC1

1.  Click on **PC1**.
2.  Go to the **Desktop** tab -\> Click **IP Configuration**.
3.  Enter the following:
    - **IPv4 Address:** `192.168.1.2`
    - **Subnet Mask:** `255.255.255.0`

## 4\. Verification & Simulation

### Method A: The Simple PING

1.  Click on **PC0**.
2.  Go to the **Desktop** tab -\> Open **Command Prompt**.
3.  Type:
    ```bash
    ping 192.168.1.2
    ```
4.  You should see `Reply from 192.168.1.2: bytes=32 time=1ms...`

### Method B: Simulation Mode (Visualizing Layers)

This is how you truly learn networking.

1.  Click the **Simulation** tab (Bottom Right).
2.  Click the **"Show All/None"** button to uncheck everything, then check **ICMP** (so we only see Ping packets).
3.  Select the **Add Simple PDU** tool (Closed Envelope icon on top toolbar).
4.  Click **PC0** (Source) then **PC1** (Destination).
5.  Press the **Play** button in the Simulation Panel.

**What to observe:**
You will see the envelope move from PC0 to the Switch, then to PC1, and back.
**Click on the envelope** at any point to open the **PDU Information** window. Here you can see the OSI Layers:

- **Layer 2:** Source/Dest MAC addresses.
- **Layer 3:** Source/Dest IP addresses.

## 5\. Common Shortcuts

| Shortcut        | Function         | Description                                         |
| :-------------- | :--------------- | :-------------------------------------------------- |
| **Alt + Click** | **Fast Forward** | Instantly converges the network (skips boot times). |
| **Del**         | **Delete**       | Removes a selected device or cable.                 |
| **Esc**         | **Cancel**       | Exits the current tool (like cabling or delete).    |
| **Ctrl + S**    | **Save**         | Always save your `.pkt` files frequently\!          |
| **R**           | **Reload**       | Reboot a router or switch.                          |
