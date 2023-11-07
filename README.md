# Part 1: Create Subscription and First Resources
After initiating my Azure subscription and documenting the details, I launched a Windows 10 Pro VM named "windows-vm" and an Ubuntu VM named "linux-vm" in the "EAST US 2" region under a specific Resource Group and Virtual Network. I selected robust VM sizes, recorded configurations, and used secure credentials. Network Security Groups for both VMs were adjusted to allow all inbound traffic, and I managed the VMs' operational status based on daily lab activity needs to optimize resource use.

### List of VM's below (including VM used to simulate attacker)
![Virtual Machines](https://github.com/alexmerelus/Azure-Resources/assets/138509128/5296f48c-8857-4d81-86ee-f5d9fc6dabad)

I accessed "windows-vm," turned off its firewall, and installed SQL Server Evaluation and SQL Server Management Studio, enabling event logging for monitoring. Testing confirmed that SQL logging was effective and capturing required data. Lastly, I successfully pinged and SSH'd into "linux-vm," ensuring network connectivity and remote access functionality. Next, I performed a ping test to the Ubuntu Virtual Machine, named "linux-vm," and successfully logged into it via SSH. This step was important to confirm network connectivity and the operational status of remote access.

### Resource Group List (Included group created for attacker simulation)
![Resource Group List](https://github.com/alexmerelus/Azure-Resources/assets/138509128/15cb2ae2-1388-4fdc-b4be-0bae743c761c)

As an administrator, I configured an additional Windows VM named "attack-vm" in a non-US region, set up its resource group and virtual network, and verified its functionality. Switching to an attacker role, I intentionally failed multiple remote desktop and SQL Server authentication attempts on "windows-vm," as well as SSH login attempts on "linux-vm," to generate erroneous logs. These actions were documented and monitored before I returned to my own system, concluding the simulated attack phase.

### Microsfot Entra AD Users
![Microsoft Entra AD Users](https://github.com/alexmerelus/Azure-Resources/assets/138509128/4be8409f-1164-4343-b691-870df97c5ae1)

I conducted a cost analysis of my Azure subscription to ensure my spending was on track. I created a user in Azure Active Directory (aka AAD, now known as Microsoft Entra Identity Services), I created users with specific roles: "global_reader_alex" as a Tenant-Level Global Reader, "subcription_reader_isaiah" as a Subscription-Level Reader, and "rg_contributor_joseph" as a Resource Group Contributor. For each role, I logged into an incognito session to verify their respective permissions, ensuring that each user had appropriate access levels before closing the sessions.

### Log Analytics Agents add to Linux and Windows VM's
![Log Analytics Agent on windows-vm](https://github.com/alexmerelus/Azure-Resources/assets/138509128/7585e4ad-3322-490a-9cf5-5359fa8c4215)

I downloaded a significant Geo-Data file for the lab and then set up a Log Analytics Workspace named "LAW-Cyber-Lab-0x" to aggregate logs. After configuring Sentinel to integrate with the workspace, I created a geoip watchlist, specifying its details meticulously, and uploaded the data file into Sentinel. To confirm the success of the ingestion process, I ran a verification query in the Log Analytics Workspace.
### Flow log created for Network Security Group
![Created a flow log for NSG](https://github.com/alexmerelus/Azure-Resources/assets/138509128/a4f4aa0b-e639-4c21-9aa1-db827ac96a2b)

I created an Azure Storage Account named "sacyberlab0x" in the same region as my VMs to store the NSG Flow Logs. Then, I enabled Flow logs for both Network Security Groups, directing them to our Log Analytics Workspace, and had to ensure the storage account was in the correct region. Afterward, I configured Data Collection Rules within our Log Analytics Workspace, turned on the VMs, set up Linux and Windows data sources, and applied Special Windows Event Data Collection from a GitHub repository.

### SignIn Logs displayed from KQL Query to confirm logs of attacker account sign in attempts
![SignIn Logs - KQL Query to confirm logs of attacker account sign in attempts](https://github.com/alexmerelus/Azure-Resources/assets/138509128/50853ee8-b319-4d4f-b33c-936f29c2966f)

I then set up logging for Azure Active Directory, creating Diagnostic Settings to capture Audit Logs and Signin Logs. I verified the creation of "AuditLogs" and "SigninLogs" tables in the Log Analytics Workspace. I created a dummy user to log in once, using incognito mode, assigned them Global Administrator role, and then deleted them, observing the actions in the Audit Logs.

I constructed a query in the Log Analytics Workspace to filter and display changes in user roles, especially focusing on Global Administrator assignments.
Then, I switched to attacker mode, simulating a brute force attack against Azure Active Directory by producing multiple failed login attempts with an "attacker" user account.

Returning to admin mode, I monitored the SigninLogs for these failed login attempts and built a query to extract detailed location information from the logs, helping to understand the source and method of the attack.

### Key Vault Instance Created
![10 - Created a Key Vault Instance](https://github.com/alexmerelus/Azure-Resources/assets/138509128/7fafa03f-2049-466b-9ddf-82dd6446833e)

I configured logging for my Azure Storage account by enabling diagnostic settings to collect all logs and metrics, and directed them to my Log Analytics Workspace. Similarly, I set up logging for a newly created Key Vault instance, collecting the audit log and adding a secret named “Tenant-Global-Admin-Password” with a fictional password.

After configuring these logs, I generated activity by accessing blobs in Azure Storage and adding a key to the Key Vault, then monitored these actions through the logs, which required some time to become visible. Anticipating the next lab, I turned on both the windows-vm and linux-vm,  leaving them running overnight to accumulate logs from any unauthorized access attempts.

### Conclusion

This concludes the resource setup for logging and monitoring. Part 2 will go into analyzing logs and creating Incident Response reports in Microsoft Sentinel (SIEM)
