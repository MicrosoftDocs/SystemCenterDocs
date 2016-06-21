---
title: Operations Manager Accounts
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 923cdb13-3c6f-4892-ae15-6dc55c0593d4
---
# Operations Manager Accounts
To communicate with various parts of the monitoring infrastructure, the [!INCLUDE[om12long](../../includes/om12long_md.md)] management group requires two accounts: the Management Server Action Account and the System Center Configuration service and System Center Data Access Service Account. You are required to specify credentials for these accounts during installation.

If you install Reporting, you need to specify credentials for two additional accounts: the Data Warehouse Write account and the Data Reader account.

When you install an agent, you will be required to provide credentials for the Computer Discovery account and the Agent action account. You are also prompted for an account that has Administrator rights on the computers you will install the agent on.

## Action Account
The action account is used to gather information about, and run responses on, the managed computer \(a managed computer being either a management server or a computer with an agent installed\). The MonitoringHost.exe processes run under the action account or a specific Run As account. There might be more than one MonitoringHost.exe process running on the agent at any given time.

Some of the actions that MonitoringHost.exe performs include:

-   Monitoring and collecting Windows event log data.

-   Monitoring and collecting Windows performance counter data.

-   Monitoring and collecting Windows Management Instrumentation \(WMI\) data.

-   Running actions such as scripts or batches.

The separation of the Health Service process from the single and multiple uses of the MonitoringHost process means that if a script running on the managed computer stalls or fails, the functionality of the Operations Manager service or other responses on the managed computer will not be affected.

The action account can be managed through the Default action account located in **Run As Profiles** in the **Administration** workspace.

### Using a Low\-Privileged Account
When you install [!INCLUDE[om12short](../../includes/om12short_md.md)], you have the option of specifying either a domain account or using Local System. The more secure approach is to specify a domain account which allows you to select a user with the least amount of privileges necessary for your environment.

You can use a low\-privileged account for the agent’s action account. On computers running Windows Server 2003 and Windows Vista, the account must have the following minimum privileges:

-   Member of the local Users group

-   Member of the local Performance Monitor Users group

-   “Allow log on locally” permission \(SetInteractiveLogonRight\)

> [!IMPORTANT]
> The minimum privileges described above are the lowest privileges that Operations Manager supports for the Action account. Other Run As accounts can have lower privileges. The actual privileges required for the Action account and the Run As accounts will depend upon which management packs are running on the computer and how they are configured. For more information about which specific privileges are required, see the appropriate management pack guide.

Keep the following points in mind when choosing an credentials for the Management Server Action Account:

-   A low\-privileged account can be used only on computers running Windows Server 2003 and Windows Vista. On computers running Windows 2000 and Windows XP, the action account must be a member of the local Administrators security group or Local System.

-   Using a low\-privileged domain account requires password updating consistent with your password expiration policies.

-   You cannot enable Agentless Exception Monitoring \(AEM\) on a management server with a low\-privileged action account.

-   The Action account must be assigned the Manage Auditing and Security log privilege by using Local or Global policy, if a management pack is to read the event in the Security Event log.

### Action Accounts and the Operations Manager Database
You assigned credentials to the action account when you installed. By default, the action account has access to the Operations Manager database. To increase security, you can remove access to the Operations Manager database from the action account and create a new separate Run As Account for accessing the Operations Manager database.

## System Center Configuration Service and System Center Data Access Service Account
The System Center Configuration service and System Center Data Access service account is used by the System Center Data Access and System Center Management Configuration services to update information in the Operations Manager database. The credentials used for the action account will be assigned to the sdk\_user role in the Operations Manager database.

The account used for the SDK and Config Service account must have local administrative rights on the root management server computer. The account should be either a Domain User or Local System. The use of Local User account is not supported. We recommended you use a different account from the one used for the Management Server Action Account.

## Agent Installation Account
When implementing discovery\-based agent deployment, you are prompted for an account with Administrator privileges. This account is used to install the agent on the computer, and therefore it must be a local administrator on all the computers you are deploying agents to. This account is encrypted before being used and then discarded.

## Notification Action Account
This is the action account which is used for creating and sending notifications. Ensure that the credentials you use for this account have sufficient rights for the SMTP server, instant messaging server, or SIP server that you will use for notifications.

## See Also
[Implementing User Roles](https://technet.microsoft.com/library/hh230728%28v=sc.12%29.aspx)
[Managing Access in Operations Manager](Managing-Access-in-Operations-Manager.md)
[How to Create a New Action Account in Operations Manager](https://technet.microsoft.com/library/hh230739%28v=sc.12%29.aspx)
[How to Manage the Report Server Unattended Execution Account in Operations Manager](https://technet.microsoft.com/library/hh443401%28v=sc.12%29.aspx)
[Control Access by Using the Health Service Lockdown Tool in Operations Manager](https://technet.microsoft.com/library/hh212737%28v=sc.12%29.aspx)
[Accessing UNIX and Linux Computers in Operations Manager](https://technet.microsoft.com/library/hh212886%28v=sc.12%29.aspx)
[Managing Run As Accounts and Profiles](Managing-Run-As-Accounts-and-Profiles.md)


