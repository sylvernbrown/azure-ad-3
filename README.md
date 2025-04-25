<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory: Deploying Active Directory & Creating Users with PowerShell in the Cloud (Azure)(3/3)</h1>
This tutorial outlines the setup of the pre-requisite Microsoft Azure architecture for Active Directory & the creation of Users in Active Directory using PowerShell.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>High-Level Setup & Deployment Steps</h2>

- Install Active Directory on the Domain Controller VM
- Create a Domain Admin user within the domain
- Join Client-1 (VM #2) with the new domain (mydomain.com)
- Set up Remote Desktop for non-administrative users on Client-1
- Create additional users using PowerShell
- Log on to Client-1 with a randomly generated user from PowerShell


<h2>Setup & Deployment Steps</h2>

<p>
1) Log into <strong>dc-1</strong> as an administrator, navigate to the search bar, and type <strong>"run"</strong>. Then, type <strong>"gpmc.msc</strong>. <br />
  <br />
<img src="https://i.imgur.com/Y8DOtZ9.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
2) In the <strong>Group Policy Management</strong> window, <strong>[Right Click] Default Domain > Edit</strong>.  This will allow for the configuration of account lockout settings.<br />
  <br />
<img src="https://i.imgur.com/IAzqRP4.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
3) Navigate to: <strong>Account Lockout Policy > Account Lockout Duration | Account Lockout Threshold</strong>. <br />
  <br />
<img src="https://i.imgur.com/Z9m5d4A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
4) Once in <strong>Account lockout duration Properties</strong>, select the desired time frame for an account to remain locked after being locked out.  In this example, I set it to 30 minutes.<br />
  <br />
<img src="https://i.imgur.com/Y4RC6rd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




<p>
5) Then, navigate to <strong>Account lockout threshold properties</strong> and decide on a maximum threshold for consecutive login attempts, for this example I set it at 10.<br />
  <br />
<img src="https://i.imgur.com/giDSs0Z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
6) The end result should show something like this in <strong>Group Policy Management Editor.  Notice, default settings for <strong>"Reset account lockout counter after" & "Allow Administrator account lockout" both automatically enable, feel free to change these at will as well.</strong></strong><br />
  <br />
<img src="https://i.imgur.com/mSqrYXO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  <strong><i>Note: This configuration takes place within dc-1. Ensure that the following steps are on the correct VM.</i></strong>
  
</p>
<br />
<br />
<br />
<br />

<p>
7) WHile the changes have been enabled, they would take 90 minutes to apply in the domain controller without manually enabling them.  To manually enable to configurations, navigate to the domain controller (dc-1) as an admin. <br />
  <br />
<img src="https://i.imgur.com/KbNMSd5.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  <strong><i>Note: It's crucial the name _EMPLOYEES is entered verbatim or else later steps will not work.</i></strong>
  
</p>
<br />
<br />
<br />
<br />

<p>
8) Open the command prompt as an administrator, and type <strong>"gpupdate /force"</strong>.  As you can see, the updates should complete successfully.<br />
  <br />
<img src="https://i.imgur.com/oLp9sTF.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
  10) Next, test the changes made in the domain controller by logging in incorrectly on <strong>Client-1</strong> incorrectly at least 10 times.  If the changes were successful, you should see a prompt like this. <br />
  <br />
<img src="https://i.imgur.com/aLWHOX5.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
<strong><i>Note: "Jane Admin" will be the administrator for the Active Directory system in this demonstration, be sure to write down the administrator and their logon info for future use and configurations.</i></strong>
</p>
<br />
<br />
<br />
<br />

<p>
11) To unlock the account <strong>bat.cop</strong> and restore access, we will have to unlock his account in Active Directory on the domain controller.  Navigate to: [dc-1 VM] > Active Directory Users and Computers > [Right Click] mydomain.com > Find > [Username].<br />
  <br />
<img src="https://i.imgur.com/VhgqfKR.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/6NtxHAi.png" height="80%" width="60%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/MaUR8kV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />



<p>
14) After finding the user you wish to unlock, navigate to the user's properties. <strong>[Right Click] "bat.cop" > Properties > Account > [Select] "Unlock account"</strong>.<br />
  <br />
  <strong>Username:</strong>mydomain.com\[username] <br />
  <strong>Password:</strong>[password]
  <br />
<img src="https://i.imgur.com/cFtosjK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/3w0jPVj.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




<p>
15) If you need to reset a password for a particular user, once again navigate to the user.  Once you find the user, right click and select <Strong>"Reset Password".</Strong><br />
  <br />
<img src="https://i.imgur.com/3w0jPVj.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />



<p>
16) 
  <br />
<img src="https://i.imgur.com/AmntZGE.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
19) Additionally, from this panel you have the option to disable a user's account. <br />.
  <br />
<img src="https://i.imgur.com/rwlactt.png" height="40%" width="80%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/uguEAUr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
20) When logging into <strong>client-1</strong> with a disabled account, the following message would display. <br />
  <br />
<img src="https://i.imgur.com/HERSlxx.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />


<p>
22) To re-enable the account, navigate back to the user properties panel and select <strong>Enable Account</strong>.<br />
  <br />
<img src="https://i.imgur.com/z5C2yOz.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
23) Navigate to <strong>"System Properties" > "Remote Desktop" > "Select Users that Can Remotely Access this PC"</strong>. <br />
  <br />
<img src="https://i.imgur.com/tA05HSb.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
24) Select <strong>"ADD"</strong>and type <strong>"domain users"</strong> to give users access to remote desktop. This will allow the users we create in the following steps to access remote desktop. <br />
  <br />
<img src="https://i.imgur.com/UlGEWgv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
25) To create users, navigate to <strong>Windows PowerShell ISE.</strong></strong><br />
  <br />
<img src="https://i.imgur.com/Lsm4eA8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




