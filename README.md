<!-- Logo -->
<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo" width="250"/>
</p>

<!-- Title -->
<h1>On-Premises Active Directory Lab in Azure</h1>
<p style="text-align:center; font-size:1.1em; color:#a0c4ff;">
  A step-by-step guide to safely deploy an Active Directory Domain on Azure Virtual Machines.
</p>

<hr style="border-color:#00e0ff;"/>

<!-- Technologies -->
<h2>Environments & Technologies</h2>
<ul>
  <li>💻 Microsoft Azure (Virtual Machines / Compute)</li>
  <li>🖥 Remote Desktop</li>
  <li>🛠 Active Directory Domain Services</li>
  <li>💻 PowerShell</li>
</ul>

<!-- Operating Systems -->
<h2>Operating Systems</h2>
<ul>
  <li>🖥 Windows Server 2022</li>
  <li>💻 Windows 10 (21H2)</li>
</ul>

<!-- High-Level Steps -->
<h2>High-Level Deployment Steps</h2>
<ol>
  <li>✅ Create Azure resources (Domain Controller & Client VMs, Virtual Network)</li>
  <li>✅ Ensure connectivity between Client-1 and Domain Controller</li>
  <li>✅ Install Active Directory Domain Services on DC-1</li>
  <li>✅ Create Admin and standard user accounts in AD</li>
  <li>✅ Join Client-1 to your domain (<code>mydomain.com</code>)</li>
  <li>✅ Enable Remote Desktop for non-administrative users</li>
  <li>✅ Batch-create additional users and verify logins</li>
</ol>


<hr/>

<!-- Step 1 -->
<details>
<summary>Create Resources in Azure</summary>
<p>Create Domain Controller VM (DC-1) and Client VM (Client-1). Ensure they are in the same Resource Group.</p>
<img src="https://i.imgur.com/GfT71Ka.png" alt="Azure Resource Setup"/>
<img src="https://i.imgur.com/U4NcVRe.png" alt="Create DC VM"/>
<img src="https://i.imgur.com/OHOVRPi.png" alt="Create Client VM"/>
<img src="https://i.imgur.com/mznqDV5.png" alt="Set static IP"/>
<img src="https://i.imgur.com/L7CrNBo.png" alt="Verify VNet"/>
</details>

<!-- Step 2 -->
<details>
<summary>Ensure Connectivity between Client and Domain Controller</summary>
<p>Login to Client-1 via RDP and ping DC-1:</p>
<pre>ping -t &lt;DC-1_IP&gt;</pre>
<p>Enable ICMPv4 on DC firewall. Verify ping is successful.</p>
<img src="https://i.imgur.com/eGbvXsz.png" alt="Ping from Client"/>
<img src="https://i.imgur.com/gd50U4W.png" alt="Enable ICMPv4"/>
<img src="https://i.imgur.com/gxtMDa4.png" alt="Ping succeeds"/>
</details>

<!-- Step 3 -->
<details>
<summary>Install Active Directory on DC-1</summary>
<ol>
  <li>Install Active Directory Domain Services</li>
  <li>Promote DC-1 to Domain Controller</li>
  <li>Create new forest: mydomain.com</li>
  <li>Restart and log in as mydomain.com\labuser</li>
</ol>
<img src="https://i.imgur.com/gXWVoHj.png" alt="Install AD"/>
<img src="https://i.imgur.com/0sT1bwv.png" alt="Promote DC"/>
<img src="https://i.imgur.com/WHH5tBD.png" alt="Setup forest"/>
<img src="https://i.imgur.com/LgtNcyL.png" alt="Login as labuser"/>
</details>

<!-- Step 4 -->
<details>
<summary>Create Admin and Normal User Accounts in AD</summary>
<ol>
  <li>Create OUs: _EMPLOYEES and _ADMINS</li>
  <li>Create user Johnny VMan → Johnny_admin</li>
  <li>Add Johnny_admin to Domain Admins</li>
  <li>Log out and back in as Johnny_admin</li>
