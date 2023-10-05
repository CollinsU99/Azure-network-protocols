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
- Download Wireshark in VM1
- Initiate a perpetual/non-stop ping from VM1 to VM2
- Create a Network Security Group in Azure to deny the perpetual/non-stop ping
- Observe SSH,DNS,RDP, and ICMP traffic in Wireshark
- Log into VM2 using SSH
- Run Powershell Commands in VM2
- Exit VM1
- Delete Resource Groups in Azure for both VMs

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/EL2Oexz.png" height="80%" width="80%" alt="img"/>
</p>

To create the Resource group, log into your Azure portal and click "Resoure group" labeled box (1) in the image above. You can also click the search bar to search for "Resource group".

<p>
<img src="https://i.imgur.com/9I7vc4k.png" height="80%" width="80%" alt="img"/>
</p>

Click the "Create" tab at the top left.

<p>
<img src="https://i.imgur.com/3JSk340.png" height="80%" width="80%" alt="img"/>
</p>

in the "Resource group" page, select your Microsoft Azure subscription as shown in box (1). Name your Resource group "RG-LAB-02" as shown in box (2). For the region, select "(US) West US 3" as shown in box (3). Now, click the "Review + create" tab at the lower left labeled box (4).

<p>
<img src="https://i.imgur.com/myONUt3.png" height="80%" width="80%" alt="img"/>
</p>

You will see a "Vallidation passed" message, go ahead and click the "Create" tab at the lower left labeled box (2) to create the Resource Group.

<p>
<img src="https://i.imgur.com/LMmdhWT.png" height="80%" width="80%" alt="img"/>
</p>

The "Resoucre group created" notification indicates that our Resource Group was created successfully. You will also see "RG-LAB-02" listed as available Resource Group as shown in the box labeled (2)

<p>
<img src="https://i.imgur.com/Sp3379b.png" height="80%" width="80%" alt="img"/>
</p>

To create virtual machines, click the search bar and search for "virtual machines". Select "Virtual machines" labeled box (2)

<p>
<img src="https://i.imgur.com/H0r1gC7.png" height="80%" width="80%" alt="img"/>
</p>

Click "Create" tab, and then click "Azure virtual machines".

<p>
<img src="https://i.imgur.com/npHLplQ.png" height="80%" width="80%" alt="img"/>
</p>

Select your Azure subscription, select the resource group "RG-LAB-02" we created, and name your virtual machine "VM1". For the region, select "(US) West US 3" and select "No infrastructure redundancy required" as the Availability option. For the Image, select "Windows 10 Pro, version 22H2 - x64 Gen2 (free services eligible)". For the Size, select "Standard _E2s_v3 - 2vcpus, 16 GiB memory". We will use "labuser" as the VM1 Username. check the Licensing box, and click the "Networking" tab at the top









