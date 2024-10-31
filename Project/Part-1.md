# `Part 1` Project Setup and Diagram Design

## Diagram and Mapping

Start by creating a network diagram to understand how data flows through your network and how components are connected. This visual guide will also be useful in interviews where you may need to illustrate a lab setup.

### Tools and Virtualization Requirements

- **Diagram Tool**<br>[Draw.io](https://www.draw.io) – a free, accessible tool for creating and arranging network diagrams.
- **Hardware**
  - **Recommended**<br>At least **16 GB RAM** and **250 GB disk space**.
  - **Virtualization Options**
    - **Mac Users (M1/M2/M3)**<br>Consider cloud-based solutions such as **Vulture** or **Azure**.
    - **Windows Users**<br>**VirtualBox** for local virtualization.

## Diagram Components and Configuration

Each component in the network serves a distinct role. Here’s a breakdown of what to include in your diagram:

1. **Servers**:
   - **Active Directory Server**: Handles directory services.
   - **Splunk Server**: Receives and processes data logs from network components.

2. **Client Machines**:
   - **Target Machine**: A **Windows 10** machine configured with:
     - **Splunk Universal Forwarder**: For data forwarding.
     - **Sysmon**: Collects telemetry.
   - **Attacker Machine**: A **Kali Linux** machine (distinguished in red on the diagram for easy identification).

3. **Additional Network Components**:
   - **Switch**: Connects various devices.
   - **Router**: Manages data traffic between networked components and the internet.

### Network Information Setup

Assign IP addresses to ensure seamless connectivity:

- **Domain Name**: `mydfir.local`
- **Splunk Server IP**: `192.168.10.10`
- **Active Directory Server IP**: `192.168.10.0`
- **Attacker Machine IP**: `192.168.1.2`
  
---

## Assembling the Diagram

Follow these steps to build the diagram in Draw.io:

1. **Add Components**:
   - **Servers**: Search for "server" in shapes, then drag two icons onto the canvas.
   - **Client Machines**: Search for "computer" and drag two icons.
   - **Network Devices**: Search for "switch," "router," and "cloud" to represent network connections.

2. **Configure and Customize**:
   - Label each component (e.g., **Splunk Server** and **Active Directory**).
   - Set the **Attacker Machine** color to red for easy differentiation.

3. **Connect Components**:
   - Use **arrows** to show data flow, starting from **servers** to **network devices** and **client machines**.
   - Adjust lines to ensure clean, straight connections for readability.

4. **Network Information**:
   - Add a text box to label the network, including IPs and roles for each component.

---

## Telemetry and Data Flow

In this setup, logs are forwarded to Splunk for monitoring and analysis.

1. **Data Flow Indicators**:
   - Use **dotted lines** in green to represent telemetry data flowing from:
     - **Active Directory Server** → **Splunk**
     - **Target Machine** → **Splunk**
   - **Optional Additions**:
     - Intrusion Detection Systems (IDS)
     - Endpoint Detection and Response (EDR)
     - Firewalls

2. **Log Forwarding**:
   - **Sysmon** on Active Directory and Target Machine collects telemetry.
   - **Splunk Universal Forwarder** on each machine ensures logs are sent to Splunk.

---

## Conclusion and Next Steps

With the diagram complete, you now have a clear view of the lab environment structure. This setup will be referenced throughout the project. 

### Upcoming in Part 2
In the next video, you’ll move forward with:

- **Installing all components on VirtualBox** to finalize the setup and prepare for further configuration.

Stay curious and prepare for an exciting lab-building experience!

---

