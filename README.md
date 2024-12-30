<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" alt="Permissions Photo"/>
</p>

<h1>Understanding File Permissions</h1>
This lab focuses on file permissions and shares in the context of an Active Directory domain. File permissions and shares are key in a business setting to make sure users have the appropriate permissions and access to files they need. This is building up from a previous lab where I have a client joined to my domain ernestotest.com. I am logged in as Jane Doe (an admin account) on the domain controller VM and as a normal user on the client VM. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/bUjobDC.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/lz1DMos.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
In order to set permissions to folders and files, we need to create the folders to share. While logged in to the domain controller VM as an admin, create the folders. I have created 4 appropriately named folders to set permissions to on the C:\ drive. To share a folder and assign permissions, open the folder's Properties and click on Share under the Sharing tab. You can specify people on the network to share with and assign appropriate permissions. I set the following permissions for the folders (the accounting folder will be changed later):

Domain Users can Read the read-access folder and they have Read/Write permissions on the write-access folder.
Domain Admins have Read/Write access to the no-access folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/kWrpLFE.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
On the client VM, navigate to the shared folders through the following path in File Explorer: \\dc-1. Notice how some folders cannot allow you to add files, but only view them. One does not allow access at all. This is because as a Domain User, permissions for the folder are tied to the respective Security Group and the folder's own set permissions for users within that Security Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/NgM0CcI.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/I4k9T2J.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
Next, we will make a new Security Group and assign appropriate permissions to the accounting folder. On the domain controller, have the Active Directory Users and Computers panel open. Create a new Group called ACCOUNTANTS. After creating the new Group, go to the accounting folder and assign permissions to the folder so the ACCOUNTANTS Group has Read/Write permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/xev1Svv.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/SHotVB2.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
The user cannot access the accounting folder because they are not part of the ACCOUNTANTS Security Group. Log off the client so that the permissions are in place by the time the client is logged into again. On the domain controller, open the ACCOUNTANTS Properties on Active Directory Users and Computers. In the Members tab, add the respective user. In my case, it is bon.rovej. Upon logging into the client, bon.rovej is now able to open the accounting folder because they are part of ACCOUNTANTS.
<br />

<h2>Lessons Learned </h2>

This lab made me understand how file permissions work in the context of Windows/Active Directory. In a real setting, I might have to set permissions so that people can only access what they need to in order to complete their work. It is not necessary to give more permissions than what is needed.
