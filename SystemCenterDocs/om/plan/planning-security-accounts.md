---
ms.assetid: c2049a9d-fb5b-4d87-beae-529a244c97ce
title: Service, User and Security Accounts
description:  This article provides an overview of the security accounts required for initial setup of Operations Manager and for core features which may require a privileged account.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/06/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Service, User and Security Accounts

>Applies To: System Center 2016 - Operations Manager

During the setup and operation of Operations Manager, you will be asked to provide credentials for several accounts. The beginning of this section provides information about each of those accounts, including the SDK and Config Service, Agent Installation, Data Warehouse Write, and Data Reader accounts.

If you use domain accounts and your domain Group Policy object (GPO) has the default password expiration policy set as required, you will either have to change the passwords on the service accounts according to the schedule, use low maintenance system accounts, or configure the accounts so that the passwords never expire.

## Action accounts

In System Center 2016 – Operations Manager, management servers, gateway servers and agents all execute a process called MonitoringHost.exe.  MonitoringHost.exe is what each server role uses to accomplish monitoring activities such as executing a monitor or running a task.  Other examples of actions MonitoringHost.exe performs include:

- Monitoring and collecting Windows event log data.
- Monitoring and collecting Windows performance counter data.
- Monitoring and collecting Windows Management Instrumentation (WMI) data.
- Running actions such as scripts or batches.

The account that a MonitoringHost.exe process runs as is called the action account.  MonitoringHost.exe is the process that runs these actions by using the credentials that are specified in the action account.  A new instance of MonitoringHost.exe is created for each account.  The action account for the MonitoringHost.exe process running on an agent is called the Agent Action Account.  The action account used by the MonitoringHost.exe process on a management server is called the Management Server Action account.  The action account used by the MonitoringHost.exe process on a gateway server is called the Gateway Server Action Account.  On all management servers in the management group, it is recommended to grant this account local administrative rights unless least-privileged access is required by your organizations IT security policy. 

Unless an action has been associated with a Run As profile, the credentials that are used to perform the action will be those defined for the action account.  For more information about Run As Accounts and Run As Profiles, see the section [Run As Accounts](planning-security-run-as-accounts-profiles.md).  When an agent runs actions as either the default action account and/or Run As account(s), a new instance of MonitoringHost.exe is created for each account.

When you install Operations Manager, you have the option of specifying either a domain account or using Local System.  The more secure approach is to specify a domain account which allows you to select a user with the least amount of privileges necessary for your environment.

You can use a low-privileged account for the agent’s action account. On computers running Windows Server 2008 R2 or higher, the account must have the following minimum privileges:

- Member of the local Users group
- Member of the local Performance Monitor Users group
- “Allow log on locally” permission (SetInteractiveLogonRight)  

> [!NOTE] 
> The minimum privileges described above are the lowest privileges that Operations Manager supports for the action account.  Other Run As accounts can have lower privileges.  The actual privileges required for the Action account and the Run As accounts will depend upon which management packs are running on the computer and how they are configured.  For more information about which specific privileges are required, see the appropriate management pack guide.


## System Center Configuration Service and System Center Data Access Service account

The System Center Configuration service and System Center Data Access service account is used by the System Center Data Access and System Center Management Configuration services to update information in the Operational database. The credentials used for the action account will be assigned to the sdk_user role in the Operational database.

The account should be either a Domain User or Local System.  The account used for the SDK and Config Service account must have local administrative rights on all management servers in the management group.  The use of Local User account is not supported.  For increased security, we recommended you use a different account from the one used for the Management Server Action Account.  

> [!NOTE] 
> If the Operations Manager database is installed on a computer separate from the management server and Local System is selected for the Data Access and Configuration service account, the computer account for the management server computer will be assigned to the sdk_user role on the Operations Manager database computer.

## Data Warehouse Write account

The Data Warehouse Write account is the account used to write data from the management server to the Reporting data warehouse, and it reads data from the Operations Manager database.  The following table describes the roles and membership assigned to the account during setup.

| Application | Database/role | Role/account |
|:--- |:---|:--- |
| Microsoft SQL Server | OperationsManager | db_datareader | 
| Microsoft SQL Server | OperationsManager | dwsync_user |
| Microsoft SQL Server | OperationsManagerDW | OpsMgrWriter |
| Microsoftg SQL Server | OperationsManagerDW | db_owner |
| Operations Manager | User role | Operations Manager Report Security Administrators | 
| Operations Manager | Run As account | Data Warehouse Action account | 
| Operations Manager | Run As account | Data Warehouse Configuration Synchronization Reader account | 

## Data Reader account

The Data Reader account is used to deploy reports, define what user the SQL Server Reporting Services uses to execute queries against the Reporting data warehouse, and define the SQL Reporting Services account to connect to the management server.  This account is added to the Report Administrator User Profile.   The following table describes the roles and membership assigned to the account during setup.

| Application | Database/role | Role/account |
|:--- |:---|:--- |
| Microsoft SQL Server | Reporting Services Installation instance | Report Server Execution account | 
| Microsoft SQL Server | OperationsManagerDW | OpsMgrReader | 
| Operations Manager | User role | Operations Manager Report Operators | 
| Operations Manager | User role | Operations Manager Report Security Administrators | 
| Operations Manager | Run As account | Data Warehouse Report Deployment account | 
| Windows service | SQL Server Reporting Services | Logon account |

Ensure that the account you plan to use for the Data Reader account has Log on as Service and Allow Log on Locally rights for each management server, and the SQL Server hosting the Reporting Server role.  

## Agent Installation account

When performing discovery-based agent deployment, an account is required with Administrator privileges to the computers being targeted for agent installation.  The management server action account is the default account for agent installation.  If the management server action account does not have administrator rights, the operator must provide a user account and password with administrative rights on the target computers.  This account is encrypted before being used and then discarded.

## Notification Action account

The Notification Action account is the account used for creating and sending notifications. These credentials must have sufficient rights for the SMTP server, instant messaging server, or the SIP server that is used for notifications.




