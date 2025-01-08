
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Inspecting Traffic Between Azure Virtual Machines & Network Security Groups</h1>
In this walkthrough, we will observe various forms of network traffic to and from Azure Virtual Machines with Wireshark as well as see how Network Security Groups affect traffic. This project is done on a Macbook Pro <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Windows App)
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>
- MacOS 
- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create the Linux and Windows VM in Azure
- Step 2: Establish Traffic b/w the VM's
- Step 3: Observe the effect of NSG rules
- Step 4: Observe various network protocols

<h2>Walkthrough Demonstration</h2>

<p>
<img width="1438" alt="Screenshot 2025-01-07 at 10 53 29 PM" src="https://github.com/user-attachments/assets/3a014396-b9ae-4e68-a959-70d7cd2d235f" />
</p>
<p>
Upon creating an account with Microsoft Azure, navigate to Virtual Machines (VM) in the search bar and begin creating your Windows and Linux VMs.
</p>
<br />

<p>
<img width="985" alt="Screenshot 2025-01-07 at 10 54 34 PM" src="https://github.com/user-attachments/assets/c06a5e8a-8390-4c5f-815c-11e0d36fc389" />
</p>
<p>
Begin by creating a new resource group (RG) to contain our virtual machines. This RG will be created with our VM. Assign it a name and remember to put your VMs under this resource group.
</p>
<p>Region selection can be selected based upon your geographical region. For the sake of consistency, pick the same region for everything you create.</p>
<br />

<p>
<img width="859" alt="Screenshot 2025-01-07 at 11 00 32 PM" src="https://github.com/user-attachments/assets/46638387-4be9-4f0e-84f4-727c9688d545" />
</p>
<p>
We will first create our WindowsVM so give the VM a name that will help you identify it as the Windows VM. After selecting the proper region, leave the zone as is unless prompted by Azure to change it, and be sure to select Windows 10 Pro for the image. (DO NOT select Windows Server.)
</p>
<br />
