<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory: Deploying Active Directory & Creating Users with PowerShell in the Cloud (Azure)(2/3)</h1>
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
1) Log into <strong>dc-1</strong> and select <strong>"Add Roles and Features"</strong> in the Server Manager Dashboard.<br />
  <br />
<img src="https://i.imgur.com/yQpm7IK.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
2) To install Active Directory Domain Services, navigate to <strong>Server Roles > Active Directory Domain Services</strong>.  Continue with installation from that point forward.<br />
  <br />
<img src="https://i.imgur.com/7goyu1N.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
3) Next, to make <strong>dc-1</strong> a domain controller, navigate to the <strong>Server Manager Dashboard</strong>. Click on the flag with the orange triangle and <strong>"Promote this server to a new domain controller"</strong>. <br />
  <br />
<img src="https://i.imgur.com/f7C8uzQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
4) Next, navigate to <strong>Deployment Configuration > Add a New Forest > [enter] mydomain.com (or any alternative domain name) </strong>.<br />
  <br />
<img src="https://i.imgur.com/bwRgVP5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




<p>
5) Since we are logged on locally to <strong>dc-1</strong>, log out and re-login using the new domain name information as seen below.  From this point forward, we will be using our domain <strong>mydomain.com</strong> to access our virtual machines using Active Directory.<br />
  <br />
<img src="https://i.imgur.com/53IgUIW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
6) Now we are going to create an employees organizational unit in <strong>Active Directory Users and Computers (ADUC)</strong>. Navigate to <strong>search</strong> and enter <strong>Active Directory Users and Computers</strong>. [Right click] <strong>mydomain.com > New > Organizational Unit </strong> <br />
  <br />
<img src="https://i.imgur.com/ksyL5Qj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  <strong><i>Note: This configuration takes place within dc-1. Ensure that the following steps are on the correct VM.</i></strong>
  
</p>
<br />
<br />
<br />
<br />

<p>
7) Name the Organizational Unit <strong>"_EMPLOYEES"</strong>. <br />
  <br />
<img src="https://i.imgur.com/PBGXTKW.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  <strong><i>Note: It's crucial the name _EMPLOYEES is entered verbatim or else later steps will not work.</i></strong>
  
</p>
<br />
<br />
<br />
<br />

<p>
8) Add another Organizational Unit named <strong>"_ADMINS"</strong>.<br />
  <br />
<img src="https://i.imgur.com/8slDvvw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
9) Now, we will add a user to the <strong>"_ADMINS"</strong> Organizational Unit. Navigate to <strong>Active Directory Users and Computers > [right click] _ADMINS (under mydomain.com) > New > User. </strong> <br />
  <br />
<img src="https://i.imgur.com/F6ztp6l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />

<p>
  10) For demonstration purposes, the user is named <strong>Jane Doe</strong>.  However, the specific name is less important; just any username that can be easily remembered for testing purposes will do.  However, be sure to note the username and password for login purposes later on. <br />
  <br />
<img src="https://i.imgur.com/G4MblJ7.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
<strong><i>Note: "Jane Admin" will be the administrator for the Active Directory system in this demonstration, be sure to write down the administrator and their logon info for future use and configurations.</i></strong>
</p>
<br />
<br />
<br />
<br />

<p>
11) Once <strong>"Jane Doe"</strong> is added as a user in the <strong>"_Admins"</strong> OU, <strong>[right click] Jane Doe > [select] Properties</strong>.<br />
  <br />
<img src="https://i.imgur.com/pVeRDwq.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />

<p>
12) In the properties section of Jane Doe, select <strong>"Member of"</strong> and select <strong>"Add"</strong>.  A text box will appear, type <Strong>"Domain Admins"</Strong>.  This will grant Admin permissions to <strong>Jane Doe</strong>, the Organizational Unit alone will not do this automatically. <br />
  <br />
<img src="https://i.imgur.com/2HmXThg.png" height="80%" width="60%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
13) Now, disconnect from <strong>dc-1</strong> to logon to <strong>Client-1</strong> using our updated <strong>"Jane Doe"</strong> admin. <br />
  <br />
<img src="https://i.imgur.com/oeywsHB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />


