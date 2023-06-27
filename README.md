# azure-network-protocols

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group and 2 Virtual Machines (VM) in Microsoft Azure. One with Windows 10 (VM1) and the other with Ubuntu Server 20.04 LTS (VM2)
- Use Remote Desktop (RDP) to VM1 and install "Wireshark".
- Use Wireshark and PowerShell to Observe Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
  - Add new Inbound Rules to Deny/Allow ICMP traffic.
- Bonus: How to Display and Flush DNS.

<h2>Actions and Observations</h2>

1)Create Resource Group and  2 Virtual Machines

 - In the Search Box at the top header, type and select "Resource Group".
   - If "Resource Group" is already listed on the front page, then you can simply click on it, rather than manually searching.
 - Click "Create" then name Resource Group whatever you want to but for this example use (VMlab)

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - In the Search Box at the top header, type and select "Virtual machines".
   - If "Virtual machines" is already listed on the front page, then you can simply click on it, rather than manually searching.
 - Click "Create", then select "Azure virtual machine".

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Name your Virtual Machine anyway you want for this example use (VM1).
 - Change the Region that best suites your location  for this example uses ( (US) West US 3).
 - Change the Image to a Windows OS (this example uses Windows 10 Pro, version 22H2 - x64 Gen2).
 - Make sure the Size is adequate enough to run this server for this example use (Standard_E2s_v3 - 2 vcpus, 16 GiB memory).
 - Create a username and password of your choice for this example use (labuser).
 - Skip everything else and click "Review + create".
   - IF there is a Licensing Checkbox at the end, make sure that is CHECKED!
 - If Validation passed, click "Create".

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

Essentially repeat the same steps for creating the other Virtual Machine (VM2), but using Ubuntu (Linux):

  - Set the Resource Group to the same as VM1, for this example use (VMlab).
  - Name your Virtual Machine anyway you want but for this example use (VM2).
  - Change Image to Ubuntu/Linux for this example (Ubuntu Server 20.04 LTS - x64 Gen2)
  - Keep the size the same as the Windows VM, (Standard_E2s_v3 - 2 vcpus, 16 GiB memory).
  - Change the Authentication type to "Password", and create any username but for this example use (labuser).
  - Once done, press "Next" until you reach "Networking" (or simply click the Networking tab").

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>



<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
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
