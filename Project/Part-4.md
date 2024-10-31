# `Part 4` Active Directory Setup and Domain Configuration

In `Part 4` of the **Active Directory Project**, we’ll install Active Directory on the server, promote it to a domain controller, and add our Windows target machine to the new domain. By the end, your lab will have a functional Active Directory domain and user accounts ready for access.

### Prerequisites

1. **Previous Setup**  
   Ensure your lab network, Splunk configuration, and Sysmon installations from previous parts are completed.
2. **Admin Privileges**  
   Access to the server as an administrator is required.

## `Step 1` Set Static IP on Server

1. On the server, right-click the **Network Icon** and select **Open Network & Internet Settings**.
2. Under **Change Adapter Options**, right-click your adapter > **Properties**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** and set:
   - **IP Address**: `192.168.10.7`
   - **Subnet Mask**: `255.255.255.0`
   - **Default Gateway**: `192.168.10.1`
   - **DNS Server**: `8.8.8.8` (or your preferred DNS)

4. Open Command Prompt, type `ipconfig`, and confirm the IP settings.

## `Step 2` Install Active Directory Domain Services (AD DS)

1. Open **Server Manager** and click on **Manage > Add Roles and Features**.
2. Select **Role-based or feature-based installation** and **Active Directory Domain Services**.
3. Click **Add Features** when prompted, then proceed with **Next** until you reach **Install**.
4. Allow the installation to complete. 

## `Step 3` Promote the Server to Domain Controller

1. In **Server Manager**, click the **Flag Icon** > **Promote this server to a domain controller**.
2. Select **Add a new forest** and set the **Domain Name** (e.g., `mydfir.local`).
3. Enter a strong **password** for recovery and proceed with the default options.
4. Click **Next** to continue through the wizard, then select **Install**. The server will restart once the setup completes.

## `Step 4` Create Organizational Units and Users

1. After logging back in, open **Active Directory Users and Computers** under **Tools** in **Server Manager**.
2. Right-click on the domain (e.g., `mydfir.local`) > **New > Organizational Unit** and create OUs, like **IT** and **HR**.
3. For each OU, right-click > **New > User** to create users (e.g., **Jenny Smith** in IT, **Terry Smith** in HR).
   - Assign usernames (e.g., `jsmith`) and a password.
   - Uncheck **User must change password at next logon** for simplicity.

## `Step 5` Join the Windows Target Machine to the Domain

1. On the target machine, go to **System Properties**:
   - Right-click **This PC** > **Properties** > **Advanced System Settings** > **Computer Name** > **Change**.
2. Select **Domain** and enter your domain name (e.g., `mydfir.local`).
3. If a DNS error occurs, set the **DNS Server** on the target machine to point to the server IP (e.g., `192.168.10.7`).
4. Enter the **Administrator credentials** for the server when prompted.
5. Restart the machine, then log in with a domain user account (e.g., `jsmith`).

## Conclusion

By completing Part 4, you now have:

- **Active Directory Domain** with a domain controller.
- **Organizational Units and Users** configured in Active Directory.
- **Windows Target Machine** joined to the domain and ready for domain user access.

In **Part 5**, we’ll perform security testing by running a brute-force attack from Kali Linux and configuring Atomic Red Team on the target machine to generate logs for analysis in Splunk.
