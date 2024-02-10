<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://youtu.be/5L5Tibfy2xo)

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
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/db4f926a-8d29-4aae-beb6-d856246d9444" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/02d0e339-8606-49ed-9812-4b9f6bd93205" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next we're going to create our Client VM running "Windows 10 Pro, version 22H2". Name it "Client-1", place it in our "RG-AD" resource group, and size it the same 2vcpu/16 GiB. We're also going to make sure to place this VM in the same "RG-AD-vnet" Virtual network we created earlier. If you don't see this Virtual Network populate in the dropbox, go make sure that our DC-1 VM finished deploying. Once you've confirmed that DC-1 finished deploying, simply refresh your your webpage and restart the Client-1 creation process. You should now see the "RG-AD-vnet" Virtual network populate. Finish creating your VM like normal.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/2e6a2707-73e1-47bf-b295-b038f7a885a9" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/53cabca2-61e4-48b9-b182-05fc51dd9084" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/a0d3f8eb-8570-437a-a1dc-a02e19b374fc" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once our VMs have been created, login to DC-1. Once windows boots, navigate to the "Service Manager" application that automatically opened. Under the "Configure this local server" text, click "Add roles and features". In the setup wizard keep clicking next until you get to the "Server Roles" section. Here check on "Active Directory Domain Services". In the new setup Wizard, click "Add Features". Keep clicking Next from here and "Install". Once the installation finishes, close out the setup Wizard and head up towards the flag icon. Click this flag icon and then click "Promote this server to a domain controller".
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/20a0531b-4b83-441a-ab65-8d257e28aa64" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/7626bb9a-8208-4463-88b4-3d3c4b86a023" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/21080fe8-74ef-4bc1-a6be-4be3dab7982e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In this new configuration wizard, select "Add a new forest" and type in "mydomain.com", click Next and type in "Password1" for the Password text boxes. From here keep clicking next until you get to "Install". Each section you click Next between will take a few seconds to load so be patient. Once you get to and hit "Install" it well take a few minutes so again, be patient. Once it finishes installing, your VM will restart.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/51a1d755-8312-4c5b-824f-c6cb23456ba6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back into DC-1, if your regular account does not work, try "mydomain.com\testaccount" as the username. "testaccount" being whatever username you used for during VM creation. Once in DC-1, look inside the automatically opened "Server Manager" and scroll over to "Tools" in the top right and then click "Active Directory Users and Computers". Alternatively, you can also open this application by searching for it in your windows search bar.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/2f90a918-8cc6-424e-a21c-087f338e809c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/eca30ded-e9a8-4c49-88ec-68e968b8ce52" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/b1aebf61-635a-4fc6-9604-cec1d1617243" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inside "Active Directory Users and Computers" scroll over to "mydomain.com" and right click > click New> click "Organizational Unit". Name this "_EMPLOYEES" and click ok. Now repeat this process and name the next Organizational Unit "_ADMINS".
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/e877cc97-5c0a-4f2e-a727-39c66bc9dd1c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/e5d0260b-7c09-4b24-aaf6-05f257a2c357" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/2114511d-17d2-4645-a57a-467eb4d74d70" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/68f85072-9822-4f6d-9368-0d46bb1e5aa5" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now going into our new "_ADMINS" folder, right click anywhere inside the empty panel or right click "_ADMINS" and click New>User. Here we'll fill out this user with basic test information. See picture above for the info I used. Name : Jane Doe / User logon name: jane_admin . Click next and use "Password1" for Password boxes. Also make sure that only "Password never expires" is checked for test purposes. Click Next and then Finish.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/644b44dd-7db4-4ba9-b4cb-2f38e0b427df" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/8f579477-87a7-45c3-b9e9-a860c1750651" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/013dba73-e9b2-4474-a74c-cb03f896f782" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/67cfd6a5-2ddf-4e22-919e-6a9bdc9e0c29" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
With our new user created, right click Jane Doe and click "Properties". In this Properties window, navigate to the "Member of" tab, click "Add..", type in "Domain Admins", click "Check Names", and click OK. Click OK in the Properties window to exit out, and logout of DC-1. Log back in with your new jane_admin account. If jane_admin does not work, try "mydomain.com\jane_admin" as the user.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/e0c62943-f6f2-452e-8646-341d12449415" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/0197754d-3e11-4320-9922-389bc0d2d1a4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/330ac6a9-ef6a-42b7-beba-7a7c0f0121fd" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/6afa62a4-de11-494c-bbfb-e0f5099408a2" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Head to your Azure portal and pull up your DC-1 Virtual Machines page. Copy DC-1's private IP. Then head to over to Client-1's VM page and select the "Networking" tab. Here click the blue text next to "Networking Interface". In this new page navigate to the "DNS servers" tab, select "Custom" under "DNS servers" and type in or paste in DC-1's private IP. Click "Save" up top and let it process. Once it finishes saving, had back to your Client-1 VM's Overview page and Restart your VM.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/57f1e354-3901-45f4-9d09-e800675fc682" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/9e555a83-9d08-422c-bc66-55568601fd66" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After giving your VM a minute or 2 to restart, login to Client-1 with your regular account created in VM creation. Once Windows boots up, right click the Windows button in the bottom left and click "System". Here click "Rename this PC", in the new window click "Change..". In the next window select "Domain" and type in our domain "mydomain.com". Click ok and in the window that pops up login with our "jane_admin" account(Password1). Click ok. Click ok/exit out of all the windows. Let it process and then look around for a small popup window that says "Welcome to the mydomain.com domain.". Sometimes this window pops up behind everything else. Click ok to that and any other windows that pop up. Let the VM restart.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/c9c2bde7-c5fd-4297-ab22-57505d221bdc" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/98cbfb0e-61a4-4a5d-92d5-3f5b91769180" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/6913f52d-f5d0-480f-925f-48cef0e8aae3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 as mydomain.com\jane_admin Password1. Once logged in, right click the Windows button and click "System". Here click on "Remote desktop". On this next page click "Select users that can remotely access this PC". In the new window click "Add.." and then type in "Domain Users". Click "Check Names" then Ok. Ok on the previous window as well. We can now log into Client-1 as a normal, non-admin user.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/9f8650c7-4c76-4ac7-8a16-171e369167df" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/b48d31a0-360d-4449-9d5a-1bd813febec2" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/c0ffc1b8-44af-43d0-94ff-7ecbf72eaf89" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Head back to DC-1, if not already logged in, log back in with "mydomain.com\jane_admin". Here we're going to pull up "Active Directory Users and Computers" again and create a new User inside our "_EMPLOYEES" folder. Make up a test employee in the same fashion as Jane Doe with a non expiring password. With our new employee created, we now have the ability to configure this account. We can do things like Reset his password or Unlock his account right from this application.
</p>
<br />

<p>
<img src="https://github.com/bck9marketing/active-directory/assets/159003800/6af469f9-c7fd-41e4-89f8-04e68f25c80f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We can now also login to Client-1 with our new mydomain.com\bob.builder account! We are now able to create and configure admins and users within our Active Directory.
</p>
<br />
