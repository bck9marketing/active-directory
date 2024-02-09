<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines(VM)/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Deploy a Domain Controller VM & Client VM
- Install Active Directory
- Create Admin/User Accounts in Active Directory
- Join Client VM to newly created Domain
- Allow Remote Desktop for non-admin users on Client VM
- Test user account and account configuration

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/0e0b0232-82ec-4caf-84bb-00cb6718fa29" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/f2d6ba80-be10-4d3f-b9bd-db0291902756" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We're going to start off with creating our Domain Control VM. Create a VM within Azure running "Windows Server 2022", we will place this VM in a new resource group named "RG-AD". Name the VM "DC-1", and we'll be using a size of 2vcpus with 16 GiB of memory. During VM creation we'll also go to the "Networking" tab and create a new "Virtual network" named "RG-AD-vnet". Once everything is configured, create the VM.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/26cbd868-c21b-44a1-b9dc-1517c3f78588" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/df3fcc96-c604-4137-a4ca-276699ba9a0a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once our Domain Controller VM finishes deploying, go to your DC-1 VM, then go to the "Networking" tab. He're click on the text next to "Network Interface". This should take you to another page where you'll navigate to the "IP configurations" tab, click on "ipconfig1" and then set "Allocation" to "Static" and save.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
