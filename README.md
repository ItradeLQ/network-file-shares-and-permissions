<p align="center">
<a href="https://imgur.com/ortiY1T"><img src="https://i.imgur.com/ortiY1T.png" title="source: imgur.com" /></a>
</p>

<h1>Network File Shares and Permissions</h1>
In this tutorial we will create file shares with different permissions and attempt to access them.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machine, Domain Controller, Client-1 machine)
- Remote Desktop
- Active Directory Domain Services
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)


<h2>File Shares and Observation</h2>
</p>
<p>
Login to DC-1 as your Domain Admin account. My case it's (mydomain.com\jane_admin) and create some folders with varying sharing permissions.
  
Login to Client-1 as a normal user (mydomain\<normaluser>)
  
  
  
<p>
<img src="https://i.imgur.com/yLaBaKv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

On DC-1, go to the c:\ drive and create four folders “read-access”, “write-access”, “no-access”, “accounting”
</p>
<br />

<p>
<img src="https://i.imgur.com/95d8nlr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4.	Set the following permissions, and share the folder for the “Domain Users” group.
  
  
Folder: “read-access”, Group: “Domain Users”, Permission: “Read” and to do that right click -> properties -> sharing>share -> type domain users and share.
  
  
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
Now attempt to access file shares as the normal user.
</p>
<br />

<p>
<img src="https://i.imgur.com/tvziEcm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, navigate to the shared folders by running file explorer (start, run, \\dc-1)
</p>
<br />

<p>
<img src="https://i.imgur.com/R8RxzdU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Try to access the folder that you created. Which folders you can access? Which folders can you create files in?
</p>
<br />

<p>
<img src="https://i.imgur.com/bGl7MVc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go to the DC-1, in Active Directory Users and Groups -> right click mydomain.com -> new -> Organisational Unit -> _SECURITY_GROUPS. Then refresh mydomian.com.

</p>
<br />

<p>
<img src="https://i.imgur.com/KH6jrlI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Inside "_Security_Groups" create a new group called “ACCOUNTANTS”.  
</p>
<br />

<p>
<img src="https://i.imgur.com/Kiem7FW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Go to file explorer and nagivate to where you created the “accounting” folder (path:\\dc-1) you created earlier, set the following permissions: “Read/Write”
  
On the “accounting” folder: Right click -> properties -> sharing -> share -> ACCOUNTANTS -> CLICK add -> read and write -> share -> done -> close.
</p>
<br />

<p>
<a href="https://imgur.com/5rV0Sr6"><img src="https://i.imgur.com/5rV0Sr6.png" title="source: imgur.com" /></a>
</p>
<p>
On Client-1, try to access the Accounting folder. It will fail because the normal user doesn't have permission to access the folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/23QpucQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1 make the normal user a member of the Accountants Security group.

<a href="https://imgur.com/2UWtieH"><img src="https://i.imgur.com/2UWtieH.png" title="source: imgur.com" /></a>
  
Log back in as the normal user in Client-1 and try to access the Accounting share file in \DC-1. Access will still be denied. Not because you don't the required permission but because the permission has not been incorporated fully. At this point, log off as the normal user and log back in to gain access to the "Accounting" folder.

<a href="https://imgur.com/oIARPoh"><img src="https://i.imgur.com/oIARPoh.png" title="source: imgur.com" /></a>

</p>
<br />

We've reach the end of this activity. Hope you enjoyed the tutorial!
