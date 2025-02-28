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
<img src="https://i.imgur.com/qE2S03X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-From PowerShell, initiate a perpetual/non-stop ping from your Windows 10 VM to your Linux VM like so: "ping 10.0.0.5 -t" (your Linux VM private IP address may be different).

-In Wireshark, restart the packet capture by clicking on the green shark fin, filter for ICMP traffic for real-time analysis and let it run at the same time as the perpetual ping.
</p>
<br />



<h3>Step 2: Disable ICMP incoming traffic for the Linux Virtual Machine</h3>

<p>
<img src="https://i.imgur.com/yIohkeY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-While leaving the perpetual ping and packet capture running, go back to Azure and select your Linux VM.

-Under "Networking", click on "Network settings", then click on the link under "Network security group". It will open the Linux VM Network Security Group (NSG), which acts like a firewall for the Linux VM.
</p>
<br />



<p>
<img src="https://i.imgur.com/yhkex3k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Under "Settings", click on "Inbound security rules", then click on "Add".

-In the new window, under "Destination port ranges", leave an "*" since ICMP doesn't use a specific port number. 

-Under "Protocol", choose the "ICMPv4".

-Under "Action", choose "Deny"; we're basically creating a rule that denies all inbound (incoming) ICMP traffic to the Linux VM.

-Under "Priority", put 290 (or any number below 300) to ensure that the rule that we are creating will be evaluated (prioritized) first.

-Leave all the other options at their default configuration and click on "Add". You should see the new rule added to the top of the list of existing rules.
</p>
<br />



<h3>Step 3: Observe the ICMP traffic</h3>

<p>
<img src="https://i.imgur.com/z1eXNB7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Go back to PowerShell and Wireshark in your Windows VM, after a couple seconds, you should notice your perpetual ping requests timing out once the rule takes effect. This means that the NSG is dropping the ICMP packets before they reach the Linux VM.
</p>
<br />



<h3>Step 4: Re-enable ICMP incoming traffic for the Linux Virtual Machine<h3>

<p>
<img src="https://i.imgur.com/5zOk2az.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Go back to Azure and delete the rule that we created for the Linux VM. 
How do you think deleting this rule will impact the ICMP traffic?
</p>
<br />




<h3></h3>

<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

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
<img src="https://i.imgur.com/1oucI2O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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




<h3>Step 4: Prepare for Part 4</h3>

<p>
<img src="" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-From here, click on the red square symbol in the upper to stop the packet capture and directly move on to Part 3 while leaving the Wireshark and PowerShell windows open; (link).

-If you wish to end the lab without moving on to Part 3, close all opened windows and turn off the Windows VM session by clicking on the X on the upper bar. Additionally, make sure to stop or delete your VMs to avoid unnecessary costs and optimize resource usage.
</p>
<br />
