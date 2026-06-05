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

- Setup Domain Controller and Client-1 in Azure
- Configure DNS
- Install Active Directory Domain Services
- Bulk user provisioning via PowerShell



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

<p><img width="1140" height="439" alt="image" src="https://github.com/user-attachments/assets/8019db8c-5389-4566-b6bf-5769bffa6227" /></p>


<p><img width="400" height="240" alt="image" src="https://github.com/user-attachments/assets/88c63712-7e4b-44ea-8477-9103afade326" /></p>


<p><img width="585" height="584" alt="image" src="https://github.com/user-attachments/assets/038ac7ea-d45c-4f1d-acf7-75ae7f721940" /></p>


<p><img width="286" height="326" alt="image" src="https://github.com/user-attachments/assets/58210cbf-79a9-46c6-87ed-90b761f57894" /></p>


<p><img width="286" height="326" alt="image" src="https://github.com/user-attachments/assets/b9ed52d3-b574-4ad6-94fd-30dacbf7418a" /></p>


<p><img width="281" height="327" alt="image" src="https://github.com/user-attachments/assets/f1b4dda6-f0f5-4092-899c-b083387b6285" /></p>

<br />

<p>
8. Now we will set the Client-1 VM's DNS settings to the DC-1 VM's Private IP address.

  - In Azure, go to the Client-1 VM
  - Click on network settings
  - Click on Network interface/IP configuration
  - Click on DNS server and click Custom
  - Enter the Private IP address from the DC-1 VM 
</p>
<br />

<img width="1134" height="593" alt="image" src="https://github.com/user-attachments/assets/1efc22e4-7c50-4b3e-84a2-e94a73ebd979" />

<img width="679" height="478" alt="image" src="https://github.com/user-attachments/assets/dff5d655-acef-45f5-9ab9-556a8a02189c" />



<p>
9. Use Remote Desktop Connection to log in to the Client-1 VM, and attempt to ping the DC-1 Domain Controller's private IP address (10.0.0.4). 
  
  - Log in to the Client-1 VM
  - Open Powershell
  - Ping 10.0.0.4

<img width="396" height="394" alt="image" src="https://github.com/user-attachments/assets/1369bef4-1c1d-49a2-963c-5661e0389549" />

<p><img width="412" height="202" alt="image" src="https://github.com/user-attachments/assets/ba90a074-4ef3-4b17-88b3-7c90ab21f0b5" /></p>

  
</p>
<br />


<p>
10. To check that the DNS settings have been applied correctly, run ipconfig /all in Powershell. This should show you the Private IP address for DC-1. 
</p>

<img width="380" height="332" alt="image" src="https://github.com/user-attachments/assets/b2b3f7d0-8484-4196-b84d-1bbbbbac1201" />


<br />

<p>
11. On DC-1, install Active Directory Domain Services. 
  
-  Click on start, then Server Manager.
-  Add roles and features
-  Click next on all the rest of the pages of the Add Roles and Features Wizard, then click install.


  <img width="540" height="664" alt="image" src="https://github.com/user-attachments/assets/5a6df0fa-e2de-47e4-8a5f-d6384143969c" />
  <img width="1205" height="631" alt="image" src="https://github.com/user-attachments/assets/b2ffe0a9-074c-442a-a308-d23a76ca7665" />
  <img width="661" height="473" alt="image" src="https://github.com/user-attachments/assets/1a3f3a2e-4311-42e2-8161-3530c50bbff3" />
  <img width="663" height="486" alt="image" src="https://github.com/user-attachments/assets/ae82c942-6e01-4d2a-bf45-371506ce7b9a" />
  <img width="663" height="470" alt="image" src="https://github.com/user-attachments/assets/dca829a2-db90-4a12-9380-2c885e1aee4b" />
  <img width="658" height="473" alt="image" src="https://github.com/user-attachments/assets/97f1d43b-a31c-4cc8-b8de-044d53737d40" />
  <img width="351" height="370" alt="image" src="https://github.com/user-attachments/assets/7de31099-c831-4112-96f5-af99b93b3bbf" />
  <img width="658" height="468" alt="image" src="https://github.com/user-attachments/assets/c2088298-bdd2-4ebb-ac71-3e5c8c6994b9" />

</p>
<br />

<p>
12. Promote DC-1 into an actual Domain controller. 

  - On Server Manager, click on the flag icon and promote this server to a domain controller.
  - Click on Add a new forest and enter "mydomain.com"
  - Create a new password
  - Click next on the following pages of the configuration wizard and install (this will restart DC-1)
  - Log back in to DC-1, but this time you will need to click on more options and use a different account. The username will now be "mydomain.com\labuser"

<img width="1196" height="626" alt="image" src="https://github.com/user-attachments/assets/e8cd673a-d577-48a5-ab9f-ce4e6144b317" />
<img width="639" height="472" alt="image" src="https://github.com/user-attachments/assets/29fe254e-1e80-4afa-86e2-5687967338d6" />
<img width="638" height="467" alt="image" src="https://github.com/user-attachments/assets/cd825f54-804e-466f-af62-494eecc839f5" />
<img width="517" height="177" alt="image" src="https://github.com/user-attachments/assets/8b720926-5f6c-4016-91d0-af5b439dd9a3" />

