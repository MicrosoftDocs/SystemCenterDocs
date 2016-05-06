---
title: Account Information for Operations Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d15e7313-dfba-4fdf-8146-c11db2ce2aee
---
# Account Information for Operations Manager
During the setup and operation of [!INCLUDE[om12long]./Token/om12long_md.md)], you are asked to provide credentials for several accounts. This section provides information about the various accounts and how to change the credentials or passwords for the accounts after a deployment.

-   [Action Accounts](assetId:///e95045fe-a88a-4f6c-9640-cb42a0ba63eb#BKMK_ActionAccount)

-   [Service Accounts](assetId:///e95045fe-a88a-4f6c-9640-cb42a0ba63eb#BKMK_ServiceAccounts)

-   [Agent Installation Account](assetId:///e95045fe-a88a-4f6c-9640-cb42a0ba63eb#BKMK_AgentInstallationAccount)

-   [Data Warehouse Write Account](assetId:///e95045fe-a88a-4f6c-9640-cb42a0ba63eb#BKMK_DataWarehouseWriteAccount)

-   [Data Reader Account](assetId:///e95045fe-a88a-4f6c-9640-cb42a0ba63eb#BKMK_DataReaderAccount)

## <a name="BKMK_ActionAccount"></a>Action Accounts
The [!INCLUDE[om12short]./Token/om12short_md.md)] management server, gateway server, and agent, all contain a process called MonitoringHost.exe. MonitoringHost.exe is used to accomplish monitoring activities, such as running a monitor or a task. For example, when an agent subscribes to the event log to read events, it is the MonitoringHost.exe process that runs those activities. The account that a MonitoringHost.exe process runs as is called the action account. The action account for the MonitoringHost.exe process that is running on an agent is called the agent action account. The action account used by the MonitoringHost.exe process on a management server is called the management server action account. The action account used by the MonitoringHost.exe process on a gateway server is called the gateway server action account.

When you validate or change the default action account, you must ensure that the account you are using for your default Action Account is configured to be a **Role** member of the **ConfigServiceMonitoringUsers** database role.

#### To validate the Action Account

1.  On the server that hosts the operational database, open SQL Server Management Studio and connect to the local server.

2.  Expand **Databases**, and then expand the operational database, which by default is **OperationsManager**.

3.  Expand **Security**, then **Roles**, and then **Database Roles**.

4.  Verify that the **ConfigServiceMonitoringUsers** role is listed.

5.  If this role is not listed, you can right\-click **Database Roles** to add it.

### Agent Action Account
Unless an action has been associated with a Run As profile, the credentials used to perform the action are those defined for the action account. For more information about the Run As profile, see [Managing Run As Accounts and Profiles](http://go.microsoft.com/fwlink/?LinkID=207778). Some examples of actions include the following:

-   Monitoring and collecting Windows event log data

-   Monitoring and collecting Windows performance counter data

-   Monitoring and collecting Windows Management Instrumentation \(WMI\) data

-   Running actions such as scripts or batch files

MonitoringHost.exe is the process that runs these actions by using the credentials specified in the action account. A new instance of MonitoringHost.exe is created for each account.

### Using a Low\-Privileged Account
When you install [!INCLUDE[om12short]./Token/om12short_md.md)], you can choose one of two options while assigning the action account:

-   Local System

-   Domain or Local Account

A common approach is to specify a domain account, which allows you to select a user with the least amount of privileges necessary for your environment.

The default action account must have the following minimum privileges:

-   Member of the local Users group

-   Member of the local Performance Monitor Users group

-   Allow log\-on\-locally permission \(SetInteractiveLogonRight\)

The minimum described above are the lowest privileges that [!INCLUDE[om12short]./Token/om12short_md.md)] supports for the action account. Other Run As accounts can have lower privileges. The actual privileges required for the Run As accounts depend on which management packs are running on the computer and how they are configured. For more information about which specific credentials are required, see the appropriate management pack guide.

Keep the following points in mind when choosing credentials for the agent action account:

-   A low\-privileged account is all that is necessary for agents that are used to monitor domain controllers.

-   Using a domain account requires you to update your password consistent with your password expiration policies.

-   You must stop and then start System Center Management service if the action account has been configured to use a low\-privilege account and this account was added to the required groups while the System Center Management service was running.

### Notification Action Account
The notification action account is a Run As account that is created by the user to configure notifications. This is the action account that is used for creating and sending notifications. Ensure that the credentials you use for this account have sufficient rights for the SMTP server, instant messaging server, or SIP server that you will use for notifications.

If you change the password for the credentials that you entered for the notification action account, you have to make the same password changes for the Run As account.

### Managing Action Account Credentials
For the account you choose, Operations Manager determines what the password expiration date is and generates an alert 14 days before the account expires. When you change the password in Active Directory, you can change the password for the action account in Operations Manager on the **Account** tab on the **Run As Account Properties** page. For more information about managing the action account credentials, see [How to Change the Credentials for the Action Account](assetId:///df996b1d-ffc4-4840-b34b-a287ce4dd041).

## <a name="BKMK_ServiceAccounts"></a>Service Accounts
The set of credentials of the System Center Configuration service and System Center Data Access service account is used by the System Center Data Access service and System Center Management Configuration service to update and read information in the operational database. Operations Manager ensures that the credentials used for the Data Access Services \(DAS\) service account are assigned to the Sdk\_user role in the operational database. The System Center Configuration service and System Center Data Access service account can be configured as either a Local System account or as a domain account. A local User account is not supported.

If the management server and the operational database are on different computers, the System Center Configuration service and System Center Data Access account have to be changed to a domain account. For better security, we recommend that you use an account different from the one used for the management server action account. To change these accounts, see [How to Change Credentials for the Operations Manager for System Center 2012 Services](assetId:///0143b85a-9284-4333-8844-505979c82ac2).

## <a name="BKMK_AgentInstallationAccount"></a>Agent Installation Account
When implementing discovery\-based agent deployment, you are prompted for an account with administrator rights. This account is used to install the agent on the computer, and therefore it must be a local administrator on all the computers you are deploying agents to. The management server action account is the default account for agent installation. If the management server action account does not have administrator rights, select **Other user account** and type an account that has administrator rights. This account is encrypted before it is used and then discarded.

## <a name="BKMK_DataWarehouseWriteAccount"></a>Data Warehouse Write Account
The Data Warehouse Write account writes data from the management server to the Reporting data warehouse and reads data from the operational database. The credentials that you supply for this account are made a member of the roles according to the application, as described in the following table.

> [!NOTE]
> For information about supported configurations for [!INCLUDE[om12long]./Token/om12long_md.md)], see [Supported Configurations for Operations Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=219650).

|Application|Database\/Role|Role\/Account|
|---------------|------------------|-----------------|
|Supported versions of Microsoft SQL Server|Operational database|db\_datareader|
|Supported versions of Microsoft SQL Server|Operational database|dwsync\_user|
|Supported versions of Microsoft SQL Server|Data warehouse database|OpsMgrWriter|
|Supported versions of Microsoft SQL Server|Data warehouse database|db\_owner|
|[!INCLUDE[om12short]./Token/om12short_md.md)]|User role|Operations Manager Report Security Administrators account|
|[!INCLUDE[om12short]./Token/om12short_md.md)]|Run As account|Data Warehouse Action account|
|[!INCLUDE[om12short]./Token/om12short_md.md)]|Run As account|Data Warehouse Configuration Synchronization Reader account|

If you change the password for the credentials that you entered for the Data Warehouse Write account, you have to make the same password changes for the following accounts:

-   Run As account called Data Warehouse Action account

-   Run As account called Data Warehouse Configuration Synchronization Reader account

## <a name="BKMK_DataReaderAccount"></a>Data Reader Account
This account is used to deploy reports, define what user the SQL Server Reporting Services uses to run queries against the Reporting data warehouse, and for the SQL Server Reporting Services IIS Application Pool account to connect to the management server. This account is added to the Report Administrator User profile.

The credentials that you supply for this account are made a member of the roles according to the application, as described in the following table.

> [!NOTE]
> For information about supported configurations for [!INCLUDE[om12long]./Token/om12long_md.md)], see [Supported Configurations for Operations Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=219650).

