<p align="center">
<img src="https://i.imgur.com/2KUrL4H.png" alt="img"/>
</p>

<h1>Network File Shares and Permissions</h1>
This lab builds upon (https://github.com/jszaman/configure-ad) and provides a step-by-step guide to implementing file sharing and permission settings in Azure Virtual Machines.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Active Directory Domain Services
- Server Manager
- Windows Administrative Tools
- Active Directory Users and Computers


<h2>Operating Systems Used </h2>

- Windows 10 (22H2)

<h2>High-Level Steps</h2>

- Log into Cilent-1 (normal user) and DC-1 (jane_admin) VM via Remote Desktop 
- On the C:\ drive of DC-1, create "read-access", "write-access", "no-access", and "accounting" folders
- Give "Domain Users" group "Read" permission to the "read-access" folder
- Give "Domain Users" group "Read/Write" permission to the "write-access" folder
- Give "Domain Admins" group "Read/Write" permission to the "no-access" folder
- Go back to Cilent-1 VM and create a txt. file in the "write-access" folder
- Go back to DC-1 VM and create a txt.file in the "read-access" folder for other users to see
- Create a new organizational unit called "_SECURITY_GROUPS" in DC-1
- Create a new group in "_SECURITY_GROUPS" called "ACCOUNTANTS"
- Give ACCOUNTANTS Security Group "Read/Write" permissions
- Add the user in Cilent-1 to the ACCOUNTANTS Security Group
- Log into the user with ACCOUNTANTS role and observe that the permissions was applied successfully

<h2>Actions and Observations</h2>

<p align="center">
<img src="https://i.imgur.com/QM8c2lU.png" height="80%" width="80%" alt="img"/>
</p>

Let's log into DC-1's VM as jane_admin.

Go to https://portal.azure.com/ and click Virtual machines.

<p align="center">
<img src="https://i.imgur.com/9kpDOrS.png" height="80%" width="80%" alt="img"/>
</p>

Go back to virtual machines in your Azure portal and click DC-1.

<p align="center">
<img src="https://i.imgur.com/pvSb0tR.png" height="80%" width="80%" alt="img"/>
</p>

Copy DC-1 public IP address.

<p align="center">
<img src="https://i.imgur.com/9scInGF.png" height="80%" width="80%" alt="img"/>
</p>

Open Remote Desktop, paste DC-1's public IP address, and click "connect".

<p align="center">
<img src="https://i.imgur.com/In69J19.png" height="80%" width="80%" alt="img"/>
</p>

type "jane_admin" and "Password1" in the username and password box respectively, and click "Ok". 

<p align="center">
<img src="https://i.imgur.com/NA9QeOz.png" height="80%" width="80%" alt="img"/>
</p>

Click "Yes".

<p align="center">
<img src="https://i.imgur.com/FWvuMXc.png" height="80%" width="80%" alt="img"/>
</p>

Go back to your Azure virtual machine and click Client-1

<p align="center">
<img src="https://i.imgur.com/J73jcNu.png" height="80%" width="80%" alt="img"/>
</p>

Copy Client-1 public IP address.

<p align="center">
<img src="https://i.imgur.com/nVjRq04.png" height="80%" width="80%" alt="img"/>
</p>

Open Remote Desktop, paste Client-1's public IP address, and click "connect".

<p align="center">
<img src="https://i.imgur.com/xB40N1G.png" height="80%" width="80%" alt="img"/>
</p>

We will connect to Client-1 VM as a random user from our domain.

First, go back to DC-1, click the Start Menu, collapse "Windows Administrative Tools", and click "Active Directory Users and Computers".

<p align="center">
<img src="https://i.imgur.com/OpDXizl.png" height="80%" width="80%" alt="img"/>
</p>

In "Active Directory Users and Computers", click "mydomain.com" and collapse it. collapse "_EMPLOEES", double-click on any random user, click "Account", and copy that user's username as shown in the image above.

<p align="center">
<img src="https://i.imgur.com/D8f1LmC.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Client-1 VM, click "More choices" > "Use a different account". Paste the random username in the "username box", and type "Password1" in the password box, then click "OK".

<p align="center">
<img src="https://i.imgur.com/p6Qb1ny.png" height="80%" width="80%" alt="img"/>
</p>

Click "Yes" at the prompt

<p align="center">
<img src="https://i.imgur.com/YCNKXFt.png" height="80%" width="80%" alt="img"/>
</p>

You should be connecting to the user's account, as shown in the image above.

<p align="center">
<img src="https://i.imgur.com/MEhy2hP.png" height="80%" width="80%" alt="img"/>
</p>

On C:\ drive of DC-1, we will create "read-access", "write-access", "no-access", and "accounting" folders

Click the Start Menu, and then click File Explorer.

<p align="center">
<img src="https://i.imgur.com/TyQrnCo.png" height="80%" width="80%" alt="img"/>
</p>

Click "This PC", and double-click "Windows (C):".

<p align="center">
<img src="https://i.imgur.com/KWXmowK.png" height="80%" width="80%" alt="img"/>
</p>

On the C:\ drive, right-click on an empty space and click "New" > "Folder".

<p align="center">
<img src="https://i.imgur.com/P4RXROf.png" height="80%" width="80%" alt="img"/>
</p>

Name the folder "read-access". Do the same for "write-access", "no-access", and "accounting".

You should have the following folders shown in the image above.

<p align="center">
<img src="https://i.imgur.com/0nmGvGu.png" height="80%" width="80%" alt="img"/>
</p>

Next, we will give the "Domain Users" group permission to access the newly created folders.

Right-click the "read-access" folder and click "Properties".

<p align="center">
<img src="https://i.imgur.com/0nmGvGu.png" height="80%" width="80%" alt="img"/>
</p>

Click "Sharing" > "Share", type "domain users" in the box, click "Add", and click "Share". Domain Users now have "Read" permission to the "read-access" folder. Click "Done" > "Close". 

<p align="center">
<img src="https://i.imgur.com/urQgdy0.png" height="80%" width="80%" alt="img"/>
</p>

Right-click the "write-access" folder and go to "Properties". Click "Sharing" > "Share", type "domain users" in the box, and click "Add". Select "Read/Write" for the permission level and click "Share".

Click "Done" > "Close". 

<p align="center">
<img src="https://i.imgur.com/eplfBMJ.png" height="80%" width="80%" alt="img"/>
</p>

Right-click the "no-access" folder and go to "Properties". Click "Sharing" > "Share", type "domain admins" in the box, and click "Add". Select "Read/Write" for the permission level and click "Share".

Click "Done" > "Close". 

<p align="center">
<img src="https://i.imgur.com/MzuzVTu.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Client-1 VM and open Filer Explorer. Navigate to the share folders by typing "\\dc-1" on the search bar, as shown in the image above.

<p align="center">
<img src="https://i.imgur.com/P1ggSoj.png" height="80%" width="80%" alt="img"/>
</p>

Double-click the "no-access" folder. 

We got an error message because only Domain Admins have access to the folder.

<p align="center">
<img src="https://i.imgur.com/Q0Xxug5.png" height="80%" width="80%" alt="img"/>
</p>

Double-click the "read-access" folder and you will notice that we can access it

<p align="center">
<img src="https://i.imgur.com/AIiR0hp.png" height="80%" width="80%" alt="img"/>
</p>

Let's create a file in the "read-access" folder and see what happens.

Right-click on an empty space and click "New" > "Text Document".

<p align="center">
<img src="https://i.imgur.com/LCidjpw.png" height="80%" width="80%" alt="img"/>
</p>

We got an error message because we gave Domain Users on "Read" permission.

<p align="center">
<img src="https://i.imgur.com/NWP60EL.png" height="80%" width="80%" alt="img"/>
</p>

Navigate back and double-click the "write-access" folder.

<p align="center">
<img src="https://i.imgur.com/rTyYg5s.png" height="80%" width="80%" alt="img"/>
</p>

Right-click on an empty space and click "New" > "Text Document".


<p align="center">
<img src="https://i.imgur.com/BOI7Z1n.png" height="80%" width="80%" alt="img"/>
</p>

Notice we can create a file, This is because we have "Read/Write" permission for the folder

Name the txt file "hello", and type "hi" in your Notepad.

<p align="center">
<img src="https://i.imgur.com/Q5abfkD.png" height="80%" width="80%" alt="img"/>
</p>

Save the txt file by clicking "File" > "Save".

<p align="center">
<img src="https://i.imgur.com/MUIQFpq.png" height="80%" width="80%" alt="img"/>
</p>

Go back to DC-1 VM and double-click the "read-access" folder.

<p align="center">
<img src="https://i.imgur.com/QKgHDeF.png" height="80%" width="80%" alt="img"/>
</p>

Right-click on an empty space and click "New" > "Text Document".

<p align="center">
<img src="https://i.imgur.com/2k4n1Hx.png" height="80%" width="80%" alt="img"/>
</p>

Name the txt file "You can only read me", and type "hello" in your Notepad. Then save the txt file.

<p align="center">
<img src="https://i.imgur.com/Q0Xxug5.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Client-1 VM and double-click the "read-access" folder.

<p align="center">
<img src="https://i.imgur.com/jSJ0M3X.png" height="80%" width="80%" alt="img"/>
</p>

Double-click the new txt file we created in DC-1. Notice that we can read it but can't create any file in the folder.

This is how file permissions work.

<p align="center">
<img src="https://i.imgur.com/4w4cq9s.png" height="80%" width="80%" alt="img"/>
</p>

Let's create a new organizational unit called "_SECURITY_GROUPS" in DC-1.

Open "Active Directory Users and Computer", right-click "mydomain.com" and click "New" > "Organizational Units".

<p align="center">
<img src="https://i.imgur.com/FaCzSnq.png" height="80%" width="80%" alt="img"/>
</p>

Type "_SECURITY_GROUPS" in the box and click "Ok".

<p align="center">
<img src="https://i.imgur.com/mIKBPE7.png" height="80%" width="80%" alt="img"/>
</p>

As shown in the image above, we now have "_SECURITY_GROUPS" on our lists of OUs. Go ahead and double-click it.

Right-click on an empty space and click "New" > "Group".

<p align="center">
<img src="https://i.imgur.com/EvAQ94S.png" height="80%" width="80%" alt="img"/>
</p>

Type "ACCOUNTANTS" and click "Ok".

<p align="center">
<img src="https://i.imgur.com/l9jDNyT.png" height="80%" width="80%" alt="img"/>
</p>

Open File Explorer and click "Wndows (C:)". Right-click the "accounting" folder and click "Properties".

<p align="center">
<img src="https://i.imgur.com/FVccjsz.png" height="80%" width="80%" alt="img"/>
</p>

Click "Sharing" > "Share", type "ACCOUNTANTS" in the box and click "Add". Select "Read/Write" for Permission Level and click "Share". Click "Done" > "Close".

<p align="center">
<img src="https://i.imgur.com/lrDiCuf.png" height="80%" width="80%" alt="img"/>
</p>

Next, we will Add the user (bibag.pidet) in Cilent-1 to the ACCOUNTANTS Security Group.

Double-click "ACCOUNTANTS" and click "Members" > "Add". Type the name of the user you signed into in Client-1 VM, and click "Check Names" > "Ok" > "Apply" > "Ok".

Minimize DC-1 VM.

<p align="center">
<img src="https://i.imgur.com/0R5eTz2.png" height="80%" width="80%" alt="img"/>
</p>

Log out of Client-1 VM. Permissions will only apply to the user after we log out and log back in.

Open Command Prompt and run the command "logoff".

<p align="center">
<img src="https://i.imgur.com/JxrcJWy.png" height="80%" width="80%" alt="img"/>
</p>

Log back into Client-1 VM with the user you picked via Remote Desktop.

Type "run" in the search box and click "Open".

<p align="center">
<img src="https://i.imgur.com/evSAhyl.png" height="80%" width="80%" alt="img"/>
</p>

Type "\\dc-1" and click "Ok".

<p align="center">
<img src="https://i.imgur.com/a7l5ILT.png" height="80%" width="80%" alt="img"/>
</p>

Double-click the "accounting" folder. Notice we can access the folder

The permissions were successfully applied.






























