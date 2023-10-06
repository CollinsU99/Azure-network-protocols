![265865191-f64f4a5b-bc43-4cd8-acfd-20bc707d00aa](https://github.com/CollinsU99/Azure-network-protocols/assets/124742607/ca25afdd-b194-426a-b247-356402906ce1)

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Microsoft Azure Virtual Machines</h1>

This lab will focus on using Wireshark to examine network traffic flowing between Azure Virtual Machines (VMs). We will also explore the functionality of Network Security Groups (NSGs).

In simpler terms, this lab will teach you how to use Wireshark to monitor network traffic between Azure VMs and how to use NSGs to control access to Azure VMs.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resource Group
- Create Virtual Machine in Windows and Linux
- Connect to both VMs using RDP (Remote Destop Protocol)
- Download Wireshark on VM1 (Windows 10 Pro)
- Initiate a perpetual/non-stop ping from VM1 to VM2
- Create a Network Security Group in Azure to deny the perpetual/non-stop ping
- Observe SSH,DNS,RDP, and ICMP traffic in Wireshark
- Log into VM2 using SSH
- Run Powershell Commands in VM2
- Exit VM1
- Delete Resource Groups in Azure for both VMs

<h2>Actions and Observations</h2>

<p align="center">
<img src="https://i.imgur.com/EL2Oexz.png" height="80%" width="80%" alt="img"/>
</p>

To create the Resource group, log into your Azure portal and click "Resoure group" labeled box (1) in the image above. You can also click the search bar to search for "Resource group".

<p align="center">
<img src="https://i.imgur.com/9I7vc4k.png" height="80%" width="80%" alt="img"/>
</p>

Click the "Create" tab at the top left.

<p align="center">
<img src="https://i.imgur.com/3JSk340.png" height="80%" width="80%" alt="img"/>
</p>

in the "Resource group" page, select your Microsoft Azure subscription as shown in box (1). Name your Resource group "RG-LAB-02" as shown in box (2). For the region, select "(US) West US 3" as shown in box (3). Now, click the "Review + create" tab at the lower left labeled box (4).

<p align="center">
<img src="https://i.imgur.com/myONUt3.png" height="80%" width="80%" alt="img"/>
</p>

You will see a "Vallidation passed" message, go ahead and click the "Create" tab at the lower left labeled box (2) to create the Resource Group.

<p align="center">
<img src="https://i.imgur.com/LMmdhWT.png" height="80%" width="80%" alt="img"/>
</p>

The "Resoucre group created" notification indicates that our Resource Group was created successfully. You will also see "RG-LAB-02" listed as available Resource Group as shown in the box labeled (2)

<p align="center">
<img src="https://i.imgur.com/Sp3379b.png" height="80%" width="80%" alt="img"/>
</p>

To create virtual machines, click the search bar and search for "virtual machines". Select "Virtual machines" labeled box (2)

<p align="center">
<img src="https://i.imgur.com/H0r1gC7.png" height="80%" width="80%" alt="img"/>
</p>

Click "Create" tab, and then click "Azure virtual machines".

<p align="center">
<img src="https://i.imgur.com/npHLplQ.png" height="80%" width="80%" alt="img"/>
</p>

Select your Azure subscription, select the resource group "RG-LAB-02" we created, and name your virtual machine "VM1". For the region, select "(US) West US 3" and select "No infrastructure redundancy required" as the Availability option. For the Image, select "Windows 10 Pro, version 22H2 - x64 Gen2 (free services eligible)". For the Size, select "Standard _E2s_v3 - 2vcpus, 16 GiB memory". We will use "labuser" as the VM1 Username. check the Licensing box, and click the "Networking" tab at the top

<p align="center">
<img src="https://i.imgur.com/d5USAEa.png" height="80%" width="80%" alt="img"/>
</p>

In the networking section, the virtual network, subnet, and public IP will be automatically created for you.
So make sure they all say "(new)". Then click "Review + create" tab at the lower left.

<p align="center">
<img src="https://i.imgur.com/XnRzI0G.png" height="80%" width="80%" alt="img"/>
</p>

"Deployment is in progess" means that the virtual machine is being created.

<p align="center">
<img src="https://i.imgur.com/da8cy1u.png" height="80%" width="80%" alt="img"/>
</p>

"Your deployment is complete" means that the virtual machine has been created.

<p align="center">
<img src="https://i.imgur.com/d3AJDTY.png" height="80%" width="80%" alt="img"/>
</p>

To create the Linux virtual machine, click the search bar and click "Virtual machines".

<p align="center">
<img src="https://i.imgur.com/hPvLnZT.png" height="80%" width="80%" alt="img"/>
</p>

Click "Create", and then click "Azure virtual machine".

<p align="center">
<img src="https://i.imgur.com/WI2nqUw.png" height="80%" width="80%" alt="img"/>
</p>

Select your Azure subscription, select "RG-LAB-02" for the Resource group

NOTE: We want to make sure that both virtual machines are in the same Resource group.

Name your virtual machine "VM2", for the virtual machine Region, select "(US) West US 3". For Availability options, select "No infrastructure redundancy required". For Image, select "Ubuntu server 20.04 LTS x64 Gen2 (free services eligible)". For Size, select "Standard_E2s_v3 - 2vcpus, 16 GiB memory". For the Authentication type, select "Password", and use "labuser" as your Username. Choose a unique password you can remember, and click the "Networking" tab at the top

<p align="center">
<img src="https://i.imgur.com/8ZdonPu.png" height="80%" width="80%" alt="img"/>
</p>

Make sure your VM2 is on the same virtual network as VM1, which is "VM1-vnet". The Subnet and Public IP will be generated automatically, then click "Review + create" tab at the lower left.

<p align="center">
<img src="https://i.imgur.com/epNjJhH.png" height="80%" width="80%" alt="img"/>
</p>

You will see a "Validation passed" message. Click the "Create" tab at the lower left.

<p align="center">
<img src="https://i.imgur.com/1OeRzOX.png" height="80%" width="80%" alt="img"/>
</p>

"Your deployment is complete" message means that VM2 has been created. Click the search bar and search for "virtual machines". 

<p align="center">
<img src="https://i.imgur.com/lKtFVwZ.pngg" height="80%" width="80%" alt="img"/>
</p>

Click "Virtual machines".

We will go ahead and connect both virtual machines using RDP (Remote Destop Protocol).

<p align="center">
<img src="https://i.imgur.com/HGxTcyH.png" height="80%" width="80%" alt="img"/>
</p>

Click "VM1".

<p align="center">
<img src="https://i.imgur.com/Jph5PHG.png" height="80%" width="80%" alt="img"/>
</p>

Copy the Public IP of VM1

<p align="center">
<img src="https://i.imgur.com/wdB60b4.png" height="80%" width="80%" alt="img"/>
</p>

On your local computer, click the search bar, search for "remote desktop", and click "open" to open RDP.

<p align="center">
<img src="https://i.imgur.com/4yiLN1j.png" height="80%" width="80%" alt="img"/>
</p>

Paste the VM1 public IP, and click Connect.

<p align="center">
<img src="https://i.imgur.com/Tfdsy2a.png" height="80%" width="80%" alt="img"/>
</p>

Click "More choices" > "Use a different account", type in VM1 username and password, and click "Ok" button.

<p align="center">
<img src="https://i.imgur.com/MRxCz7K.png" height="80%" width="80%" alt="img"/>
</p>

We are now connected to VM1, you can choose "No" for all the options as shown in the above image. Click the "Accept" button at the lower right to proceed.

<p align="center">
<img src="https://i.imgur.com/HWKEyKK.png" height="80%" width="80%" alt="img"/>
</p>

Click the "Yes" button.

<p align="center">
<img src="https://i.imgur.com/ymZmp3u.png" height="80%" width="80%" alt="img"/>
</p>

On your VM1 desktop, click the "Microsoft Edge" application to open it

<p align="center">
<img src="https://i.imgur.com/gT61gLQ.png" height="80%" width="80%" alt="img"/>
</p>

Select "Start without your data" > "Confirm and continue" > "Continue without this data" > "Confirm and start browsing".

<p align="center">
<img src="https://i.imgur.com/ymLBHYt.png" height="80%" width="80%" alt="img"/>
</p>

In the search bar, search for "wireshark download", and click Enter.

<p align="center">
<img src="https://i.imgur.com/UwtpLhY.png" height="80%" width="80%" alt="img"/>
</p>

Click on the first link on the web page.

<p align="center">
<img src="https://i.imgur.com/Y9QHjes.png" height="80%" width="80%" alt="img"/>
</p>

Click "Windows x64 Installer" and click the three dots (...) at the top right of the page. click the downloaded Wireshark application to proceed with installation.

<p align="center">
<img src="https://i.imgur.com/axgGzQF.png" height="80%" width="80%" alt="img"/>
</p>

Click "Next" > "Noted" > "Next" > "Next" > "Next" > "Next" > "Next" > "Install" > "I Agree" > "Install" > "Next" > "Finish" > "Next" > "Finish". 

You've now successfully installed Wireshark on Your Windows 10 Pro VM.

<p align="center">
<img src="https://i.imgur.com/tanIfmu.png" height="80%" width="80%" alt="img"/>
</p>

in VM1, search for "Wiresahrk" on the search bar and click "Open".

<p align="center">
<img src="https://i.imgur.com/hUqgGs1.png" height="80%" width="80%" alt="img"/>
</p>

Select "Ethernet" and click the blue wireshark icon at the top left to start capturing packets.

<p align="center">
<img src="https://i.imgur.com/LxsYwHS.png" height="80%" width="80%" alt="img"/>
</p>

You can see the live traffic that is happening on our virtual machine.

Let's go ahead and filter the traffic so that it stops spamming.

<p align="center">
<img src="https://i.imgur.com/jJADguZ.png" height="80%" width="80%" alt="img"/>
</p>

Search for "icmp" on the search bar, select "icmp" from the list of options provided and press "Enter" on your keyboard

NOTE: ICMP (Internet Control Messaging Protocol) is a network layer protocol used by network devices to communicate errors or other information to other devices (test connectivity to differnt hosts on  a network).

In this case, we will use it to test connectivity to VM2 by pinging VM2's private IP address.

<p align="center">
<img src="https://i.imgur.com/uFLN32h.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Azure portal and click VM2. Take note of VM2's private IP address.

<p align="center">
<img src="https://i.imgur.com/ikAncIa.png" height="80%" width="80%" alt="img"/>
</p>

Go back to VM1 remote desktop connection, search for "powershell" at the search bar and click open.

<p align="center">
<img src="https://i.imgur.com/83QW6rm.png" height="80%" width="80%" alt="img"/>
</p>

in Powershell, ping VM2's private IP address by typing "ping 10.0.0.5" and press the Enter button on your keyboard.

The image above shows that our ping was successful, as indicated by the 4 replies we got from VM2 (10.0.0.5). 

The Ping statistics shows that 4 packets were sent and received, and 0 packet was lost.

You can also confirm this on the Wireshark app, which shows us the source and destination IP addresses (VM1 & VM2), and the protocol used (ICMP). It also shows us that 4 requests was sent and we recieve 4 replies

<p align="center">
<img src="https://i.imgur.com/mgtx50E.png" height="80%" width="80%" alt="img"/>
</p>

Let's ping www.comptia.org (ping wwww.comptia.org -4). the -4 means we are specifying ICMP to ping www.comptia.org IPV4 address.

As you can see from the image above, we got 4 replies, and 4 packets were sent and received, and 0 packet was lost. 

in the Wireshark app, you can see the source and destination IP address of VM1 (10.0.0.4) and wwww.comptia.org (104.18.16.29).

<p align="center">
<img src="https://i.imgur.com/oPHdkBZ.png" height="80%" width="80%" alt="img"/>
</p>

We will now initiate a non-stop ping from VM1 to VM2.

Lets clear the current ICMP tarffic by clicking the green symbol and select "Continue without Saving"

<p align="center">
<img src="https://i.imgur.com/dWN9x57.png" height="80%" width="80%" alt="img"/>
</p>

in Powershell, initiate a non-stop ping to VM2 by typing "ping 10.0.0.5 -t), where -t means non-stop.

Non-stop ping is now initiated.

<p align="center">
<img src="https://i.imgur.com/dWN9x57.png" height="80%" width="80%" alt="img"/>
</p>

Lets change the firewall setting of VM2 to not allow ICMP traffic to come through. 



















