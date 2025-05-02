# Deploying AD
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines installing Active Directory and creating a Domain admin user  <br />


- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Installation and Domain admin user creation Steps</h2>

- Step 1: Install Active Directory and promote as a Domain Controller 
- Step 2: Create a Domain Admin user within the domain
- Step 3: Join Client-1 to the domain

<h2>Install Active Directory and promote as a Domain Controller </h2>

<p>
First, let's start both our devices from the Azure portal, and then let's remote in to DC-1. Once we are in, Server Manager should open up automatically. Click on "Add roles and features." Click next, next, and next. Then, on Server roles, we are going to want to select "Active Directory Domain Services." That will open a new window, and then we will want to select "Add Features." Then next until we get to Confirmation. We will want to select "Restart the destination server automatically if required" and then install. Once that finishes installation, you'll notice that there is a yellow warning sign on the top right. Click on that, then "Promote this server to a domain controller". This will open up a new window, and we will want to select the "Add a new forest" radio button. We will need to give the Root domain name. I am going to do "mydomain.com", but you can do anything you would like here. If you do, make sure you remember it. Click next, then we will enter a password. For the sake of this tutorial, we won't need to enter this information again, so let's just do "Password1". Click next and uncheck DNS options, and then click next. Next, next, next, and install. Now we have made our DC-1 an actual domain controller. This will restart and log us out. When we log back into it using RDP, we cannot log in as just labuser. Because it is a domain controller, we need to specify the context of how we want to log in. When we make this VM, the user accounts exist in a domain, so we have to specify the domain and the user. This will come into play more when Client 1. With Client 1, we can log in as a local account on the computer or as a domain user. There is an image below that should provide a little more context to the situation.
</p>
<br />

![image](https://github.com/user-attachments/assets/d315b4f4-27ac-4ac3-8578-d718188988cd)


<p>
So, for example, if we type in just labuser, that specifies the context as a local user. If we want to log in as a domain user for DC-1, we would specify in RDP as mydomain.com\labuser or whatever you had named your domain. You'll notice below that the first image shows it as a Microsoft account; we need to change this so it is a domain user, which is shown in the 2nd screenshot. (We will be using the same password as before, my case is Azurelab123!
</p>

![image](https://github.com/user-attachments/assets/e770db0d-e27f-4feb-818f-768e81b97a0a)
![image](https://github.com/user-attachments/assets/e9c531bd-25a2-4d4f-8192-f7f26449c835)



<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
