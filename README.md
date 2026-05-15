<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure</h1>
This project outlines the configuration of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2025 Datacenter

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Deploy the Windows Server virtual machine that will host Active Directory Domain Services (AD DS)
- Step 2: Deploy the Windows Client virtual machine 
- Step 3: Configure Internal Networking
- Step 4: Verify VM and Network Connectivity

<h2>Deployment and Configuration Steps</h2>

---

Step 1: Deploy the Windows Server virtual machine that will host Active Directory Domain Services (AD DS)

---

<p>
<img width="1624" height="971" alt="AD-RG-Creation" src="https://github.com/user-attachments/assets/65dd75bf-fe2f-46c8-8f95-017ffb509897" />
</p>
<p>

- Created an Azure resource group named "Active-Directory-RG" to organize the virtual machines, networking resources, and supporting infrastructure for the lab environment.

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-Server VM Creation 1" src="https://github.com/user-attachments/assets/1fbb4d7c-1c1b-44a9-a453-af3910ba8bd8" />
</p>
<p>

- Configured the Windows Server virtual machine by selecting the "Active-Directory-RG" resource group, deploying it in the US East region, and naming it "Domain-Controller" to be designated to serve as the Active Directory server.

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-Server VM Creation 2" src="https://github.com/user-attachments/assets/ed3d61ef-d970-4c0e-826d-f0ef9ce86986" />
</p>
<p>

- Selected the "Windows Server 2025 Datacenter x64 Gen 2" image, allocated 2 vCPUs and 16 GiB of memory for performance, and configured a local administrator account for remote system access (labuser).

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-Server VM Creation VNet" src="https://github.com/user-attachments/assets/853b1d61-3135-4cfe-a602-87756bce85d1" />
</p>
<p>

- Created a new virtual network named "Active-Directory-VNet" to provide internal network connectivity between the server and client virtual machines.

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-Server VM Creation End" src="https://github.com/user-attachments/assets/5ec8a239-d919-48aa-a45a-ff07a915e5b1" />
</p>
<p>

- Reviewed the virtual machine deployment settings to verify proper configuration before provisioning the Active Directory server environment.

</p>
<br />

---

## Step 2: Deploy Windows Client virtual machine

---

<p>
<img width="1624" height="971" alt="Client-1 VM Creation 1" src="https://github.com/user-attachments/assets/5349c218-8caa-402f-8d53-3bfaecf0cee3" />
</p>
<p>

- Configured a second virtual machine named "Client-1" within the same resource group and region to serve as the client system for Active Directory testing.

</p>
<br />

<p>
<img width="1624" height="974" alt="Client-1 VM Creation 2" src="https://github.com/user-attachments/assets/6d047a0a-30e7-497f-8984-edfea1b39200" />
</p>
<p>

- Configured the client virtual machine using a "Windows Server 2025 Datacenter X64 Gen2" image due to Azure lab availability, allocating 2 vCPUs and 16 GiB of memory and creating a local administrator account for access (labuser).

- Note: A "Windows 11 Pro" image would more closely represent a real end-user workstation, but Windows Server was used due to lab environment availability.

</p>
<br />

<p>
<img width="1624" height="971" alt="Client-1 VM Creation VNet" src="https://github.com/user-attachments/assets/08de72cd-c30e-4d04-ad4f-cac1322516f2" />
</p>
<p>

- Connected the "Client-1" virtual machine to the "Active-Directory-VNet" to enable internal communication with the "Domain-Controller" virtual machine.

</p>
<br />

<p>
<img width="1624" height="971" alt="Client-1 VM Creation End" src="https://github.com/user-attachments/assets/a41a1c94-f3e2-4248-b5db-ae06653c109a" />
</p>
<p>

- Reviewed the client virtual machine configuration settings and successfully deployed the system.

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-RG VM Verify" src="https://github.com/user-attachments/assets/cc8a9675-4c32-4aac-af73-91587b32f0ac" />
</p>
<p>

- Verified that both "Domain-Controller" and "Client-1" virtual machines were successfully deployed within the same Azure resource group "Active-Directory-RG".

</p>
<br />

---

Step 3: Configure Internal Networking

---

<p>
<img width="1624" height="971" alt="Static IP Nav" src="https://github.com/user-attachments/assets/6cd245ae-9e79-45db-ba27-1c9237f1abe6" />
</p>
<p>

- Navigated to the "Domain-Controller" virtual machine network interface settings and internal NIC to configure a static private IP address for reliable internal network communication.

</p>
<br />

<p>
<img width="1624" height="971" alt="Changing to Static" src="https://github.com/user-attachments/assets/bd04379f-40ce-4015-b2cb-af7229e2fb6d" />
</p>
<p>

- Changed the "Domain-Controller" VM private IP configuration from dynamic to static, noting the assignment of "10.0.0.4" to ensure client machines could consistently locate the server.

</p>
<br />

