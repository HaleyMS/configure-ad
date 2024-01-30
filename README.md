<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

Part 1: https://i.imgur.com/lHcAaa3.mp4
<p>
Part 2: https://i.imgur.com/N0HkSji.mp4

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Created a Domain Controller and Client-1 Virtual Machines in Azure
- Step 2: Install Active Directory on the Domain Controller
- Step 3: Created an Administrator and Normal User Accounts in Active Directory
- Step 4: Join Client-1 VM to the Domain Controller (DC-1)
- Step 5: Set up Remote Desktop for Non-Administrative Users
- Step 6: Created Additional User Accounts
- Step 7: Created New A-Records and CNAME-Records in Active Directory
- Step 8: Configured Network File Sharing and Permissions 
- Step 9: Created a Security Group, Configured Permissions, and Tested 

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/LOia10Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 This is an image of me doing the initial set up for this project. I created two different virtual Machines in Azure. One with the Windows Server 2022 Data Center, the other on Windows 10 Pro, and set both up on the same v-net 
</p>
<br />

<p>
<img src="https://i.imgur.com/do1UNKO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 In the image above I am installing Active Directory onto DC-1. In the Server Manager I was able to configure the set up for Active Directory, under roles I installed the Active Directory Domain Services. I was able to promote DC-1 to a domain controller, adding a new foster I named my root domain "mydomain.com". I was  logged out and had to use the FQDN or fully qualified domain name of the user to get back in. 
</p>
<br />

<p>
<img src="https://i.imgur.com/mCtuS19.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Here I am creating Organizational Units named _EMPLOYEES and _ADMINS. I created a new admin user with the name of HaleyMS, configured their properties, and assigned them to the domain admins group in Active Directory. After creating the account I was successfully able to log in to the admin account on the DC-1 VM. 
</p>
<br />

<p>
<img src="https://i.imgur.com/cwYa4Qp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 The image above shows one of the steps I took to join Client-1's VM. Inside Azure I configured the NIC Private IP address for Client-1. I configured the DNS Server to "Custom" and set it to DC-1's Private Address, and restarted the Virtual MAchine. Signing back into Client-1 I had to use the FQDN (Fully Qualified Domain Name) of my domain.     
</p>
<br />

<p>
<img src="https://i.imgur.com/PnWvr01.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 From inside Client-1 I was able to set up Remote Desktop access for the non-administrative user accounts. 
</p>
<br />

<p>
<img src="https://i.imgur.com/UlQwimI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 The image above is a screenshot I took while creating a bunch of additional users into Active Directory. In PowerShell ISE I was able to upload a script that included new users which were randomly configured. They were added into the _EMPLOYEES file created in Active Directory. I was able to establish a remote desktop connection of a few of the random user accounts and logged into Client-1's VM. 
</p>
<br />

<p>
<img src="https://i.imgur.com/nXYX790.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 Here I am creating A-Records and CNAME-Records in Active Directory. I attempted to ping mainframe from Client-1 and did not get a response. I went into DC-1 and named an A-Record named mainframe, and connected it to DC-1's Private IPv4 Address. Going back to Client-1 I was able to successfully ping the mainframe. I went back to DC-1 and configured the mainframe A-Record to have an IP Address of 8.8.8.8 and attempted to ping the mainframe again from Client-1. After checkeing the DNS Cache I noticed the IP Address of 10.0.0.4 still reading for the mainframe. I flushed the DNS and attempted the ping again, I was able to successfully get the IP address of 8.8.8.8 I had configured the mainframe to. I than created a CNAME-Record called search and linked it to www.google.com. I was able to successfully ping "search" and get a response from the appropriate alias linked to the record.   
</p>
<br />

<p>
<img src="https://i.imgur.com/qU7vDVi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 This Image shows me creating one of four new files onto the (C:) drive of the domain controller (DC-1). The first file I created was titled Read-Access, which was accessible to the Domain Users, with read only permissions. The second was Write-Access, which was accessible to the Domain Users, with read and write permissions. The third file was titled No-Access, I gave the Domain Administrators access, and read and write permissions. The last file created was Accounting, for later use. After adding the files I logged onto Client-1 under a random user account to test the accessibility of the files created.  
</p>
<br />

<p>
<img src="https://i.imgur.com/5NRRXTl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 After assigning the random user account to the appropriate groups. I was successfully able to access the Accounting file, the read-access file, and write-access file shared over the network. I had given the randomly created user the permissions to view the documents by adding them to the ACCOUNTANTS group. 
</p>
<br />
