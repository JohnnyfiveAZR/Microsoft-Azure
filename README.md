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
<h3 align="left">Create Resources in Azure</h3>

<p>

  
  <img src="https://i.imgur.com/GfT71Ka.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the Domain Controller VM (Windows Server 2022) named |DC-1|
</p>
<br />

<p>
<img src="https://i.imgur.com/U4NcVRe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the Client VM (Windows 10) named |Client|. Use the same Resource Group
</p>
<br />

<p>
<img src="https://i.imgur.com/OHOVRPi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set Domain Controller’s NIC Private IP address static:
</p>
<br />


<img src="https://i.imgur.com/mznqDV5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Verify that both VMs are in the same Vnet(Virtual Network). You can check the topology with Network Watcher.



<img src="https://i.imgur.com/L7CrNBo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3 align="left">Ensure Connectivity between the client and Domain Controller</h3>

Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)


<img src="https://i.imgur.com/eGbvXsz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall

<img src="https://i.imgur.com/gd50U4W.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Check back at Client-1 to see the ping succeed:

<img src="https://i.imgur.com/gxtMDa4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3 align="left">Installing Active Directory</h3>


Login to DC-1 and install Active Directory Domain Services

<img src="https://i.imgur.com/gXWVoHj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Promote as a Domain Controller:

<img src="https://i.imgur.com/0sT1bwv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)

<img src="https://i.imgur.com/WHH5tBD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


Restart and then log back into DC-1 as user: mydomain.com\labuser

<img src="https://i.imgur.com/LgtNcyL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


Text

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
  
Text
  
  
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
