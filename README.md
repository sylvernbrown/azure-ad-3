<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory: Group Policy & Account Management in the Cloud (Azure)(3/3)</h1>
This tutorial outlines common functions in Active Directory that are used to manage group policy and users.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>High-Level Group Policy & Account Management Steps</h2>

- Managing Account Lockouts
- Resetting Account Passwords
- Enabling & Disabling Accounts
- Observing Logs


<h2>Group Policy & Account Management Steps</h2>

<p>
1) Log into <strong>dc-1</strong> as an administrator, navigate to the search bar, and type <strong>"run"</strong>. Then, type <strong>"gpmc.msc"</strong>. <br />
  <br />
<img src="https://i.imgur.com/Y8DOtZ9.png" height="40%" width="60%" alt="Disk Sanitization Steps"/><br />
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
4) Once in <strong>Account lockout duration Properties</strong>, select the desired time frame for an account to remain locked after being locked out.<br />
  <br />
<img src="https://i.imgur.com/Y4RC6rd.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />




<p>
5) Then, navigate to <strong>Account lockout threshold properties</strong> and decide on a maximum threshold for consecutive login attempts, for this example it's set at 10.<br />
  <br />
<img src="https://i.imgur.com/giDSs0Z.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
6) The end result should show something like this in <strong>Group Policy Management Editor</strong>.  Notice: Default settings for <strong>"Reset account lockout counter after" & "Allow Administrator account lockout"</strong> both automatically enable.<br />
  <br />
<img src="https://i.imgur.com/mSqrYXO.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
7) While the changes have been enabled, they would take 90 minutes to apply in the domain controller automatically.  To manually enable to configurations, login to the domain controller (dc-1) as an admin. <br />
  <br />
<img src="https://i.imgur.com/KbNMSd5.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
8) Open the command prompt as an administrator, and type <strong>"gpupdate /force"</strong>.  As you can see, the updates should complete successfully.<br />
  <br />
<img src="https://i.imgur.com/oLp9sTF.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
9) Next, test the changes made in the domain controller by logging in incorrectly on <strong>Client-1</strong> incorrectly at least 10 times.  If the changes were successful, you should see a prompt like this. <br />
  <br />
<img src="https://i.imgur.com/aLWHOX5.png" height="60%" width="40%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
10) To unlock the account <strong>bat.cop</strong> and restore access, we will have to unlock his account in Active Directory on the domain controller.  Navigate to: <strong>[dc-1 VM] > Active Directory Users and Computers > [Right Click] mydomain.com > Find > [Username]</strong>.<br />
  <br />
<img src="https://i.imgur.com/VhgqfKR.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/6NtxHAi.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/MaUR8kV.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
11) After finding the user you wish to unlock, navigate to the user's properties. <strong>[Right Click] "bat.cop" > Properties > Account > [Select] "Unlock account"</strong>.<br />
  <br />
  <br />
<img src="https://i.imgur.com/cFtosjK.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




<p>
12) If you need to reset a password for a particular user, once again navigate to the user.  Once you find the user, right click and select <Strong>"Reset Password".</Strong><br />
  <br />
<img src="https://i.imgur.com/3w0jPVj.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/AmntZGE.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br /> 
</p>
<br />
<br />
<br />
<br />




<p>
13) Additionally, from this panel you have the option to disable a user's account. <br />.
  <br />
<img src="https://i.imgur.com/rwlactt.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/uguEAUr.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />

<p>
14) When logging into <strong>client-1</strong> with a disabled account (bat.cop), the following message would display. <br />
  <br />
<img src="https://i.imgur.com/HERSlxx.png" height="60%" width="40%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />


<p>
15) To re-enable the account, navigate back to the user properties panel and select <strong>Enable Account</strong>.<br />
  <br />
<img src="https://i.imgur.com/z5C2yOz.png" height="80%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
16) To witness failed/successful logins by username, login to the domain controller (dc-1) navigate to search and type <strong>"eventvwr.msc"</strong>. <br />
  <br />
<img src="https://i.imgur.com/tA05HSb.png" height="40%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
17) Then, navigate to <strong>Find > [USERNAME] > Find All</strong>. This will show all the attempted logins that were rejected and accepted in the security tab. <br />
  <br />
<img src="https://i.imgur.com/UlGEWgv.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
18) As seen below, in the event viewer, you can see all logon attempts and make security decisions based off of them.  Here, we see all login attempts by <strong>bat.cop</strong> and can see where access was restored in the lab environment.</strong><br />
  <br />
<img src="https://i.imgur.com/Lsm4eA8.png" height="60%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />



