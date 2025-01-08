
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

- Step 1: Create the Windows and Linux VM in Azure
- Step 2: Establish Traffic b/w the VM's
- Step 3: Observe the effect of NSG rules
- Step 4: Observe various network protocols

<h2>Walkthrough Demonstration</h2>

<h3> Step 1a: Create the Windows VM in Azure </h3>

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

<p>
<img width="851" alt="Screenshot 2025-01-07 at 11 00 54 PM" src="https://github.com/user-attachments/assets/be842a97-4b65-471b-85ce-b40fefdd8f25" />
</p>
<p>
For size, anything with at least 2 vCPU's and 8 GiB of memory will be sufficient. Next, enter in a username and password that you would like to use for the Windows VM.
</p>
<p> Finally, scroll down to the bottom of the page and check the box for licensing, click Review+Create and Create once the review is passed. The Windows VM will now take a few minutes to deploy. </p>
<br />

<h3>Step 1b: Create the Linux VM in Azure </h3>
<p>
<img width="835" alt="Screenshot 2025-01-07 at 11 02 26 PM" src="https://github.com/user-attachments/assets/41a917cd-1b2e-4489-8bcb-429dd1780120" />
</p>
<p>
Going back to the Virtual Machines home page, create another virtual machine. Be sure that it is under the same Resource Group as the Windows VM. 
</p>
<p> Name this VM to indicate that it is the Linux VM, pick the same region as the Windows VM, and leave the zone selection as is unless prompted by Azure. </p>
<br />

<p>
<img width="839" alt="Screenshot 2025-01-07 at 11 04 11 PM" src="https://github.com/user-attachments/assets/186ec692-9fc4-418c-a13c-ac4735f504b5" />
</p>
<p>
For the image, please select Ubuntu Server 22.04. 2 vCPU's and 8Gib memory will suffice. </p>
<br />


<p>
<img width="838" alt="Screenshot 2025-01-07 at 11 05 01 PM" src="https://github.com/user-attachments/assets/bf019ab9-ea77-4d05-b4a6-814a92e0b083" />
</p>
<p>
  Deselect SSH public key and select password instead. Enter in a username and password for the Linux VM. Preferably the same one as the Windows VM for ease of memory.
</p>
<br />


<p>
<img width="840" alt="Screenshot 2025-01-07 at 11 07 44 PM" src="https://github.com/user-attachments/assets/c6017b09-d820-481a-88b0-26dd70d4badb" />
</p>
Scroll to the top and select the Networking tab. Make sure that this VM is in the same Virtual Network as the Windows VM. There may have been a Virtual Network that was created with the Windows VM and this will be one of the options for the Linux VM. In this step, be sure to select the same Virtual Network that the Windows VM is on. In this case, the Windows VM-net is the only option so it will be the same network.
</p>
<p> Finally, click Review+Create and create once the review has passed. It will take a few minutes for the Linux VM to deploy.</p>
<br />

<p>
<img width="1165" alt="Screenshot 2025-01-07 at 11 28 44 PM" src="https://github.com/user-attachments/assets/b1ad41b7-709a-468e-bc40-0f9035fc14ee" />
</p>
<p>
  Once both VMs are deployed, they should appear in the Virtual Machines homepage. To confirm that they are on the same Virtual Network, click on each Virtual Machine and you will be brought to their configurations. From there you can confirm their Virtual Networks are the same.
</p>
<br />



