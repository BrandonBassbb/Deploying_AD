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

<h2>Installation and Domain Admin User Creation Steps</h2>

- Step 1: Install Active Directory and promote as a Domain Controller 
- Step 2: Create a Domain Admin user within the domain
- Step 3: Join Client-1 to the domain

<h2>Install Active Directory and promote as a Domain Controller </h2>

<p>
First, let's start both our devices from the Azure portal, and then let's log in to DC-1. Once we are in, Server Manager should open up automatically. Click on "Add roles and features." Click next, next, and next. Then, on Server roles, we are going to want to select "Active Directory Domain Services." That will open a new window, and then we will want to select "Add Features." Then next until we get to Confirmation. We will want to select "Restart the destination server automatically if required" and then install. Once that finishes installation, you'll notice a yellow warning sign on the top right. Click on that, then "Promote this server to a domain controller". This will open up a new window, and we will want to select the "Add a new forest" radio button. We will need to give the Root domain name. I am going to do "mydomain.com", but you can do anything you would like here. If you do, make sure you remember it. Click next, then we will enter a password. For the sake of this tutorial, we won't need to enter this information again, so let's just do "Password1". Click next and uncheck DNS options, and then click next. Next, next, next, and install. Now we have made our DC-1 an actual domain controller. This will restart and log us out. When we log back into it using RDP, we cannot log in as just labuser. Because it is a domain controller, we need to specify the context of how we want to log in. When we make this VM, the user accounts exist in a domain, so we have to specify the domain and the user. This will come into play more when Client 1. With Client 1, we can log in as a local account on the computer or as a domain user. The image below should provide a little more context for the situation.
</p>
<br />

![image](https://github.com/user-attachments/assets/d315b4f4-27ac-4ac3-8578-d718188988cd)


<p>
So, for example, if we type in just labuser, that specifies the context as a local user. If we want to log in as a domain user for DC-1, we would specify in RDP as mydomain.com\labuser or whatever you had named your domain. You'll notice below that the first image shows it as a Microsoft account; we need to change this so it is a domain user, which is shown in the 2nd screenshot. (We will be using the same password as before, my case is Azurelab123!)
</p>

![image](https://github.com/user-attachments/assets/e770db0d-e27f-4feb-818f-768e81b97a0a)
![image](https://github.com/user-attachments/assets/e9c531bd-25a2-4d4f-8192-f7f26449c835)


<h2>Create a Domain Admin user within the domain</h2>
<p>
After we log back into DC-1 with mydomain.com\labuser we're going to Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”. If we click start, the bottom left Windows icon, we can see a folder there labeled "Windows Administrative Tools". Click on that, and then let's click on ADUC. We are going to create 2 OUs to future-proof us in a coming activity. Click on the domain to expand it, and then right click on the domain, go down to New, then Organizational Unit

</p>

![image](https://github.com/user-attachments/assets/2fbda71f-4a73-417e-82da-430d4e94be09)

<p>
For name, make sure you enter the name correctly here, so feel free to copy and paste _EMPLOYEES, then we will create a new one labeled _ADMINS. The reason we are naming them at first with an _ is that if we right-click on the domain and hit refresh, it will auto-sort them alphabetically. Now we are going to create an Admin user. Right click _ADMINS and select new, user. Feel free to fill this out, but it should reflect similarly to the one below.
</p>

![image](https://github.com/user-attachments/assets/14908c1b-7071-454c-93e3-8bcc4105dfc3)

<p>
The password should stay consistent for the sake of the lab, so Azurelab123! Let's go ahead and uncheck User must change password at next login and check Password never expires for the sake of the activity. Now this account is not an admin yet, just because we named it admin and put it in the admin folder, we will need to set it as an admin in the built-in security group. So, right click Jane Doe, select add to group, then you can just type in domain admins and hit the check name button, and it should auto add it to domain admins. You'll know if it worked if it becomes underlined. Click ok, now log out of DC-1 and log back in as mydomain.com\jane_admin
</p>

![image](https://github.com/user-attachments/assets/609167a3-83ce-4c18-b29d-733dae569954)

<h2>Join Client-1 to the domain</h2>

<p>
Since the last activity, we have already set Client-1 DNS as the private IP of DC-1. Now we need to log back in as the local user labuser on Client-1 and then add it to the domain. So let's click the start button and then settings. Go into About, then click on Rename this PC (advanced). Click Change, and under domain type out your domain name, and click Ok. Since we set the DNS settings for this computer to DC-1's IP address, it is able to locate the domain controller. It is going to ask us for a username and password to sign in. mydomain.com\jane_admin and the same password Azurelab123!. It will have a welcome message, then it'll ask us to reboot, to which we will say Yes. 
</p>

![image](https://github.com/user-attachments/assets/34f5fcea-1435-49b6-b9af-9a0dd2cda356)

<p>
Let's go ahead and confirm that Client-1 is a part of the domain by going back to DC-1 and clicking the search bar and typing, "Active Directory Users and Computers". Once inside, if we click on the domain, then the Computers folder, you will see Client-1. For organizational purposes, let's create a new OU named _Clients and drag Client-1 into _Clients.
</p>

![image](https://github.com/user-attachments/assets/29d2c871-a512-4513-930b-f575902d0a28)

<p>
  <a href ="https://github.com/BrandonBassbb/Creating_Users"> Next Lab</a>
</p>
<br />
