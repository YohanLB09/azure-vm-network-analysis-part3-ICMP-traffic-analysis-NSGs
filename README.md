# Azure VM Network Analysis - Part 2 - ICMP Traffic Analysis and Network Security Groups (NSGs)

In this tutorial, we will experiment with Network Security Groups while observing more ICMP network traffic with Wireshark and PowerShell.

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




<h3>Step 4: Re-enable ICMP incoming traffic for the Linux Virtual Machine</h3>

<p>
<img src="https://i.imgur.com/5zOk2az.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Go back to Azure and delete the rule that created for the Linux VM. How do you think deleting this rule will impact the ICMP traffic?
</p>
<br />




<h3>Step 5: Observe the ICMP traffic</h3>

<p>
<img src="https://i.imgur.com/gDWs5rF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-Go back to PowerShell and Wireshark in your Windows VM, wait a few seconds and observe the ICMP traffic changing. Is it what you anticipated?

-You should notice successful two-way communication. This confirms that ICMP traffic is no longer being blocked by the NSG, allowing normal ping operations.
</p>
<br />





<h3>Step 6: Prepare for Part 4 (Final Part)</h3>

<p>
<img src="https://i.imgur.com/gE6YL31.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-In PowerShell, type "Ctrl c" to stop the perpetual ping requests. 

-In Wireshark, click on the small red square to stop the packet capture.

-From here, you can directly move on to part 4 while leaving the Wireshark and PowerShell windows open; (link)

-If you wish to end the lab without moving on to Part 4, close all opened windows and turn off the Windows VM session by clicking on the X on the upper bar. Additionally, make sure you stop or delete your VMs to avoid unnecessary costs and optimize resource usage.
</p>
<br />
