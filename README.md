<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
The purpose of this project is to explain the process of setting up Active Directory using the Azure platform including connection to an endpoint and user creation.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Remote Desktop and a laptop that is capable of  using Remote Desktop Protocol
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2019
- Windows 11 (23H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory & Promotion To Domain Controller
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create an additional users and attempt to log into client-1 with one of the users


<h2>Prerequisites</h2>

- Microsoft Azure Subscription
- Creation of the following
	- Resource Group
	- Virtual Machines (Windows Server 2019 & Windows 11 Pro
	- Virtual Networks & Subnets
- Both Virtual Machines are to be set up under the same virtual network


<h2>Deployment and Configuration Steps</h2>

Environments & Technologies Used
- Microsoft Azure (Virtual Machines)
- Active Directory Domain Services
- Remote Desktop
- Windows Powershell

<h3>Step 1 - Setup Resources in Azure</h3>

- Resource Group - rg-lab-03
- Virtual Machine 1 (Windows Server): DC-01
- Virtual Machine 2 (Windows 11 pro client): CL-01
- Initial username: testadmin
- Network: provided by platform or can be suggested

Resource Group creation

![image](https://github.com/user-attachments/assets/72ff0de4-d2e4-498e-9dba-0bb1356a3023)

Virtual Machine Setup

![image](https://github.com/user-attachments/assets/0ec48670-664c-4e2e-8ae8-9518c65023e3)

![image](https://github.com/user-attachments/assets/196d4b22-bf0c-4dc3-b792-7eb953cf4831)

![image](https://github.com/user-attachments/assets/8fde6ed0-51ce-4ffa-9ea4-8f26f395ffb9)

![image](https://github.com/user-attachments/assets/1127747e-5a70-4f61-9774-255e242ff5a3)

Click Next

Disk field has already being filled based on the settings in the previous tab, but amend if required

![image](https://github.com/user-attachments/assets/f2b098a7-85c9-49a9-b17c-1bdf78589541)

Networking Tab

![image](https://github.com/user-attachments/assets/a78c4f60-dcad-4b0b-a1f1-a3e1f1381f7d)


Select Create new for the Virtual network

![image](https://github.com/user-attachments/assets/54995373-e85d-4150-b718-ab79985f7d05)


Then click Review and Create

The server will now be created and deployed

![image](https://github.com/user-attachments/assets/24922bf2-fb8d-49f5-93e8-2318150d3514)


NOTE: As part of this, the "NetworkWatcher RG" resource group is also automatically created in addition to the Network Interface, Network Security Group, Public IP Address.

![image](https://github.com/user-attachments/assets/1eeabf93-c84b-46c8-bc61-6216161c6a40)


Creating the Client

![image](https://github.com/user-attachments/assets/883dd424-05ec-45b0-a2dc-949c5d7a7065)

![image](https://github.com/user-attachments/assets/83abd07f-d4eb-4866-8c36-db53ba6e7394)


Disk

![image](https://github.com/user-attachments/assets/807d4114-c452-4ad2-9b44-edee300fd6d9)

Network

Ensure the virtual network is the same as the windows server created previously

![image](https://github.com/user-attachments/assets/17e1738e-ef7d-40b4-bb6a-306c9867b73c)

Review & Create


Resource group post creation
![image](https://github.com/user-attachments/assets/03e947ec-a595-41ba-be07-b34c01368505)


<h3>Step 2 - Ensure Connectivity between the client and Domain Controller</h3>

Required

-Public IP address and private IP address of the both server and client

-Server IP addresses

Select the Virtual Machine DC-01

![image](https://github.com/user-attachments/assets/c04f1b8b-f1c0-4893-bf51-c914680cc8a7)

Client IP Addresses
Select the Virtual Machine CL-01

![image](https://github.com/user-attachments/assets/a8dfbe34-18f2-4914-a44d-88b2094f795a)



Using the remote desktop tool, log into both client and server

![image](https://github.com/user-attachments/assets/35a5c4ae-9149-4812-a653-439cebee7e55)

Connection to server completed

![image](https://github.com/user-attachments/assets/1c32a715-2f21-4465-9339-c79acac08f9d)

Connection to Client via remote desktop

![image](https://github.com/user-attachments/assets/1c65a629-4880-4f35-81d2-bdeffe08c2c2)

Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)

To enter the  Windows Powershell (Admin), right click on the start button and select Windows Powershell (Admin)

![image](https://github.com/user-attachments/assets/8724f309-4fd9-42df-96d8-4a92f8eee00f)

Pinging the client CL-01  private ip address with a pepetual ping
- ping -t 10.0.0.5

![image](https://github.com/user-attachments/assets/3552d66c-5ac6-4612-90e4-8bbe4bb64633)

Ping unsuccessful due to ICMPv4 protocol being deactivated

Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall, repeat on the client as well

Sort protocol by ICMP and view the Core Networking Diagnostics highlighted below

![image](https://github.com/user-attachments/assets/acfb0c92-5b8c-4690-ba18-94b8b1a0b224)

Enable rule for both by highlighting and right-clicking and selecting enable rule

Check back at Client-1 to see the ping succeed

You can see the ping become successful once the rules have been enabled

<h3>Step 3 - Install Active Directory & Promotion To Domain Controller</h3>

Active Directory Installation 

While in Server Manager, click Add roles and features

![image](https://github.com/user-attachments/assets/8072e168-a843-4658-9904-9ff2bb5f7f84)

Click Next

![image](https://github.com/user-attachments/assets/423d1906-7069-4a4b-8cf8-c26546d60e28)

Click Next

![image](https://github.com/user-attachments/assets/a1c3689b-6412-4afa-a58c-691b1a8783d9)

Click Next, Select DC-01

![image](https://github.com/user-attachments/assets/5e059529-e87a-4ed4-a241-2599f98346a1)

Click Next, Select Active Directory Domain Services

![image](https://github.com/user-attachments/assets/dd3a2873-54db-4d24-b811-bfff03b0bd4a)

On the next screen, click Add features and then Next

![image](https://github.com/user-attachments/assets/b201d4b1-4249-464b-af48-7c5fa0b604ee)

Click Next

![image](https://github.com/user-attachments/assets/1111f65a-a764-4269-944b-9ae20c133793)

Click Install

![image](https://github.com/user-attachments/assets/c97be109-e77e-4032-a469-9c79439c279c)

Once complete, there is a yellow flag in server manager

![image](https://github.com/user-attachments/assets/2a4d334d-bbb0-4fdd-8660-57054c81337a)

Promote as a DC: Setup a new forest as testdomain.com 

![image](https://github.com/user-attachments/assets/331a952c-5d5d-495e-ad5d-2f850521350b)

Select Add a new forest and specify the root domain name and click next

![image](https://github.com/user-attachments/assets/e686a2a2-94b4-4cff-a2b2-484eeeda8ec8)

Enter the password and click next

![image](https://github.com/user-attachments/assets/b8f608ea-0483-45ff-bb2a-8949960f7f07)

Click Next

![image](https://github.com/user-attachments/assets/ac85c0e0-7436-4d34-8ca6-cb9a51eaec8c)

Click Next

![image](https://github.com/user-attachments/assets/c55c075a-82f0-4283-b517-19cb40b5a5b6)

Click Next

![image](https://github.com/user-attachments/assets/0c0af147-2bb7-4c62-98e1-fcb4169e1740)

Click Next

![image](https://github.com/user-attachments/assets/be60eec1-da43-4f6e-ada4-f543132edb2d)

Click Next

![image](https://github.com/user-attachments/assets/9298d8cf-2a96-40a3-8c75-48fe909987c0)

Click install

You may be signed out as the system will restart.


Restart and then log back into DC-1 as user: testdomain.com\testuser
