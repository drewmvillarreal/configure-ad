<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2025 Datacenter: Azure Edition - x64 Gen 2
- Windows 11 Pro (25H2)

<h2>High-Level Deployment and Configuration Steps</h2>

Setup Domain Controller in Azure
—
Create a Resource Group
Create a Virtual Network and Subnet
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Username: labuser
Password: Cyberlab123!
After VM is created, set Domain Controller’s NIC Private IP address to be static
Log into the VM and disable the Windows Firewall (for testing connectivity)

Setup Client-1 in Azure
—
Create the Client VM (Windows 10) named “Client-1”
Username: labuser
Password: Cyberlab123!
Attach it to the same region and Virtual Network as DC-1
After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address
From the Azure Portal, restart Client-1
Login to Client-1
Attempt to ping DC-1’s private IP address
Ensure the ping succeeded
From Client-1, open PowerShell and run ipconfig /all
The output for the DNS settings should show DC-1’s private IP Address


<h2>Deployment and Configuration Steps</h2>


<p>
1. Create a Resource Group within Azure (portal.azure.com)
</p>

<img width="755" height="328" alt="image" src="https://github.com/user-attachments/assets/b7d35f3a-1a2f-4d10-b6b3-ca61800b5919" />
<br />


<p>
2. Create a Virtual Network and Subnet
</p>

<img width="773" height="655" alt="image" src="https://github.com/user-attachments/assets/0a40936d-cd22-4273-a2f1-5f7c3dd4acbb" />

<br />




<p>
3. Create a new Domain Controller VM (Windows Server 2025 Datacenter: Azure Edition - x64 Gen 2), and name it DC-1.
  
  - Be sure to place it in the same resource group created earlier, and within the same region (I did (US) East US 2).

<img width="718" height="633" alt="image" src="https://github.com/user-attachments/assets/c17c0c64-7589-4b53-bd2a-4a0c29887709" />

<img width="736" height="610" alt="image" src="https://github.com/user-attachments/assets/1426e2b9-e325-40f3-9be9-1e35ddd11913" />

  
</p>
<br />


<p>
4. Create a new username and password for the virtual machine.
  
  - Username: labuser
    
  - Password: Password123!

  - Note: You will need to check both licensing prompts before clicking Review + Create and creating the virtual machine. 
</p>
<br />

<img width="710" height="144" alt="image" src="https://github.com/user-attachments/assets/5c493ad6-1d7a-4434-9535-216aa5da473f" />



<p>
5. Create a new virtual machine (Windows 11 Pro(25H2) named Client-1
</p>
<br />

<img width="729" height="549" alt="image" src="https://github.com/user-attachments/assets/a46ae4c4-9665-4266-8550-02cfe28fb274" />

<img width="732" height="492" alt="image" src="https://github.com/user-attachments/assets/1cc81564-b89c-4eec-9cc8-d69d55f3589a" />

- Username: labuser
- Password: Password123!
- Check the licensing prompt, then click Review + create

<img width="729" height="660" alt="image" src="https://github.com/user-attachments/assets/7b645c2d-f5f2-40d3-825e-c7ae87fcf9bb" />



<p>
6. Now that both VMs have been created, set the Domain Controller's NIC Private IP address to be static by going to the VM -> Network settings -> Network interface/IP configuration -> click on ipconfig1 -> select Static under Private IP address settings -> click Save
</p>

<img width="913" height="591" alt="image" src="https://github.com/user-attachments/assets/0ed4ae80-9b98-4390-aaa0-269f7af30c0a" />

<img width="1063" height="621" alt="image" src="https://github.com/user-attachments/assets/ebf29abd-7a27-4218-924f-5ebae542500d" />

<img width="574" height="620" alt="image" src="https://github.com/user-attachments/assets/40ef28d4-018c-472b-822e-dd76f05d8920" />



<br />




<p>
7. For this next part, you will need the public IP address for DC-1 so you can remote in using Remote Desktop Connection.
  Once logged in to the Domain Controller, you will want to disable the Windows Firewall for testing connectivity. 
  
  - Click the Windows icon and type WF for windows firewall
  - In Windows Defender Firewall, click Windows Defender Firewall Properties
  - Now turn off the firewall in Domain Profile, Private Profile, and Public Profile
</p>
<img width="1140" height="439" alt="image" src="https://github.com/user-attachments/assets/8019db8c-5389-4566-b6bf-5769bffa6227" />

<img width="400" height="240" alt="image" src="https://github.com/user-attachments/assets/88c63712-7e4b-44ea-8477-9103afade326" />

<img width="585" height="584" alt="image" src="https://github.com/user-attachments/assets/038ac7ea-d45c-4f1d-acf7-75ae7f721940" />


<p><img width="286" height="326" alt="image" src="https://github.com/user-attachments/assets/58210cbf-79a9-46c6-87ed-90b761f57894" /></p>


<p><img width="286" height="326" alt="image" src="https://github.com/user-attachments/assets/b9ed52d3-b574-4ad6-94fd-30dacbf7418a" /></p>


<p><img width="281" height="327" alt="image" src="https://github.com/user-attachments/assets/f1b4dda6-f0f5-4092-899c-b083387b6285" /></p>

<br />



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
