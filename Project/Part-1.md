# `Part 1` Project Overview and Diagram Design

In `Part 1` of the **Active Directory Project**, we’re laying the groundwork by designing a **network diagram** for our lab environment. This setup will prepare us for installing Active Directory, Splunk, and Windows machines in later parts. By the end of this section, you'll have a clear, organized diagram representing how all components in our lab will connect and interact.

### Project Goals

1. **Learn to install and configure** an on-premises domain environment.
2. **Gain practical experience** with Active Directory, Splunk, and networked Windows clients.
3. **Develop a visual representation** of network data flow and relationships for interview readiness.

---

## `Step 1` Setting Up the Diagram

### Prerequisites

1. **Hardware Requirements**  
   - At least **16 GB RAM** and **250 GB disk space** recommended.
   - If using an M1/M2 Mac, consider a cloud provider like **Vultr** or **Azure** as VirtualBox may be unsupported.

2. **Diagram Tool**  
   - Use [Draw.io](https://www.draw.io) to create the network diagram for this lab setup.

### Diagram Components

- **Active Directory Server**  
  - IP: `192.168.10.0`  
  - Includes **Sysmon** and **Splunk Universal Forwarder** for data collection.

- **Splunk Server**  
  - IP: `192.168.10.10`  
  - Receives telemetry data from the network.

- **Target Machine**  
  - Windows 10 (DHCP assigned IP)  
  - Configured with **Sysmon**, **Splunk Universal Forwarder**, and **Atomic Red Team** for simulated attack testing.

- **Attacker Machine**  
  - Kali Linux (Static IP: `192.168.1.2`)  
  - Used for brute force and penetration testing activities.

---

## `Step 2` Building the Diagram in Draw.io

1. **Add Icons**  
   - Use icons for **servers**, **computers**, **router**, and **switch** to represent each component in the lab.

2. **Arrange Connections**  
   - Connect each component to the **switch**, and the switch to the **router**.
   - Add a **cloud icon** to represent internet connectivity.

3. **Annotate Components**  
   - Label each component with its role (e.g., “Active Directory Server”) and its IP address for clarity.
   - Use **dotted green lines** to represent data flows, especially where logs are forwarded to Splunk.

### Finalize and Save

Once all connections and annotations are complete, save the diagram to refer to as we move forward.

---

## Conclusion

In Part 1, we established:

- **A detailed network diagram** with all required components.
- **IP assignments and roles** for each component in the lab environment.

In **Part 2**, we’ll move on to installing VirtualBox and setting up each virtual machine to build out our lab infrastructure.
