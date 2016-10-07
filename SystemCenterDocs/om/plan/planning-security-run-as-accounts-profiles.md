---
ms.assetid: 6e01e763-068a-4d67-aaff-a9d91a4afe41
title: Run As Accounts and Profiles
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Run As Accounts and Profiles

>Applies To: System Center 2016 - Operations Manager

Run As accounts define which credentials will be used for certain actions that are carried out by the Operations Manager agent. These accounts are centrally managed through the Operations console and assigned to different Run As profiles. If a Run As profile is not assigned to a particular action, it will be carried out under the Default Action account. In a low-privilege environment, the default account may not have the required permissions for a particular action, and a Run As profile can be used to provide this authority. Management packs may install Run As profiles and Run As accounts to support required actions. If this is the case, their documentation should be referenced for any required configuration.

## Default Run As accounts

The following table lists the default Run As accounts that are created by Operations Manager during setup.  

| Name | Description | Credentials |
|:--- |:--- |:--- |
|Domain\ManagementServerActionAccount | This is the user account under which all rules run by default on management servers. | Domain account specified as the Management Server Action account during setup. | 
| Local System Action Account | Built-in System account used as an action account. | Windows Local System account | 
| APM Account | Application Performance Monitoring account used to provide keys for encrypting secure information collected from the application during monitoring. | Encrypted binary account | 
| Data Warehouse Action Account | Used to authenticate with SQL Server hosting the OperationsManagerDW database. | Domain account specified during setup as the Data Warehouse Write account. | 
| Data Warehouse Report Deployment Account | Used to authenticate between the management server and SQL Server hosting Operations Manager Reporting Services. | Domain account specified during setup as the Data Reader account. | 
| Local System Windows Account | Built-in SYSTEM account used by the agent action account. | Windows Local System account | 
| Network Service Windows Account | Built-in Network service account | Windows NetworkService account | 


## Default Run As profiles

The following table lists the Run As profiles that are created by Operations Manager during setup. Note that if the Run As account is left blank for the particular profile, the Default Action account (either the Management Server Action account or the Agent Action account, depending on the location of the action) will be used.

| Name | Description | Run As account |
|:--- |:---|:--- |
|  Active Directory Based Agent Assignment Account | Account used by Active Directory-based agent assignment module to publish assignment settings to Active Directory. | Local System Windows Account | 
| Automatic Agent Management Account | This account will be used to automatically diagnose agent failures. | None | 
| Client Monitoring Action Account | If specified, used by Operations Manager 2016 to run all client monitoring modules.  If not specified, Operations Manager uses the default action account. | None | 
| Connected Management Group Account | Account used by Operations Manager management pack to monitor connection health to the connected management groups. | None | 
| Data Warehouse Account | If specified, this account is used to run all Data Warehouse collection and synchronization rules instead of the default action account. If this account is not overridden by the Data Warehouse SQL Server Authentication account, this account is used by collection and synchronization rules to connect to the Data Warehouse databases using Windows integrated authentication. | None | 
| Data Warehouse Report Deployment Account | This account is used by Data Warehouse report auto-deployment procedures to execute various report deployment-related operations. | Data Warehouse Report Deployment Account | 
| Data Warehouse SQL Server Authentication Account | If specified, this login name and password is used by collection and synchronization rules to connect to the Data Warehouse databases using SQL Server authentication. | Data Warehouse SQL Server Authentication Account | 
| MPUpdate Action Account | This account is used by the MPUpdate notifier. | None | 
| Notification Account | Windows account used by notification rules. Use this account's e-mail address as the e-mail and instant message 'From' address. | None | 
| Operational Database Account | This account is used to read and write information to the Operations Manager database. | None | 
| Privileged Monitoring Account | This profile is used for monitoring, which can only be done with a high level of privilege to a system; for example, monitoring that requires Local System or Local Administrator permissions. This profile defaults to Local System unless specifically overridden for a target system. | None | 
| Reporting SDK SQL Server Authentication Account | If specified, this login name and password is used by SDK Service to connect to the Data Warehouse databases using SQL Server authentication. | Reporting SDK SQL Server Authentication Account | 
| Reserved | This profile is reserved and must not be used | None | 
| Validate Alert Subscription Account | Account used by the validate alert subscription module that validates that notification subscriptions are in scope. This profile needs administrator rights. | Local System Windows Account | 
| SNMP Monitoring Account | This account is used for SNMP monitoring. | None | 
| SNMPv3 Monitoring Account | This account is used for SNMPv3 monitoring. | None |
| UNIX/Linux Action Account | THis account is used for low privilege UNIX and Linux access. | None | 
| UNIX/Linux Agent Maintenance Account | This account is used for privileged maintenance operations for UNIX and Linux agents.  Without this account agent maintenance operations will not work. | None | 
| UNIX/Linux Privileged Account | This account is used for accessing protected UNIX and Linux resources and actions that require high privileges.  Without this account some rules, diagnostics and recoveries will not work. | None | 
| Windows Cluster Action Account | This profile is used for all discovery and monitoring of Windows Cluster components. This profile defaults to used action accounts unless specifically populated by the user. | None | 
| WS-Management Action Account | This profile is used for WS-Management access. | None |