|Application|Database\/Role|Role\/Account|
|---------------|------------------|-----------------|
|Supported versions of Microsoft SQL Server|Reporting server installation instance|Report Server Execution Account|
|Supported versions of Microsoft SQL Server|Data warehouse database|OpsMgrReader|
|[!INCLUDE[om12long]./Token/om12long_md.md)]|User role|Operations Manager Report Security Administrators|
|[!INCLUDE[om12long]./Token/om12long_md.md)]|User role|Operation Manager Report Operators|
|[!INCLUDE[om12long]./Token/om12long_md.md)]|Run As account|Data Warehouse Report Deployment account|
|Internet Information Services \(IIS\)|Application pool|ReportServer$<INSTANCE>|
|Windows Service|SQL Server Reporting Services|Log on account|

If you change the password for the credentials that you entered for the Data Reader account, you have to make the same password changes for the following accounts:

-   Report Server Execution Account

-   The SQL Server Reporting Services service account on the computer that is hosting SQL Server Reporting Services \(SSRS\)

-   The IIS ReportServer$<INSTANCE> Application Pool account

-   Run As account called Data Warehouse Report Deployment account

## Account Information

-   [How to Change the Credentials for the Action Account](assetId:///df996b1d-ffc4-4840-b34b-a287ce4dd041)

-   [How to Change Credentials for the System Center Management Configuration Service and System Center Data Access Service](assetId:///0143b85a-9284-4333-8844-505979c82ac2)

-   [How to Change IIS ReportServer Application Pool Account Password](assetId:///e357e8a4-fd78-4e0a-9c38-458226f71a69)

-   [How to Change the Reporting Server Execution Account Password](assetId:///9630b555-fa03-4355-89bb-54b5805dc5ca)

-   [How to Change the Windows Service Account Password for the SQL Server Reporting Service](assetId:///63832555-006c-4b4c-b273-9107c6a87ff1)

-   [How to Change the Run As Account Associated with a Run As Profile](assetId:///76b2c729-9ab5-458b-aafc-62c51eb77471)