<p>
<img width="1624" height="971" alt="AD-VM RDC Info" src="https://github.com/user-attachments/assets/af5266d1-4eaf-4144-86f5-28bd86cef23e" />
</p>
<p>

- Verified both virtual machines were running and noted the public IP address of the "Domain-Controller" VM to establish a Remote Desktop connection.
  
</p>
<br />

<p>
<img width="1624" height="974" alt="RD-AD Firewall Nav" src="https://github.com/user-attachments/assets/bd3a5c2d-586c-4a1e-b501-db65ac2b720d" />
</p>
<p>

- Connected to the "Domain-Controller" virtual machine using Remote Desktop (Public IP Address: 20.121.114.214, Credentials: labuser) and navigated to "Windows Defender Firewall with Advanced Security" to adjust connectivity settings for lab testing.

</p>
<br />

<p>
<img width="1624" height="974" alt="Turning Firewall Off" src="https://github.com/user-attachments/assets/121249a0-5da2-4386-ba67-21d9a6ce0b72" />
</p>
<p>

- Temporarily disabled Windows Firewall on the domain controller to test internal network connectivity between systems.

- Note: Disabling the firewall state was performed for lab testing only. In production environments, firewall rules would be configured securely rather than disabling the firewall entirely.

</p>
<br />

<p>
<img width="1624" height="974" alt="AD-VM DNS Info" src="https://github.com/user-attachments/assets/45207c0a-1fe8-4b9d-85de-5c055d85c415" />
</p>
<p>

- Noted the "Domain-Controller" VM private IP address (10.0.0.4) for use as the client system’s DNS server.

</p>
<br />

<p>
<img width="1624" height="979" alt="Client-1 DNS Nav" src="https://github.com/user-attachments/assets/2ce43037-9f2a-4281-a457-65037eafd485" />
</p>
<p>

- Navigated to the "Client-1" VM  network interface settings and internal NIC to configure DNS server settings for domain communication.

</p>
<br />

<p>
<img width="1624" height="979" alt="Change DNS" src="https://github.com/user-attachments/assets/31951bb0-25ad-47fe-ad8b-82169245f1d5" />
</p>
<p>

- Configured the "Client-1" virtual machine to use the "Domain-Controller" (10.0.0.4) as its DNS server, allowing domain-related name resolution through the server.

</p>
<br />

<p>
<img width="1624" height="979" alt="Client-VM RD Info" src="https://github.com/user-attachments/assets/9c2d2b2a-e792-4ae5-b21e-367528eb498b" />
</p>
<p>

- Recorded the public IP address of "Client-1" to establish a Remote Desktop connection for client-side testing.

</p>
<br />

<p>
<img width="1624" height="976" alt="Client-1 Ping DNS" src="https://github.com/user-attachments/assets/b976dd03-41cb-4d00-b54a-0bd95f5950e4" />
</p>
<p>

- Connected to Client-1 via Remote Desktop (Public IP Address: 20.121.116.188, Credentials: labuser) and used PowerShell to ping the "Domain-Controller" VM's private IP address: "ping 10.0.0.4", confirming internal network connectivity between systems.

</p>
<br />

<p>
<img width="1624" height="976" alt="Client-1 DNS Verify" src="https://github.com/user-attachments/assets/3a7f897a-696d-4d68-82df-cf400047e131" />
</p>
<p>

- Used "ipconfig /all" in PowerShell to verify the client system was correctly using 10.0.0.4 as its DNS server, confirming successful network configuration.

</p>
<br />

## Skills Developed

### Microsoft Azure Infrastructure Deployment

Gained hands-on experience deploying and managing virtual machines, resource groups, and virtual networking within a Microsoft Azure cloud environment.

### Windows Server Administration

Configured and managed Windows Server environments, including system setup, remote access, and preparation for Active Directory services.

### Active Directory Infrastructure Preparation

Built the foundational infrastructure required to support an Active Directory Domain Services (AD DS) environment, including server and client system preparation.

### Virtual Networking Configuration

Configured Azure virtual networking components to allow internal communication between virtual machines within the same environment.

### Static IP Address Configuration

Configured a static private IP address for the domain controller to ensure reliable network communication and consistent server accessibility for client systems.

### DNS Configuration

Configured client DNS settings to use the domain controller as the primary DNS server, enabling proper domain name resolution and Active Directory communication.

### Remote Desktop Administration

Used Remote Desktop Protocol (RDP) to remotely access and manage Windows-based virtual machines within the Azure environment.

### Network Connectivity Testing and Troubleshooting

Validated internal network communication between systems using tools such as PowerShell, ping, and ipconfig /all to confirm connectivity and DNS configuration.

### Basic Network Security Awareness

Developed awareness of firewall behavior and the role network security settings play in system communication, while understanding the difference between lab testing practices and production security standards.

### Technical Documentation

Documented infrastructure deployment, network configuration, and validation steps using structured technical documentation and screenshots to clearly communicate setup procedures and outcomes.
