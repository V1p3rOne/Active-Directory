# `Part 5` Brute Force Attack and Telemetry with Atomic Red Team

In `Part 5` of the **Active Directory Project**, you will simulate an attack using **Kali Linux** to perform a brute force attack, then install and configure **Atomic Red Team** to generate telemetry on your Windows target machine. By the end, you’ll understand how to detect these attacks using Splunk, refining your skills in cybersecurity monitoring.

### Prerequisites

1. **Kali Linux VM**  
   Make sure Kali Linux is set up and connected to your lab network.
2. **Splunk and Sysmon**  
   Installed and configured on the target and Active Directory machines.

---

## `Step 1` Set a Static IP on Kali Linux

1. Open **Network Connections** on Kali Linux and edit the wired connection.
2. Set IP configuration to **Manual** and assign:
   - **IP Address**: `192.168.1.2`
   - **Netmask**: `255.255.255.0`
   - **Gateway**: `192.168.1.1`
   - **DNS Server**: `8.8.8.8`
3. Save the settings, disconnect, and reconnect to apply changes.

## `Step 2` Install Crowbar for Brute Force Attack

1. Install **Crowbar**, a brute force tool:
   ```bash
   sudo apt-get install crowbar -y
   ```
2. Navigate to the **rockyou** wordlist:
   ```bash
   cd /usr/share/wordlists/
   sudo gunzip rockyou.txt.gz
   ```
3. Copy the **rockyou.txt** file to a new project directory:
   ```bash
   mkdir ~/ad-project
   cp rockyou.txt ~/ad-project/passwords.txt
   ```

## `Step 3` Enable Remote Desktop on Target Machine

1. On your Windows target machine, go to **This PC > Properties > Advanced System Settings**.
2. Enable **Allow remote connections** and add **Jenny Smith** and **Terry Smith** as remote users.
3. Confirm settings to allow RDP access for your attack simulation.

## `Step 4` Run Crowbar Brute Force Attack

1. On Kali Linux, enter the following Crowbar command to start a brute force attack on RDP:
   ```bash
   crowbar -b rdp -u TSmith -C ~/ad-project/passwords.txt -s 192.168.1.10/32
   ```
2. This command will try each password in `passwords.txt` against the **TSmith** user on the Windows target machine, simulating a brute force attempt.

## `Step 5` Analyze Brute Force Activity in Splunk

1. Open Splunk, navigate to **Search & Reporting**, and search for recent failed logon events.
2. Search using:
   ```spl
   index="endpoint" "T Smith" 
   ```
3. Look for **Event Code 4625** (failed logons) and **Event Code 4624** (successful logon) to analyze brute force indicators.

## `Step 6` Install and Configure Atomic Red Team

1. Open PowerShell as an administrator on the Windows target machine.
2. Run the following to bypass execution policy and download Atomic Red Team:
   ```powershell
   Set-ExecutionPolicy Bypass -Scope CurrentUser
   iwr -Uri https://path-to-atomic-red-team -OutFile C:\AtomicRedTeam.zip
   Expand-Archive -Path C:\AtomicRedTeam.zip -DestinationPath C:\AtomicRedTeam
   ```

### Exclude Atomic Red Team from Windows Defender
1. Open **Windows Security > Virus & Threat Protection > Manage Settings**.
2. Add an exclusion for the **C:\AtomicRedTeam** folder to prevent Defender from blocking tests.

## `Step 7` Run Atomic Red Team Tests and Verify in Splunk

1. Use PowerShell to initiate a specific test (e.g., create a new user):
   ```powershell
   Invoke-AtomicTest T1116
   ```
2. Go to Splunk and search for telemetry data related to this activity:
   ```spl
   index="endpoint" "T1116"
   ```

## Conclusion

By completing Part 5, you should now have:

- **Experience with Brute Force Attacks** using Crowbar on Kali Linux.
- **Atomic Red Team Configured** on the target machine to simulate attacks.
- **Telemetry Analysis in Splunk** to detect and monitor security events.

This final part of the Active Directory Project has equipped you with hands-on skills in monitoring, detecting, and analyzing threats within an Active Directory environment.