<p>
14) Now, log into <strong>Client-1</strong> using the following information.<br />
  <br />
  <strong>Username:</strong>mydomain.com\[username] <br />
  <strong>Password:</strong>[password]
  <br />
<img src="https://i.imgur.com/i2VnmpL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />




<p>
15) Now, we are going to join <strong>Client-1</strong> to our newly-created domain. Navigate to <strong> Settings > About > Rename this PC (Advanced)</strong><br />
  <br />
<img src="https://i.imgur.com/rafTcaK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
16) Under <strong>"Member Of"</strong> select <strong>"Domain"</strong> and enter <strong>"mydomain.com"</strong>. <br />
  <br />
<img src="https://i.imgur.com/5EBhFMO.png" height="80%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
17) Once completed, a prompt will ask for admin verification. Enter the adminuser you created in the previous steps to join <strong>Client-1</strong> to the domain. <br />
  <br />
<img src="https://i.imgur.com/1KPHc7G.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
18) For changes to be implemented, a restart will be required. Click <strong>"Restart Now"</strong>.<br />
  <br />
<img src="https://i.imgur.com/viTuBws.png" height="40%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
19) Navigate back to <Strong>dc-1 to modify domain controller settings.</Strong> Now, we are going to create another Organizational Unit Navigate to <strong>Active Directory Users and Computers</strong>.<br />
  <br />
<img src="https://i.imgur.com/x1KjUDR.png" height="40%" width="80%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />

<p>
20) <strong>[Right Click] mydomain.com > New > Organizational Unit</strong>. <br />
  <br />
<img src="https://i.imgur.com/HyeqUMH.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />

<p>
  21) Name the Organizational Unit <strong>_CLIENTS</strong>. <br />
  <br />
<img src="https://i.imgur.com/3eFc5sQ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
22) Next, log into <strong>Client-1</strong> as <strong>mydomain.com\jane_admin</strong>.<br />
  <br />
<img src="https://i.imgur.com/hWg2i4X.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/IQkCG5d.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />
<br />
<br />

<p>
23) Navigate to <strong>"System Properties" > "Remote Desktop" > "Select Users that Can Remotely Access this PC"</strong>. <br />
  <br />
<img src="https://i.imgur.com/PvHjPqR.png" height="60%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<br />
<br />
<br />
<br />

<p>
24) Select <strong>"ADD"</strong>and type <strong>"domain users"</strong> to give users access to remote desktop. This will allow the users we create in the following steps to access remote desktop. <br />
  <br />
<img src="https://i.imgur.com/bNoSMcI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
</p>
<br />
<br />
<br />
<br />



<p>
25) To create users, navigate to <strong>Windows PowerShell ISE.</strong></strong><br />
  <br />
<img src="https://i.imgur.com/rStTpHU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


<p>
26) On the header bar, select <strong>File > New</strong>.  Then, paste the prompt provided in this text document https://drive.google.com/file/d/1-auybwRQDAw4wtEO2-DSK2EDU9KFZUH7/view?usp=sharing. <br />
  <br />
<img src="https://i.imgur.com/cCHwxb0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
<img src="https://i.imgur.com/HxM0u22.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
<br />
<br />
<br />
<br />
 
  
<p>
27) After running the prompt, users should begin to be created. This prompt will generate <strong>10,000</strong> unique users in Active Directory.<br />
  <br />
<img src="https://i.imgur.com/zPlGcxG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />

<p>
28) Navigate to <strong>Active Directory Users and Computers > mydomain.com > _EMPLOYEES.</strong> Next, select a user at random to login to <strong>Client-1</strong> to test our new Active Directory system.  For demonstration purposes, I've selected the user <Strong>"bat.cop"</Strong> as shown below.<br />
  <br />
<img src="https://i.imgur.com/coXCci2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />

<p>
29) After selecting a user at random, test this user's access by logging into <Strong>client-1</Strong> with their information. <br />
  <br />
<img src="https://i.imgur.com/SWs3mrp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
 
</p>
<br />
<br />
<br />
<br />

<p>
30) As seen below, <strong>bat.cop</strong> has access to <strong>client-1</strong> under the <strong>mydomain.com</strong> domain.  This concludes this part of the Active Directory tutorial. <br />
  <br />
<img src="https://i.imgur.com/b1A7nXT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br />
  
</p>
<br />
<br />
<br />
<br />