<p><img width="449" height="574" alt="image" src="https://github.com/user-attachments/assets/c038234b-9ed4-4568-ada5-fdc3334c5126" /></p>



  
</p>
<br />

<p>
13. Create a Domain Admin user within the domain.

  - In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called "_EMPLOYEES"
  - Create a new OU named "_ADMINS"
  - Create a new employee named "Jane Doe" and make a new password and username of "jane_admin"
  - Add jane_admin to the "Domain Admins" Security Group
  - Log out from DC-1, and then log back in as "mydomain.com\jane_admin"

<img width="649" height="601" alt="image" src="https://github.com/user-attachments/assets/db301f02-65f7-40bb-897d-e22a3b053eff" />
<img width="632" height="447" alt="image" src="https://github.com/user-attachments/assets/1cdf3895-4669-49de-98d2-7ec0164c2772" />
<img width="628" height="444" alt="image" src="https://github.com/user-attachments/assets/9bde90b6-1839-4feb-bbb1-18a0ec245a00" />
<img width="634" height="444" alt="image" src="https://github.com/user-attachments/assets/1e72249b-68bc-4a0c-a538-b5798f623781" />
<img width="371" height="321" alt="image" src="https://github.com/user-attachments/assets/0e56ca68-82f3-4e43-89f6-96bd6566d3ff" />
<img width="367" height="321" alt="image" src="https://github.com/user-attachments/assets/3385e4fd-16df-4322-934f-072ac201bd5c" />
<img width="632" height="443" alt="image" src="https://github.com/user-attachments/assets/b72d286b-6403-421e-930d-12e5114ef09e" />
<img width="344" height="446" alt="image" src="https://github.com/user-attachments/assets/d1bb7902-e187-4dac-8e0f-40ccec2c9546" />
<img width="385" height="209" alt="image" src="https://github.com/user-attachments/assets/9bbb0925-f3ef-433f-a5c1-8c4c73cf1a00" />
<img width="448" height="578" alt="image" src="https://github.com/user-attachments/assets/7e90c49e-7340-4a2f-9811-3e98498a31a3" />







</p>
<br />

<p>
14. Join Client-1 to the Domain

  - Go to System Properties
  - Click on Change under Computer Name
  - Click on Member Of and enter "mydomain.com"
  - Enter mydomain.com\jane_admin and use the password previously created when you added Jane Doe to the Domain Controller as a user/admin

<img width="345" height="396" alt="image" src="https://github.com/user-attachments/assets/4e297466-012e-4269-9c4d-925639302010" />
<img width="346" height="392" alt="image" src="https://github.com/user-attachments/assets/ffab19a6-2747-47db-853d-c19140b3b11d" />
<img width="373" height="315" alt="image" src="https://github.com/user-attachments/assets/b58772ce-6a50-4377-937f-72807e98529e" />
<img width="259" height="127" alt="image" src="https://github.com/user-attachments/assets/27fecd21-7252-4e79-9e5c-c7458c7b6c2a" />




</p>
<br />

<p>
15. Setup Remote Desktop for non-administrative users on Client-1

  - Log into Client-1 as jane_admin (mydomain.com\jane_admin)
  - Use the search bar and type "remote desktop settings"
  - Click on "Remote Desktop Users"
  - Allow "domain users" access to remote desktop by clicking "Add", and on the next popup screen type "domain users", click "Check Names", then Ok.
  - Now "MYDOMAIN\Domain Users" will show under the Remote Desktop Users popup. Click ok, and you have successfully allowed domain users access to remote desktop.

<img width="703" height="662" alt="image" src="https://github.com/user-attachments/assets/53debc93-e5a9-4ede-a19c-76d6cb1e2ca4" />

<img width="1007" height="580" alt="image" src="https://github.com/user-attachments/assets/694c139a-6b59-4da4-b328-a013f27bb6f7" />

<img width="727" height="276" alt="image" src="https://github.com/user-attachments/assets/875e18f6-8dca-4901-93fb-aea49d4e2cc1" />

<img width="314" height="275" alt="image" src="https://github.com/user-attachments/assets/67afaaf7-cb48-4c04-9a22-74a9b2cbf564" />




</p>
<br />

<p>
16. Create a batch of users and attempt to log into Client-1 with one of the new users

- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it
- Run the script and observe the accounts being created
- When finished, open Active Directory Users and Computer and observe the accounts in the appropriate OU　(_EMPLOYEES)
- attempt to log into Client-1 with one of the accounts (take note of the password in the script)

<img width="649" height="608" alt="image" src="https://github.com/user-attachments/assets/95a29c68-4b33-4601-9964-4e26afb41c17" />

<img width="1610" height="888" alt="image" src="https://github.com/user-attachments/assets/758986b1-0c09-495b-9285-425a0aa621b2" />

<img width="632" height="439" alt="image" src="https://github.com/user-attachments/assets/ab4adffb-64af-4d4d-99bd-9bc56eb290db" />

<img width="450" height="575" alt="image" src="https://github.com/user-attachments/assets/2fb91f07-0d05-416a-b260-506d3d59c1f9" />

<img width="406" height="455" alt="image" src="https://github.com/user-attachments/assets/9b1797b3-b54f-42c9-9e7f-5a362f33d5ac" />


</p>
