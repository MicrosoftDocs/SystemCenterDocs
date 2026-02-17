---
ms.assetid: c2049a9d-fb5b-4d87-beae-529a244c97ce
title: Service, User, and Security Accounts
description: This article provides an overview of the security accounts required for initial setup of Operations Manager and for core features that may require a privileged account.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Service, User, and Security Accounts

During the setup and daily operations of Operations Manager, you'll be asked to provide credentials for several accounts. This article provides information about each of these accounts, including the SDK and Config Service, Agent Installation, Data Warehouse Write, and Data Reader accounts.

>[!NOTE]
> Operations Manager installation provisions all necessary SQL permissions.

If you use domain accounts and your domain Group Policy Object (GPO) has the default password expiration policy set as required, you'll either have to change the passwords on the service accounts according to the schedule, use system accounts, or configure the accounts so that the passwords never expire.

## Action accounts

In System Center Operations Manager, management servers, gateway servers, and agents all execute a process called MonitoringHost.exe. MonitoringHost.exe is used to accomplish monitoring activities such as executing a monitor or running a task. The other examples of the actions MonitoringHost.exe performs include:

- Monitoring and collecting Windows event log data
- Monitoring and collecting Windows performance counter data
- Monitoring and collecting Windows Management Instrumentation (WMI) data
- Running actions such as scripts or batches

The account that a MonitoringHost.exe process runs as is called the action account.  MonitoringHost.exe is the process that runs these actions by using the credentials that are specified in the action account. A new instance of MonitoringHost.exe is created for each account.  The action account for the MonitoringHost.exe process running on an agent is called the Agent Action Account.  The action account used by the MonitoringHost.exe process on a management server is called the Management Server Action account.  The action account used by the MonitoringHost.exe process on a gateway server is called the Gateway Server Action Account.  On all management servers in the management group, we recommend that you grant the account local administrative rights unless least-privileged access is required by your organization's IT security policy.

Unless an action has been associated with a Run As profile, the credentials that are used to perform the action will be those you defined for the action account.  For more information about Run As Accounts and Run As Profiles, see the section [Run As Accounts](plan-security-runas-accounts-profiles.md).  When an agent runs actions as either the default action account and/or Run As account, a new instance of MonitoringHost.exe is created for each account.

When you install Operations Manager, you have the option to specify a domain account or use LocalSystem.  The more secure approach is to specify a domain account, which allows you to select a user with the least privileges necessary for your environment.

You can use a least-privilege account for the agent’s action account. On computers running Windows Server 2008 R2 or higher, the account must have the following minimum privileges:

- Member of the local Users group
- Member of the local Performance Monitor Users group
- Allow log on locally (SetInteractiveLogonRight) permission (not applicable for Operations Manager 2019 and later).

> [!NOTE]
> The minimum privileges described above are the lowest privileges that Operations Manager supports for the action account. Other Run As accounts can have lower privileges. The actual privileges required for the Action account and the Run As accounts will depend upon which management packs are running on the computer and how they're configured.  For more information about which specific privileges are required, see the appropriate management pack guide.

::: moniker range="<sc-om-2019"
The domain account that is specified for the action account can be granted either Log on as a Service (SeServiceLogonRight) or Log on as Batch (SeBatchLogonRight) permission if your security policy doesn't allow a service account to be granted an interactive log on session, such as when smart card authentication is required.  Modify the registry value HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\System Center\Health Service:
::: moniker-end

::: moniker range=">=sc-om-2019"

The domain account that is specified for the action account is granted with Log on as a Service (SeServiceLogonRight) permission. To change the logon type for health service, modify the registry value *HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\System Center\Health Service:*

::: moniker-end

* Name:  Worker Process Logon Type
* Type: REG_DWORD
::: moniker range="sc-om-2016"
* Values: Four (4) -  Log on as batch, Two (2) -  Allow log on locally and Five (5) - Log on as Service.  Default value is 2. 
::: moniker-end  
::: moniker range=">=sc-om-2019"
* Values: Four (4) - Log on as Batch, Two (2) -  Allow log on locally, and Five (5) - Log on as Service.  Default value is 5. 
::: moniker-end 

