<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Creation of the Domain Controller and Client VM
- Ensuring Connectivity
- Active Directory Installation and Configuration
- User and Computer Management

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure:</h3>
<ul>
    <li>I created a Domain Controller VM named “DC-1” using Windows Server 2022.</li>
    <li>Note was made of the Resource Group and Virtual Network (Vnet) that were automatically created.</li>
    <li>I set the Domain Controller’s NIC Private IP address to be static.</li>
    <li>A Client VM named “Client-1” was created using the same Resource Group and Vnet as in step 1.</li>
    <li>I ensured both VMs were in the same Vnet, confirmed by checking the topology with Network Watcher.</li>
</ul>

<h3>Ensure Connectivity between the client and Domain Controller:</h3>
<ul>
    <li>Logged into Client-1 with Remote Desktop and executed a perpetual ping to DC-1’s private IP address.</li>
    <li>On the Domain Controller, I enabled ICMPv4 in the local Windows Firewall.</li>
    <li>Confirmed successful ping responses back at Client-1.</li>
</ul>

<h3>Install Active Directory:</h3>
<ul>
    <li>Logged into DC-1 and initiated the installation of Active Directory Domain Services.</li>
    <li>Promoted the server as a Domain Controller, setting up a new forest named "mydomain.com".</li>
    <li>After the installation, I restarted DC-1 and logged back in as user: mydomain.com\labuser.</li>
</ul>

<h3>Create an Admin and Normal User Account in AD:</h3>
<ul>
    <li>In Active Directory Users and Computers (ADUC), I created an Organizational Unit (OU) called "_EMPLOYEES".</li>
    <li>Created a new OU named "_ADMINS".</li>
    <li>Added a new employee named “Jane Doe” with the username “jane_admin”, using the same password.</li>
    <li>Assigned jane_admin to the “Domain Admins” Security Group.</li>
    <li>Logged out from DC-1 and logged back in as “mydomain.com\jane_admin” to use jane_admin as my admin account from then on.</li>
</ul>

<h3>Join Client-1 to the domain (mydomain.com):</h3>
<ul>
    <li>Set Client-1’s DNS settings in the Azure Portal to the DC’s Private IP address.</li>
    <li>Restarted Client-1 from the Azure Portal.</li>
    <li>Logged into Client-1 as the original local admin (labuser) and joined it to the domain. The computer restarted as part of the process.</li>
    <li>Logged into the Domain Controller and verified that Client-1 appeared in ADUC inside the “Computers” container at the root of the domain.</li>
    <li>Created a new OU named "_CLIENTS" and moved Client-1 into it for organizational purposes.</li>
</ul>

<h3>Setup Remote Desktop for non-administrative users on Client-1:</h3>
<ul>
    <li>Logged into Client-1 as mydomain.com\jane_admin and opened system properties.</li>
    <li>Enabled Remote Desktop and allowed “domain users” access to it.</li>
    <li>Configured Client-1 to allow login as a normal, non-administrative user.</li>
</ul>

<h3>Create Additional Users and Test Login:</h3>
<ul>
    <li>Logged into DC-1 as jane_admin and opened PowerShell_ise as an administrator.</li>
    <li>Created and ran a script to generate multiple user accounts in AD.</li>
    <li>Observed the newly created accounts in ADUC, placed in the appropriate OU.</li>
    <li>Attempted to log into Client-1 with one of the new user accounts to test the setup.</li>
</ul>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Active Directory Configuration"/>
</p>
<p>
    Completing these steps ensured the successful deployment and configuration of an Active Directory environment in Azure, demonstrating how on-premises strategies can be adapted for cloud platforms.
</p>
<br />

<!-- Footer or additional notes -->