</ol>
<img src="https://i.imgur.com/niMqWpd.png" alt="Create OUs"/>
<img src="https://i.imgur.com/SfIYWad.png" alt="ADUC interface"/>
<img src="https://i.imgur.com/Lk96BPh.png" alt="Create Admin user"/>
<img src="https://i.imgur.com/LZkhdlu.png" alt="Add to Domain Admins"/>
<img src="https://i.imgur.com/DOsaVl3.png" alt="Confirm Admin group"/>
<img src="https://i.imgur.com/qg0wF3K.png" alt="Check user"/>
<img src="https://i.imgur.com/A4Qgc4X.png" alt="Verify user"/>
<img src="https://i.imgur.com/nJaxfP1.png" alt="Final verification"/>
<img src="https://i.imgur.com/6a7ltWe.png" alt="Login as Johnny_admin"/>
</details>

<!-- Step 5 -->
<details>
<summary>Join Client-1 to Domain</summary>
<ol>
  <li>Set Client DNS to DC private IP</li>
  <li>Restart Client-1</li>
  <li>Join domain via local admin</li>
  <li>Verify Client-1 in ADUC → Computers</li>
  <li>Move Client-1 to _CLIENTS OU</li>
</ol>
<img src="https://i.imgur.com/KZ7ZBsZ.png" alt="Set Client DNS"/>
<img src="https://i.imgur.com/WNRBYvs.png" alt="Join domain"/>
<img src="https://i.imgur.com/PeEBULu.png" alt="Domain joined"/>
<img src="https://i.imgur.com/xSr4Jyy.png" alt="Verify domain"/>
<img src="https://i.imgur.com/jhvlR4m.png" alt="Check Client"/>
<img src="https://i.imgur.com/GE7fJZC.png" alt="Move Client to OU"/>
</details>

<!-- Step 6 -->
<details>
<summary>Enable Remote Desktop for Non-Admins</summary>
<ol>
  <li>Login as Johnny_admin on Client-1</li>
  <li>System Properties → Remote Desktop → Allow domain users</li>
  <li>Non-admin users can now log in via RDP</li>
</ol>
<img src="https://i.imgur.com/oeTMvYh.png" alt="Enable Remote Desktop"/>
</details>

<!-- Step 7 -->
<details>
<summary>Create Additional Users via Script</summary>
<ol>
  <li>Login to DC-1 as Johnny_admin</li>
  <li>Open PowerShell ISE as Admin</li>
  <li>Paste and run script: <a href="https://github.com/JohnnyfiveAZR/Active-Directory">GitHub Script</a></li>
  <li>Verify users in ADUC and test login</li>
</ol>
<img src="https://i.imgur.com/Iic8jTH.png" alt="Open PowerShell ISE"/>
<img src="https://i.imgur.com/nkKJwDx.png" alt="Create Script"/>
<img src="https://i.imgur.com/5ppkwmC.png" alt="Run Script"/>
<img src="https://i.imgur.com/5a95s0z.png" alt="Verify created users"/>
<img src="https://i.imgur.com/Mm0IEFI.png" alt="Login test"/>
<img src="https://i.imgur.com/QMm3pbC.png" alt="Confirm user accounts"/>
<img src="https://i.imgur.com/HcldyWN.png" alt="Final check"/>
</details>

<hr/>

<h2>🎯 Lab Complete</h2>
<p>Congratulations! Your AD Lab is ready. Use it to explore user management, permissions, password resets, device connections, and advanced AD features.</p>

<h2>🧹 Cleanup & Best Practices</h2>
<ul>
  <li>Close all Guest VMs</li>
  <li>Log off via RDP or CLI</li>
  <li>Delete Azure Resource Groups & VMs</li>
  <li>Refresh portal to confirm all resources removed</li>
</ul>

<h2>🌟 Next Steps</h2>
<ul>
  <li>Automate AD tasks with PowerShell</li>
  <li>Apply Group Policy across multiple clients</li>
  <li>Explore replication, trusts, and OU delegation</li>
  <li>Expand to hybrid AD with Azure AD</li>
</ul>

<p align="center" style="font-weight:bold; font-size:1.2em;">Keep experimenting, and happy learning! 🚀</p>

</body>
</html>
