<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources in Azure (Virtual Machines | Windows Server 2022)
- Set Connectivity between Domain Controller (DC) with Client-1
- Install Active Directory
- Create Admin and User accounts in Active Directory
- Join Client-1 to Domain Controller-1
- Set up Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>

<p>

  ![Screenshot 2024-09-04 131803](https://github.com/user-attachments/assets/fd61baea-5a91-4754-bd6b-f39be8e9061a)

![Screenshot 2024-09-04 131757](https://github.com/user-attachments/assets/c0025146-685c-477e-a7c8-b819c6342160)

![Screenshot 2024-09-04 132406](https://github.com/user-attachments/assets/e6cac9c5-32cf-4283-a284-caed00be3306)

![Screenshot 2024-09-04 133626](https://github.com/user-attachments/assets/933794f8-1239-4a01-9b73-9f703dbacc9d)

</p>
<p>
My first step is to create a Resource Group and VMs (DC-1 and Client-1). After creating the Domain Controller VM, I take the following steps:

  - Set DC-1 NIC Private IP address to Static
  - After, I created the Client-1 VM on a Windows 10 using the same Resource Group created for the Domain Controller also known as DC-1.
  - Confirm the connectivity between Client-1 and DC-1:

        - Using Remote Desktop on Client-1 and ping with perpetual ping
        - Login to DC-1: enable ICMPv4 on the local Windows Firewall (view ping success on Client-1 perpetual ping)
</p>
<br />

<p>

![Screenshot 2024-09-04 135755](https://github.com/user-attachments/assets/0a0d463c-bd53-4873-8978-573533abe1f0)


  ![Screenshot 2024-09-04 135736](https://github.com/user-attachments/assets/9e4f8518-c372-4d4f-a4c3-673ff0eec8fe)

![Screenshot 2024-09-04 135839](https://github.com/user-attachments/assets/c9269841-0514-4fdb-956f-1732c038f211)

![Screenshot 2024-09-04 140123](https://github.com/user-attachments/assets/ee12ec9e-b418-46ab-87c5-f0a826ff8638)

</p>
<p>
In this step, I installed Active Directory within our DC-1 by:

  - Logging into DC-1
      - Server Manager --> add roles and features --> select server role: active directory domain services
  - Set up a new forest, ex:mydomain.com restart --> log back into DC-1
  - In Active Directory User and Computers, I created an Organization Unit (OU) called "_EMPLOYEES" and "_ADMINS"
  - Created a sample employee as an admin and added it to the "Domain Admins" Security Group
</p>
<br />

<p>

  ![Screenshot 2024-09-04 142716](https://github.com/user-attachments/assets/5278012a-7393-4378-9cf7-08e074d20ec2)

![Screenshot 2024-09-04 143934](https://github.com/user-attachments/assets/170e1b7e-46d2-41a9-8951-d11f489540ea)

</p>
<p>
For the final steps, I joined Client-1 in the domain that I created and set up a remote desktop for non-administrative users on Client-1. The following are the steps that I took:

  - From the Azure Portal, I set Client-1's DNS settings to the DC-1 Private IP address
  - I restarted Client-1, logged in as the original local admin to join the domain
  - Logged into DC-1 to verify that Client-1 was active on Active Directory Users and Computers


Setup for Remote Desktop for non-admin users on Client-1:

  - Logged into Client-1 as an admin
  - System "Remote Desktop"
  - Allow "Domain Users" group access to remote desktop
  - I can now log into Client-1 as a normal, non-administrative user
</p>
<br />