You can centrally manage the setting using Group Policy by copying the ADMX file  `healthservice.admx` from a management server or agent-managed system located in the folder `C:\Windows\PolicyDefinitions` and configuring the setting **Monitoring Action Account Logon Type** under the folder `Computer Configuration\Administrative Templates\System Center - Operations Manager`.  For more information working with Group Policy ADMX files, see [Managing Group Policy ADMX files](/previous-versions/windows/it-pro/windows-vista/cc709647(v=ws.10)).

## System Center Configuration Service and System Center Data Access Service account

The System Center Configuration service and System Center Data Access service account is used by the System Center Data Access and System Center Management Configuration services to update information in the Operational database. The credentials used for the action account will be assigned to the sdk_user role in the Operational database.

The account should be either a Domain User or LocalSystem.  The account used for the SDK and Config Service account should be granted local administrative rights on all management servers in the management group.  The use of Local User account isn't supported.  For increased security, we recommended you use a domain user account, and it's a different account from the one used for the Management Server Action Account. LocalSystem account is the highest privilege account on a Windows computer, even higher than local Administrator. When a service runs under the context of LocalSystem, the service has full control of the computer’s local resources, and the identity of the computer is used when authenticating to and accessing remote resources. Using LocalSystem account is a security risk because it doesn’t honor the principle of least privilege. Because of the rights required on the SQL Server instance hosting the Operations Manager database, a domain account with least privilege permissions is necessary to avoid any security risk if the management server in the management group is compromised.  The reasons are:

* LocalSystem has no password
* It doesn't have its own profile
* It has extensive privileges on the local computer
* It presents the computer’s credentials to remote computers

> [!NOTE]
> If the Operations Manager database is installed on a computer separate from the management server and LocalSystem is selected for the Data Access and Configuration service account, the computer account for the management server computer is assigned the sdk_user role on the Operations Manager database computer.  

For more information, see [about LocalSystem](/windows/desktop/services/localsystem-account).

## Data Warehouse Write account

The Data Warehouse Write account is the account used to write data from the management server to the Reporting data warehouse, and it reads data from the Operations Manager database.  The following table describes the roles and membership assigned to the domain user account during setup.

| Application | Database/role | Role/account |
|:--- |:---|:--- |
| Microsoft SQL Server | OperationsManager | db_datareader |
| Microsoft SQL Server | OperationsManager | dwsync_user |
| Microsoft SQL Server | OperationsManagerDW | OpsMgrWriter |
| Microsoft SQL Server | OperationsManagerDW | db_owner |
| Operations Manager | User role | Operations Manager Report Security Administrators |
| Operations Manager | Run As account | Data Warehouse Action account |
| Operations Manager | Run As account | Data Warehouse Configuration Synchronization Reader account |

## Data Reader account

The Data Reader account is used to deploy reports, define what user the SQL Server Reporting Services uses to execute queries against the Reporting data warehouse, and define the SQL Reporting Services account to connect to the management server.  This domain user account is added to the Report Administrator User Profile.  The following table describes the roles and membership assigned to the account during setup.

| Application | Database/role | Role/account |
|:--- |:---|:--- |
| Microsoft SQL Server | Reporting Services Installation instance | Report Server Execution account |
| Microsoft SQL Server | OperationsManagerDW | OpsMgrReader |
| Operations Manager | User role | Operations Manager Report Operators |
| Operations Manager | User role | Operations Manager Report Security Administrators |
| Operations Manager | Run As account | Data Warehouse Report Deployment account |
| Windows service | SQL Server Reporting Services | Logon account |

Verify the account you plan to use for the Data Reader account is granted the Log on as Service (for 2019 and later) or Log on as Service and Allow Log on Locally (for earlier release), right for each management server, and the SQL Server hosting the Reporting Server role.  

## Agent Installation account

When performing discovery-based agent deployment, an account is required with Administrator privileges on the computers targeted for agent installation.  The management server action account is the default account for agent installation.  If the management server action account doesn't have administrator rights, the operator must provide a user account and password with administrative rights on the target computers.  This account is encrypted before being used and then discarded.

## Notification Action account

The Notification Action account is the account used for creating and sending notifications. These credentials must have sufficient rights for the SMTP server, instant messaging server, or the SIP server that is used for notifications.
