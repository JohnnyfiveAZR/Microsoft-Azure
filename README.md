<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br/>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a batch of additional users and attempt to log into Client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Create Resources in Azure</h3>
<br />
<br />
<p>

  
  <img src="https://i.imgur.com/GfT71Ka.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<br />
<br />
 Create the Domain Controller VM (Windows Server 2022) named |DC-1|
</p>
<br />
<br />
<p>
<img src="https://i.imgur.com/U4NcVRe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<br />
<br />
Create the Client VM (Windows 10) named |Client|. Use the same Resource Group
</p>
<br />
<br />
<p>
<img src="https://i.imgur.com/OHOVRPi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<br />
<br />
Set Domain Controller’s NIC Private IP address static:
</p>
<br />
<br />

<img src="https://i.imgur.com/mznqDV5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Verify that both VMs are in the same Vnet(Virtual Network). You can check the topology with Network Watcher.
<br />
<br />
<br />

<img src="https://i.imgur.com/L7CrNBo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h3 align="center">Ensure Connectivity between the client and Domain Controller</h3>
<br />
<br />
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
<br />
<br />
<br />
  

<img src="https://i.imgur.com/eGbvXsz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
<br />
<br />
<br />
  

<img src="https://i.imgur.com/gd50U4W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Check back at Client-1 to see the ping succeed:
<br />
<br />
<img src="https://i.imgur.com/gxtMDa4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<h3 align="center">Installing Active Directory</h3>
<br />
<br />

Login to DC-1 and install Active Directory Domain Services
<br />
<br />

<img src="https://i.imgur.com/gXWVoHj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Promote as a Domain Controller:
<br />
<br />
  
<img src="https://i.imgur.com/0sT1bwv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
<br />
<br />
  
<img src="https://i.imgur.com/WHH5tBD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Restart and then log back into DC-1 as user: mydomain.com\labuser
<br />
<br />
  
<img src="https://i.imgur.com/LgtNcyL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 
<h3 align="center">Create an Admin and Normal User Account in AD</h3>
<br />
<br />
  
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” and "_ADMINS"
<br />
<br />
  
<img src="https://i.imgur.com/niMqWpd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
   
<img src="https://i.imgur.com/SfIYWad.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Create a new employee named “Johnny VMan” (same password) with the username of “Johnny_admin”
<br />
<br />
    
<img src="https://i.imgur.com/Lk96BPh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Add Johnny_admin to the “Domain Admins” Security Group
<br />
<br />
  
<img src="https://i.imgur.com/LZkhdlu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/DOsaVl3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/qg0wF3K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/A4Qgc4X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/nJaxfP1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\Johnny_admin”
<br />
<br />
  
<img src="https://i.imgur.com/6a7ltWe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h3 align="center">Join Client-1 to your domain (mydomain.com)</h3>
<br />
<br />

From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
<br />
<br />

<img src="https://i.imgur.com/KZ7ZBsZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
From the Azure Portal, restart Client-1
<br />
<br />
  
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain |computer will restart|
<br />
<br />
  
<img src="https://i.imgur.com/WNRBYvs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/PeEBULu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/xSr4Jyy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/jhvlR4m.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
<br />
<br />

Create a new OU named “_CLIENTS” and drag Client-1 into there
<br />
<br />
  
<img src="https://i.imgur.com/GE7fJZC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<h3 align="center">Setup Remote Desktop for non-administrative users on Client-1</h3>
<br />
<br />
<p>
Log into Client-1 as mydomain.com\Johnny_admin and open system properties.
</p>
<p>
  Click “Remote Desktop”.
</p>
<p>
  Allow “domain users” access to remote desktop.
</p>
<p>
  You can now log into Client-1 as a normal, non-administrative user now.
</p>
<p>
  Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)
<br />
<br />

<img src="https://i.imgur.com/oeTMvYh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  

<h3 align="center">Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>
<br />
<p>
  Login to DC-1 as Johnny_admin
</p>
<p>
  Open PowerShell_ise as an administrator.
</p> 
<p>  
  Create a new File and paste the contents of this script into it: https://github.com/JohnnyfiveAZR/Active-Directory
<br />
<br />
  
<img src="https://i.imgur.com/Iic8jTH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
  
<img src="https://i.imgur.com/nkKJwDx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
  
<img src="https://i.imgur.com/5ppkwmC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Run the script and observe the accounts being created
<br />
<br />
  
  
<img src="https://i.imgur.com/5a95s0z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)
<br />
<br />

<img src="https://i.imgur.com/Mm0IEFI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/QMm3pbC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
  
<img src="https://i.imgur.com/HcldyWN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
<h3 align="left">Finished!</h3>
  
I hope this tutorial gives you a bit of insight and better understanding on how to go about setting up an Active Directory (Domain) Lab through your virtual machine environment. Repeat this lab as many times as you please and make this virtual environment your own learning playground and explore the other possibilities in managing user accounts, permissions, passwords, devices, and control access on a large scale. (This lab can be completed in both Windows and MACos)
<br />
<br />
<br />
<h3 align="left">Note:</h3> Dont forget to close out your Guest VMs while in RDP by going to CMD> Logoff. Also make sure to CLEAN UP your Microsoft Azure environment and ensure your Resource Groups and Virtual Machines are deleted which may take a few minutes then refresh to confirm.
  
