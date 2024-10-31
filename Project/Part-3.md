# `Part 3` Installing and Configuring Sysmon and Splunk Forwarder

In `Part 3` of the **Active Directory Project**, we’ll install and configure **Sysmon and Splunk Universal Forwarder** to collect and forward telemetry data from our Windows target machine and server to the Splunk server. By the end, both machines will be sending security, system, and application logs to Splunk, preparing our environment for active monitoring and analysis.

### Prerequisites

1. **Splunk Account**  
   Ensure you have a Splunk account and have downloaded the **Splunk Enterprise** DEB package and **Splunk Universal Forwarder**.

2. **Network Configuration**  
   Verify your virtual machines are set to the same NAT Network and have **static IPs** assigned as per your network diagram.

## `Step 1` Configure NAT Network for VMs

1. Open VirtualBox, go to **File > Host Network Manager**.
2. Select **NAT Network** and configure the IP range, using the same prefix as your lab diagram.
3. Apply the network to each VM (Splunk server, target machine, etc.) under **Settings > Network**.

## `Step 2` Set Static IP for Splunk Server

1. On the Splunk VM, set a **static IP** using:
   ```bash
   sudo nano /etc/netplan/00-installer-config.yaml
   ```
2. Specify IP settings matching your diagram, and apply changes with:
   ```bash
   sudo netplan apply
   ```

## `Step 3` Install Splunk Enterprise on the Splunk Server

1. **Transfer the DEB package** to the Splunk VM and install:
   ```bash
   sudo dpkg -i splunk-package.deb
   ```
2. Set up **admin credentials** and configure Splunk to auto-start.

## `Step 4` Install Sysmon on Windows Target Machine

1. Download **Sysmon** and **Sysmon configuration file** (e.g., from [Olaf Hartong’s GitHub](https://github.com/olafhartong/sysmon-modular)).
2. Open PowerShell with admin privileges, navigate to the Sysmon executable location, and run:
   ```powershell
   .\sysmon.exe -accepteula -i sysmonconfig.xml
   ```

## `Step 5` Install and Configure Splunk Universal Forwarder

1. Install **Splunk Universal Forwarder** on the Windows target machine.
2. Configure the `inputs.conf` file under:
   ```
   C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
   ```
3. Specify the IP and port of the Splunk server (e.g., `9997` for forwarding logs) and save.

4. Restart the **Splunk Forwarder** service.

---

## Conclusion

By completing Part 3, you now have:

- **Sysmon and Splunk Forwarder** installed on your Windows machines
- **Telemetry Collection** configured to gather logs for security, system, and application events
- **Splunk Server** receiving and indexing logs from each configured machine

In **Part 4**, we’ll dive into installing and configuring **Active Directory** to establish our domain environment.