<p align="center">
<img src="https://github.com/user-attachments/assets/d630ac9b-d82f-47cc-82fa-044d1afb1bb0" height="80%" width="80%" alt="Azure-VM's"/> 

<br />

<h1>Azure Virtual Machines and Networking</h1>

 

<h2>Description</h2>
The project consists of creating two virtual machines and a network where I monitor network traffic with Wireshark software. This is all done within Microsoft Azure. 
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b> 
- <b>Wireshark</b>
- <b>Various Network Protocols (ICMP, SSH, DHCP, DNS)</b>
- <b>Command-Line Tools</b>

<h2>Operating Systems Used </h2>

- <b>Windows 10</b>
- <b>Ubuntu 24.04</b>

<h2>Project Walk-through:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group: <br/>
<img src="https://github.com/user-attachments/assets/df6affb1-2689-4e50-868f-6af240022613" height="80%" width="80%"/> 

<br />
<br />
Once my resource group is created, next I'll create the first virtual machine:  <br/>
<img src="https://github.com/user-attachments/assets/85d0fae4-071d-4c23-b29e-dc8614459458" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Setting up the first virtual machine:  <br/>
<img src="https://github.com/user-attachments/assets/5e3c829c-26fb-430f-92a7-a014e2b22c0d" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
<img src="https://github.com/user-attachments/assets/729a1f62-914c-47dd-a3e6-6143ea04bc58" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
I'll leave all other settings to default and create this VM:  <br/>
<img src="https://github.com/user-attachments/assets/d743908e-e2c9-4469-be05-215c0a9cc170" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Now Azure has set up a VM, an IP for the VM, a network security group, a virtual network, a disk, and a NIC (Network Interface Card):  <br/>
<img src="https://github.com/user-attachments/assets/aeaff981-ae51-4c55-a141-7878cddda70f" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Second VM setup:  <br/>
<img src="https://github.com/user-attachments/assets/fab35f7f-11e9-4fb9-af85-b31eac2a6285" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
<img src="https://github.com/user-attachments/assets/66229831-def7-4bbf-9791-e33686674302" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
In the "Networking" tab, I want to ensure this VM will be on the same virtual network as the first one I made. So, I'll select the one already made for "VM1" instead of creating a new virtual network:  <br/>
<img src="https://github.com/user-attachments/assets/9c3eea71-8287-410d-8e16-523f7cf6b662" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Now, if I go back to my resource group, we can see that Azure created everything for VM2 as it did for VM1. Notice how there is only one network, however. This is because the two VMs are on the same network:  <br/>
<img src="https://github.com/user-attachments/assets/eec763c0-e5a7-4eaa-99fc-9f3061c43515" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
I use VM1's public IP to connect to it using RDP:  <br/>
<img src="https://github.com/user-attachments/assets/cb14ba45-eff0-4c0c-ad1e-b36cb62af26d" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Once my computer has connected to VM1, I will download Wireshark on the VM:  <br/>
<img src="https://github.com/user-attachments/assets/40e648fa-2794-4626-98b0-9f13a6ac6c8b" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Once Wireshark has downloaded and opened, I will select "Ethernet" to observe network traffic:  <br/>
<img src="https://github.com/user-attachments/assets/bf58498a-ff74-431b-a88d-cfb8e21fae61" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
To filter for ICMP (Internet Control Message Protocol) traffic, I type "ICMP" at the top of Wireshark. To make traffic, I will get the private IP address of VM2 and ping it from PowerShell:  <br/>
<img src="https://github.com/user-attachments/assets/59f17e00-91c0-475d-a6e7-25560177361f" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
<img src="https://github.com/user-attachments/assets/e730f54d-ed6f-433a-b85f-62f15075db94" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Now, we can make some firewall configurations to deny any ICMP traffic. To do this, I will enter a perpetual ping command into PowerShell:  <br/>
<img src="https://github.com/user-attachments/assets/1f9f9ed5-a4d9-4e88-b206-efd177ffcc86" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Next, I will go to VM2's network security group and create a new inbound security rule denying all ICMP traffic, making sure to put its priority highest so it will take precedence before all other rules:  <br/>
<img src="https://github.com/user-attachments/assets/f4746ac4-d8e8-4716-8702-6f64286ee2c1" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
Going back to our VM, we can see that the ICMP echo requests aren't getting any responses due to the security change:  <br/>
<img src="https://github.com/user-attachments/assets/0f0d4d92-6b12-4469-acb3-d81e30614732" height="80%" width="80%" alt="Setting Up in Azure"/> 

<br />
<br />
To revert the change, I can either switch the inbound rule to "Allow" instead of "Deny" or delete the rule:  <br/>
<img src="https://i.imgur.com/4tetl2l.png" height="80%" width="80%" alt="Setting Up in Azure"/> 
<br />
<br />
Now ICMP echo requests are back to getting responses:  <br/>
<img src="https://i.imgur.com/FPXmXdY.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now I will filter to only show SSH (Secure Shell) traffic by typing SSH into the bar at the top, and I will SSH into VM2 using PowerShell:  <br/>
<img src="https://i.imgur.com/blrFX07.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
I can type commands like pwd (print working directory) and observe the traffic:  <br/>
<img src="https://i.imgur.com/Corgjvn.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After filtering for DHCP (Dynamic Host Configuration Protocol) traffic, I attempted to get a new IP address by using the ipconfig /renew command:  <br/>
<img src="https://i.imgur.com/Zq7X1Zv.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Filtering for DNS (Domain Name System) traffic, I can use nslookup to find IP addresses for domain names like "www.google.com" and "www.amazon.com":  <br/>
<img src="https://i.imgur.com/3cGR7xZ.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Finally, I'll observe RDP (Remote Desktop Protocol) traffic by typing in "tcp.port == 3389" in the top bar. You'll notice there is traffic happening without us doing anything. This is because I used RDP to connect to this machine from my own computer and RDP shows us a constant live stream of whats happening:  <br/>
<img src="https://i.imgur.com/0eQAkky.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