## Understanding distribution and targeting

Both Run As account distribution and Run As account targeting must be correctly configured for the Run As profile to work properly.

When you configure a Run As profile, you select the Run As accounts you want to associate with the Run As profile. After you create that association, you can specify the class, group, or object for which the Run As account is to be used for running tasks, rules, monitors, and discoveries against.

Distribution is an attribute of a Run As account, and you can specify which computers will receive the Run As account credentials. You can choose to distribute the Run As account credentials to every agent-managed computer or only to selected computers.

Example of Run As account targeting: Physical computer ABC hosts two instances of Microsoft SQL Server, instance X and instance Y. Each instance uses a different set of credentials for the sa account. You create a Run As account with the sa credentials for instance X, and you create a different Run As account with the sa credentials for instance Y. When you configure the SQL Server Run As profile, you associate both Run As account credentials—for example, X and Y—with the profile and specify that the Run As account instance X credentials are to be used for SQL Server instance X and that the Run As account Y credentials are to be used for SQL Server instance Y. Then you must also configure each set of Run As account credentials to be distributed to physical computer ABC.

Example of Run As account distribution: SQL Server1 and SQL Server2 are two different physical computers. SQL Server1 uses the UserName1 and Password1 set of credentials for the SQL sa account. SQL Server2 uses the UserName2 and Password2 set of credentials for the SQL sa account. The SQL management pack has a single SQL Run As profile that is used for all SQL Servers. You can then define one Run As account for UserName1 set of credentials and another Run As account for the UserName2 set of credentials. Both of these Run As accounts can be associated with the one SQL Server Run As profile and can be configured to be distributed to the appropriate computers. That is, UserName1 is distributed to SQL Server1 and UserName2 is distributed to SQL Server2. Account information sent between the management server and the designated computer is encrypted.

## Run As account security

In System Center 2016 - Operations Manager, Run As account credentials are distributed only to computers that you specify (the more secure option). If Operations Manager automatically distributed the Runs As account according to discovery, a security risk would be introduced into your environment as illustrated in the following example. This is why an automatic distribution option was not included in Operations Manager.

For example, Operations Manager identifies a computer as hosting SQL Server 2016 based on the presence of a registry key. It is possible to create that same registry key on a computer that is not actually running an instance of SQL Server 2016. If Operations Manager were to automatically distribute the credentials to all agent managed computers that have been identified as SQL Server 2016 computers, the credentials would be sent to the imposter SQL Server and they would be available to anyone with administrator rights on that server.

When you create a Run As account using Operations Manager 2016, you are prompted to choose whether the Run As account should be treated in a Less secure or More secure fashion. “More secure” means that when you associate the Run As account with a Run As profile, you have to provide the specific computer names that you want the Run As credentials distributed to. By positively identifying the destination computers, you can prevent the spoofing scenario that was described before. If you choose the less secure option, you will not have to provide any specific computers and the credentials will be distributed to all agent-managed computers. 

> [!NOTE] 
> The credentials you select for the Run As account must have at a minimum, logon locally rights; otherwise, the module will fail.
