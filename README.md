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

<img src="https://i.imgur.com/59g5dAz.png.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>

 - In the Search Box at the top header, type and select "Virtual machines".
   - If "Virtual machines" is already listed on the front page, then you can simply click on it, rather than manually searching.
 - Click "Create", then select "Azure virtual machine".

<img src="https://i.imgur.com/q7smLsM.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

 - Name your Virtual Machine anyway you want for this example use (VM1).
 - Change the Region that best suites your location  for this example uses ( (US) West US 3).
 - Change the Image to a Windows OS (this example uses Windows 10 Pro, version 22H2 - x64 Gen2).
 - Make sure the Size is adequate enough to run this server for this example use (Standard_E2s_v3 - 2 vcpus, 16 GiB memory).
 - Create a username and password of your choice for this example use (labuser).
 - Skip everything else and click "Review + create".
   - IF there is a Licensing Checkbox at the end, make sure that is CHECKED!
 - If Validation passed, click "Create".

<img src="https://i.imgur.com/pyRIFyC.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/M5IYZQN.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

Essentially repeat the same steps for creating the other Virtual Machine (VM2), but using Ubuntu (Linux):

  - Set the Resource Group to the same as VM1, for this example use (VMlab).
  - Name your Virtual Machine anyway you want but for this example use (VM2).
  - Change Image to Ubuntu/Linux for this example (Ubuntu Server 20.04 LTS - x64 Gen2)
  - Keep the size the same as the Windows VM, (Standard_E2s_v3 - 2 vcpus, 16 GiB memory).
  - Change the Authentication type to "Password", and create any username but for this example use (labuser).
  - Once done, press "Next" until you reach "Networking" (or simply click the Networking tab").

<img src="https://i.imgur.com/xpNePyM.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/jAdjy6d.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

  - Make sure that the Virtual Network is setup the same as Windows (VM1), for this example were using (VM1-vnet).
  - Set the Public IP to whatever it has automatically assigned to you (might have to confirm the selection).
  - Then press "Review + create".
  - If Validation passed, click "Create".

<img src="https://i.imgur.com/Xd4M5jd.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

2)Connecting to VM1 and Installing Wireshark

 - From Azure Portal, go to VM1's Overview page and copy the Public IP address.
 - Press the Windows Key/Button, then type in "Remote Desktop Connection" (RDP).
 - Input the IP into RDP and click "Connect".
 - Enter the login credentials for VM1, then click "OK".
 - When the Certificate Error prompt appears, just click "Yes".
 - As it boots up, you can disable all privacy settings when prompted, then hit "Accept".

<img src="https://i.imgur.com/M8BtMwY.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xXiiQo4.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

 - On VM1, open Microsoft Edge (or any internet browser), then go to the Wireshark download page.
   - You can simply Google Search it, or type "www.wireshark.org/download.html"
 - Click on "Windows Intel Installer" to start downloading the executable.
 - Once downloaded, click "Open file" to run the .exe file (you can also find this inside your Downloads folder within File Explorer).

<img src="https://i.imgur.com/s5OmrOY.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

 - The installation prompt will appear, hit "Next".
 - When the installation prompt appears, leave everything by default and keep pressing "Next" until you start Installing.
 - If any agreement prompts appear during installation, just hit "I Agree" and click install (without checking anything).
 - After all installations are complete, click "Finish".

<img src="https://i.imgur.com/LOl5Nrs.png.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

3)Observe ICMP Traffic using Wireshark

 - Open the wireshark app by clicking the windows button and typing in "Wireshark".
 - Once open click the first button at the top (blue shark fin), to start capturing activity on the VM1
   - You can see there is activity constantly going in the background of the VM, despite you not doing anything.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Click in the search box above, type in "ICMP", then press ENTER to confirm.
   - You should then see all boxes blank this is due to having no activity under the ICMP protocol.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Minimize (VM1)and go back to the Azure Portal.
 - Go to VM2's Overview page and copy the PRIVATE IP address for this example use (10.0.0.5).
 - Return to VM2, press the Windows Key/Button and seach for "CMD" or "PowerShell".
 - Type in ping -t <Private IP address> for this example we would use (ping -t 10.0.0.5).
   - On Wireshark, you should be able to see the results of packets being perpetually pinged sent and received.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

While that is infinitely pinging, we'll try to deny those packets and observe what happens next:

 - Minimize the VM1 and go back to the Azure Portal.
 - In the Search Box at the top header, type and select "Network Security Groups".
 - Click on "VM2-nsg".
 - Go to "Inbound security rules".
 - Click "Add"

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Change the protocol to "ICMP".
 - Change the Action to "Deny" (we are trying to stop any packet requests from VM1).
 - Change the Priorty to a lower number than the lowest one already set for this example use (200).
 - You can change the name if you desire, but for this example use (DENY_ICMP_PING_).
 - Click "Add".
 - Wait for a bit,for it to take effect, but return to VM1 and observe the requests time out.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Now that we've observed the denial of packets, let's try to allow it again, however, instead of deleting the added rule, we can simply edit the Action to "Allow".

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Once done, you can press Control+C to stop the pinging in PowerShell.

4)Observe SSH Traffic using Wireshark

 - From Wireshark, type "SSH" in the search bar and press ENTER (there should be no activity).
   - A more direct way is typing "tcp.port == 22".

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 -  From PowerShell, type (ssh labuser@10.0.0.5)
 -  When it asks if you want to continue connecting, just type "yes", then ENTER.
 -  It will then ask you for the password for VM2.
 -  When typing the password, there will be no visual indicator of you typing, but inputs are being read.
 -  Once you think you typed your password correctly, press ENTER.
 -  You should then see the VM2's username, but colored Green.
 -  Because VM2 uses Ubuntu, commands must now be in Linux format.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Now accessed to VM2, from PowerShell, type "id", then ENTER.
   - This will give you the indentity group information for VM2's user.
 - Observe the new traffic on Wireshark.
 - Type in "exit" to close the linked connection and return to VM1's control.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

5)Observe DHCP, DNS, and RDP Traffic using Wireshark

 - From Wireshark, search for "dhcp", then ENTER (there should be no activity).
 - From PowerShell, type ipconfig /renew, then ENTER.
   - The virtual machine will briefly lose connection, but will return shortly.
 - Observe the new activity in Wireshark.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

Next to observe DNS traffic activity:

 - From Wireshark, search for "dns", then ENTER (there should be a lot of traffic).
   - A more direct way is typing "udp.port == 53".
 - Clear the boxes by pressing the "Restart current capture" button (green shark fin).
 - From PowerShell, type nslookup www.google.com, observe the new activity in Wireshark.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

Finally to observe DNS traffic activity:

 - From Wireshark, search for "rdp", then ENTER (there should be a lot of traffic, non-stop)
   - A more direct way is typing "tcp.port == 3389".
     -  Because we are currently using RDP to run the virtual machine, anything and everything done while in the VM is captured into Wireshark.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

6)BONUS: Display and Flush DNS

 - From PowerShell, type ipconfig /displaydns, the ENTER
   - You should see many domain names to other websites with information below them.
   - The saved data here allows your system to remember information a website that was already visited without and have access to it without making requesting for new info.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

 - Type ipconfig /flushdns, then ENTER
   - This will essentially delete all entries within the cache, making your system require to make requests from the site for information as if were visiting the first time, which is then saved in the cache.
 - Type ipconfig /displaydns to see how everything has been cleared out and nothing to display.

<img src="https://i.imgur.com/DJmEXEB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

!!! Complete !!! Delete all Resource Group.
