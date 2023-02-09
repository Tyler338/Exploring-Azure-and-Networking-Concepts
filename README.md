# Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
 

 

<h2>Actions and Observations</h2>

<h2>Create Resource Group and VM's</h2>

<img src="https://i.imgur.com/12splKt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM) inside the newly created Resource Group
- While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
- Create a Linux (Ubuntu) VM
- While creating the VM, select the previously created Resource Group and Vnet
- Observe Your Virtual Network within Network Watcher

</p>
<p>

<h2>Observe ICMP Traffic</h2>

<img src="https://i.imgur.com/tycd6yn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Use Remote Desktop to connect to the Windows 10 VM
- Within Windows 10 Virtual Machine, Download and Install [Wireshark](https://1.eu.dl.wireshark.org/win64/Wireshark-win64-4.0.3.exe)
- Open Wireshark and filter for ICMP traffic only
- Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
  - Observe ping requests and replies within WireShark


</p>
<h2>Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM</h2>

<img src="https://i.imgur.com/WWHXzQT.png" height="70%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/wHYmlZO.png" height="60%" width="40%" alt="Disk Sanitization Steps"/>

- Open the Network Security Group the Ubuntu VM is using
- Disable incoming (inbound) ICMP traffic
- Observe the ICMP traffic in WireShark and the command line Ping activity (Timed Out)


<h2>Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using</h2>

<img src="https://i.imgur.com/Vd9tXLj.png" height="80%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/8E0P2QC.png" height="80%" width="40%" alt="Disk Sanitization Steps"/>

- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
- Stop the ping activity


<h2>Observe SSH Traffic</h2>


<img src="https://i.imgur.com/7gtdOm2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- In Wireshark, filter for SSH traffic only
- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
  - Command: ssh labtyler@10.0.0.5 (Use username from VM2 setup, along with the private IP address for VM2 -When prompted, enter the password that you used during the setup of VM2
- Observe SSH traffic spam in WireShark
- Exit the SSH connection by typing ‘exit’ and pressing "Enter"


<h2>Observe DHCP Traffic</h2>

<img src="https://i.imgur.com/6JvndOO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


- InWireshark, filter for DHCP traffic only
- From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
  - Observe the DHCP traffic appearing in WireShark


<h2>Observe DNS Traffic</h2>

<img src="https://i.imgur.com/DgrqIzY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


- In Wireshark, filter for DNS traffic only
- From your Windows 10 VM within a command line, use nslookup to see what google.com IP address is
- Observe the DNS traffic being show in WireShark


<h2>Observe RDP Traffic</h2>

<img src="https://i.imgur.com/vuvbLtL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- In Wireshark, filter for RDP traffic only (tcp.port == 3389)
- Oserve the immediate non-stop spam of traffic this is because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted










