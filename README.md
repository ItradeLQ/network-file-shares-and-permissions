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
- Windows Server 2022


<h2>File Shares and Observation</h2>
</p>
<p>
Login to DC-1 as your Domain Admin account. My case it's (mydomain.com\jane_admin) and create folders with varying sharing permissions.
  
Login to Client-1 as a normal user (mydomain\<normaluser>)
  
  
On DC-1, go to the c:\ drive and create four folders “read-access”, “write-access”, “no-access”, “accounting”  
<p>
<a href="https://imgur.com/zlXLhV9"><img src="https://i.imgur.com/zlXLhV9.png" title="source: imgur.com" /></a>
</p>
<p>


</p>
<br />
Set the following permissions, and share the folder for the “Domain Users” group.
  
  
Folder: “read-access”, Group: “Domain Users”, Permission: “Read” and to do that right click -> properties -> sharing>share -> type domain users and share.
  
  
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”

  
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”

Skip the accounting folder for now.
<p>
<a href="https://imgur.com/k1zwjDz"><img src="https://i.imgur.com/k1zwjDz.png" title="source: imgur.com" /></a>
</p>
<p>



</p>
<br />
Choose a normal user from the list of names created, from the script in Configure Active Directory tutorial. 
Login to Client-1. Once logged in, open file explorer and type (\\dc-1), to view the shared folders in the network.<p/>

<p>
<a href="https://imgur.com/m7qIsEX"><img src="https://i.imgur.com/m7qIsEX.png" title="source: imgur.com" /></a>
</p>
<p>

</p>
<br />
Try to access the folder that you created. Which folders you can access? Which folders can you create files in? 
In the write-access folder, you can create a file.
<p>
<a href="https://imgur.com/wE5S9Yi"><img src="https://i.imgur.com/wE5S9Yi.png" title="source: imgur.com" /></a>
</p>
<p>

</p>
<br />
Open up DC-1, navigate to the network path with the folders, and create a text file, you can only read me.
Now return to Client-1 as the normal user, go to the file explorer path: (\\dc:), and interact with the file. 
Try deleting the file and what happens? </p>

<a href="https://imgur.com/7zFp6KP"><img src="https://i.imgur.com/7zFp6KP.png" title="source: imgur.com" /></a>


</p>
<br />
Go to the DC-1, in Active Directory Users and Groups -> right click mydomain.com -> new -> Organisational Unit -> _SECURITY_GROUPS. Then refresh mydomian.com.</p>
<p>
<a href="https://imgur.com/b2wuhqo"><img src="https://i.imgur.com/b2wuhqo.png" title="source: imgur.com" /></a>
</p>
<p>


</p>
<br />
Within the  "_Security_Groups", add a new group name "ACCOUNTANTS". </p>
<a href="https://imgur.com/05AmZ9I"><img src="https://i.imgur.com/05AmZ9I.png" title="source: imgur.com" /></a>
</p>
<p>


</p>
<br />
Return to DC-1 to update the sharing permissions to the accounting folder.

Go to file explorer and navigate to where you created the “accounting” folder (path:\\dc-1) you created earlier, set the following permissions: “Read/Write”
  
On the “accounting” folder: Right click -> properties -> sharing -> share -> ACCOUNTANTS -> CLICK add -> read and write -> share -> done -> close.

<a href="https://imgur.com/dea6Znn"><img src="https://i.imgur.com/dea6Znn.png" title="source: imgur.com" /></a>
</p>
<p>

</p>
<br />
On Client-1, try to access the Accounting folder. It will fail because the normal user doesn't have permission to access the folder.
<p>
<a href="https://imgur.com/5rV0Sr6"><img src="https://i.imgur.com/5rV0Sr6.png" title="source: imgur.com" /></a>
</p>
<p>

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
