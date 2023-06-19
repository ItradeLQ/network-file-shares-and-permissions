<p align="center">
<img src="https://i.imgur.com/mT7ZBJg.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network File Shares and Permissions</h1>
In this tutorial we will crete some file shares with different permissions and attempt to access them.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machine,Domain Controller, Client one machine)
- Remote Desktop
- Active Directory Domain Services
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)


<h2>File Shares and Observation</h2>
</p>
<p>
Login to DC-1 as your domain admin account, in my case it is mydomain.com\kanza_admin) and create some file shares with various permissions.
  
login to Client-1 as a normal user (mydomain\<someuser>)
  
  
  
<p>
<img src="https://i.imgur.com/yLaBaKv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

On DC-1, go the c:\ drive and create four folders “read-access”, “write-access”, “no-access”, “accounting”
</p>
<br />

<p>
<img src="https://i.imgur.com/95d8nlr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4.	Set the following permissions, share the folder for the “Domain Users” group.
  
  
Folder: “read-access”, Group: “Domain Users”, Permission: “Read” and to do that right click>properties>sharing>share>type domain users and share.
  
  
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”

  
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”


</p>
<br />

<p>
<img src="https://i.imgur.com/i6eg92t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Skip the accounting folder for now.
</p>
<br />

<p>
<img src="https://i.imgur.com/URaqAQl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now attempt to access file shares as the normal users.
</p>
<br />

<p>
<img src="https://i.imgur.com/tvziEcm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, navigate to the shared folder On to file explorer (start, run, \\dc-1)
</p>
<br />

<p>
<img src="https://i.imgur.com/R8RxzdU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Try to access the folder that you created, which folder that you can access? which folder you can create some stuff in?
</p>
<br />

<p>
<img src="https://i.imgur.com/bGl7MVc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to the DC-1, in Active Directory>right click mydomain.com>new>OU>_SECURITY_GROUPS and refresh mydomian.com.

</p>
<br />

<p>
<img src="https://i.imgur.com/KH6jrlI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Inside "Security Groups" create new group called “ACCOUNTANTS”.  
</p>
<br />

<p>
<img src="https://i.imgur.com/Kiem7FW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Go to file explorer On the “accounting” folder you created earlier, set the following permissions: “Read/Write”
  
“accounting” Right click>properties>sharing>share>ACCOUNTANTS>CLICK add>read and write>share>done>close.
</p>
<br />

<p>
<img src="https://i.imgur.com/NWD4coR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On client-1, try to access the Accounting folder. It will fail, then logout from client-1. 
</p>
<br />

<p>
<img src="https://i.imgur.com/23QpucQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1 make the user the member of the Accountant Security group.
  
Login back as that user in Client-1 and try to access the Accounting share file in \DC-1.
</p>
<br />
