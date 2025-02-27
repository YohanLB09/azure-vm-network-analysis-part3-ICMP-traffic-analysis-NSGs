# Part-3

# Azure VM Network Analysis - Part 2 - ICMP Traffic Analysis

In this tutorial, we will observe ICMP network traffic between two Azure Virtual Machines using Wireshark and PowerShell.

<p align="center">
<img src="https://i.imgur.com/mbLUNMY.png" alt="Traffic Examination"/>
</p>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop 
- PowerShell 
- Network protocol (ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro, version 22H2
- Ubuntu Server 22.04 LTS

<h2>High-Level Steps</h2>

- Step 1: Ping the Linux Virtual Machine
- Step 2: Disable ICMP incoming traffic for the Linux Virtual Machine
- Step 3: Observe the ICMP traffic
- Step 4: Re-enable ICMP incoming traffic for the Linux Virtual Machine
- Step 5: Observe the ICMP traffic
- Step 6: Prepare for Part 4 (Final Part)

<h2>Actions and Observations</h2>

<h3>Step 1: Ping the Linux Virtual Machine</h3>

<p>
<img src="https://i.imgur.com/yNra2NP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-From PowerShell, initiate a perpetual/non-stop ping from your Windows 10 VM to your Linux VM like so: "ping 10.0.0.5 -t" (your Linux VM private IP address may be different).

-In Wireshark, restart the packet capture and let it run at the same time as the perpetual ping.
</p>
<br />



<h3>Step 2: Disable ICMP incoming traffic for the Linux Virtual Machine</h3>

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-While leaving the perpetual ping and packet capture running, go back to Azure and select your Linux VM.

-Under "Networking", click on "Network settings", then click on the link under "Network security group". It will open the Linux VM Network Security Group (NSG), which acts like a firewall for the Linux VM.
</p>
<br />



<p>
<img src="https://i.imgur.com/jtXUYuE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Paste your Windows VM Public IP address in Remote Destop Connection and click on "Connect".
  
-In the new pop-up window, enter your Windows VM password (the one created in Part 1) and click on "OK" to initiate the session.
</p>
<br />



<p>
<img src="https://i.imgur.com/XsmfHbI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-After inserting your credentials and pressing "OK", you should see this pop-up window appearing on your screen. Don't worry, this is normal as the remote computer (the Windows VM) is using a self-signed Remote Desktop Protocol (RDP) certificate, which is not automatically trusted by your local machine. You can go ahead and press "Yes" to connect to your VM since we have created it in Azure.
</p>
<br />



<p>
<img src="https://i.imgur.com/Vtkde9D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Once the session is initated, you should see this loading screen appearing. This indicates that you are officially connected to your Windows VM. 
  
-Additionally, before reaching the desktop, you may be asked to configure certain features/options. These are not important for the purpose of this lab so you can leave them as disabled or manually disable them.
</p>
<br />




<h3>Step 2: Install Wireshark</h3>

<p>
<img src="https://i.imgur.com/sqtRiCZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Use the Microsoft Edge app on the desktop and go to www.wireshark.org.
  
-Click on "Download".
</p>
<br />



<p>
<img src="https://i.imgur.com/ZgCC1Gq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Download the Windows x64 installer version. 
  
-Once the download is completed, click on "Open file" and you should see the installation pop-up window appearing. 

-Follow along the Wizard while leaving all the default configuration as they are and complete the installation process.
</p>
<br />




<h3>Step 3: Filter for ICMP traffic and observe</h3>

<p>
<img src="https://i.imgur.com/9KIg9Xj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Type Wireshark in the Desktop Seach bar and click on "Open".
  
-In Wireshark, click on "Ethernet" to select the Ethernet network adapter, it should become highlighted.
  
-Click on the shark fin on the upper left to start the packet capture.
</p>
<br />



<p>
<img src="https://i.imgur.com/jEjetaJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-You will notice a high amount of traffic occurring. This is expected due to normal network operations, background processes, and Azure-related activity. 
  
-While the packet capture is still running, type "icmp" in the search bar and press "Enter" to filter for ICMP traffic. You will observe that there are no such traffic currently happening which is normal since no device has tried to initiate a ping request to your Windows VM or vice-versa.
</p>
<br />



<p>
<img src="https://i.imgur.com/WjzlWrP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-While leaving the packet capture running in Wireshark, go back to Azure, select your Linux VM, click on "Network settings" and copy your Linux VM Private IP address.
</p>
<br />



<p>
<img src="https://i.imgur.com/42TAeOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Type "Windows PowerShell" in the Desktop Search bar and click on "Open".

-In PowerShell, initiate a ping request from your Windows VM to your Linux VM like so: "ping 10.0.0.5" (your Linux VM Private IP address may be different than this one). 

-Observe the ping request and replies within Wireshark. Take the time to analyze and get a general idea of the information provided from the ICMP packet capture.

-Additionally, try pinging any website (ex: www.google.com) and observe the traffic. Can you notice any difference from the previous packet capture? What information is associated with the different systems that are communicating to one another (IP addresses, MAC addresses, protocols)?

-Keep experimenting with more ping requests and other commands to get more familiar with these tools. 

-If you don't understand the information provided by Wireshark, here is a link to their website where you will find tutorials adapted for beginners: https://www.wireshark.org/learn.
</p>
<br />




<h3>Step 4: Prepare for Part 3</h3>

<p>
<img src="https://i.imgur.com/vgk7jx7.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-From here, you can directly move on to Part 3 while leaving the Wireshark and PowerShell windows open; (link).

-If you wish to end the lab without moving on to Part 4, close all opened windows and turn off the Windows VM session by clicking on the X on the upper bar. Additionally, make sure you stop or delete your VMs to avoid unnecessary costs and optimize resource usage.
</p>
<br />
