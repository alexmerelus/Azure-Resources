# Azure Intro: Create Subscription and First Resources
Once my Azure subscription was setup and active, I opened Notepad to record all pertinent details regarding the subscription. This record became crucial throughout the lab activities as it kept track of configurations and settings.

Next, I created a Windows 10 Pro Virtual Machine and named it "windows-vm." I selected a cost-effective yet powerful size and secured it with a strong password. The VM was placed in the "EAST US 2" region, within a newly created Resource Group named "Leveld_ResourceGroup-Cyber-Lab," and it was connected to a Virtual Network that I named "Lab-VNet."

I then set up another Virtual Machine running Ubuntu, which I named "linux-vm," ensuring it resided in the same region, Resource Group, and VNet as the Windows VM. I chose a VM size larger than B1s to prevent potential DDOS attacks that could disrupt the logging process, heeding the advice from an updated instructional video. For security measures, I set up authentication using a username and password.

After the VMs were up and running, I configured the Network Security Groups for both VMs, setting the Layer 4 Firewall to allow all inbound traffic in preparation for the lab activities that would rely on these VMs.

Lastly, I left the VMs running when there were additional lab tasks to be completed. If I finished for the day, I shut them down to conserve resources and manage costs.

#### List of VM's below (including VM used to simulate attacker)
![Virtual Machines](https://github.com/alexmerelus/Azure-Resources/assets/138509128/5296f48c-8857-4d81-86ee-f5d9fc6dabad)

I then remotely accessed the Windows VM, referred to as "windows-vm," and proceeded to disable the Windows Firewall for configuration purposes. Following that, I installed SQL Server Evaluation Edition from the link provided by Microsoft's evaluation center, using 'sa' as the default username and an easy to remember password. I then installed SQL Server Management Studio (SSMS) from the official Microsoft documentation page to manage the SQL Server.

After the installations, I enabled logging for the SQL Server to ensure that events would be recorded in the Windows Event Viewer. I conducted tests on the SQL logging to verify that it was functioning correctly, ensuring that all necessary actions would be captured.

Next, I performed a ping test to the Ubuntu Virtual Machine, named "linux-vm," and successfully logged into it via SSH. This step was important to confirm network connectivity and the operational status of remote access.

#### Resource Group List (Included group created for attacker simulation)
![Resource Group List](https://github.com/alexmerelus/Azure-Resources/assets/138509128/fa479fee-2fee-4b40-b86f-723293486932)

As an admin, I created another Windows VM situated in a region outside the US and named it "attack-vm." I designated the Resource Group as RG-Cyber-Lab-Attacker and named the VNet Lab-VNet-Attacker. After logging into the VM, I made sure it was functioning properly and retrieved the public IP address of "windows-vm" from the Azure Portal, saving it for subsequent steps.

Shifting to an attacker's perspective, I generated some failed RDP logs against "windows-vm." From the "attack-vm," I tried to RDP into "windows-vm" using incorrect credentials and repeated this action two more times, each with different wrong usernames and passwords.

Continuing in the attacker mode, I aimed to create failed MS SQL authentication logs against "windows-vm." Inside "attack-vm," I installed SSMS, if it wasn't already installed, and attempted to connect to the SQL Server on "windows-vm" using a bad password.

I then generated some failed SSH logs against "linux-vm" by trying to SSH into it from "attack-vm" with the wrong credentials. After these attempts, I logged out of "attack-vm," returning to my own computer.
