---
title: Orchestrator Security Planning
description: This article describes the service account and user account requirements, and security considerations for your System Center Orchestrator deployment.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
ms.assetid: 
author: jyothisuri
ms.author: jsuri
ms.date: 08/07/2025
monikerRange: 'sc-orch-2025'
zone_pivot_groups: orchestrator-security-planning
---
# Orchestrator Security Planning

This article describes the service account and user account requirements, and security considerations for your System Center Orchestrator deployment. You should review this topic, create the required accounts and groups, and determine if you have any additional security requirements before starting the Orchestrator installation.

::: zone pivot="orchestrator-service-account"

## Orchestrator Service Accounts

Service accounts are required for the services listed in the following table. You must create these accounts before installing the features that use them. Following are the details for each account:

|**Server**|**Service**|
|---|---|
|Management server|Orchestrator Management Service<br><br>Orchestrator Runbook Server Monitor service|
|Runbook server|Orchestrator Runbook Service|

### Orchestrator Management Service account

The Orchestrator Management Service is installed on the management server. Its service account is specified during the installation of Orchestrator. If you installed the management server and the runbook server on the same computer at the same time, this is the same account used by the Management Server Service and Runbook Server Service on each computer to access system resources. If you installed the runbook server after you already installed the management server, or if you installed the runbook server on a different computer, you can use different accounts.

The Orchestrator Management Service is responsible for maintaining the orchestration database, communicating with the Runbook Designers, and communicating with the Deployment Manager.

The account used for the Orchestrator Management Service can be a local account on the management server if the database is installed locally or if you're using SQL Server authentication to communicate with the database (although this isn't recommended). However, this configuration might not allow access to other network resources. If the database is located on another server, either the account must be joined to the Active Directory domain so it can access the database server, or you must use SQL Server authentication. Use the latter option if your database server is in a different domain than the management server.

This service account doesn't have to be an Administrator or a domain Administrator account. Note, however, that the Deployment Manager requires administrator privileges.

The service account for the Management Server Service must have the following permissions:

- Permission to log on to the management server as a service. This permission is automatically granted during the installation process.

- Member of the Microsoft.SystemCenter.Orchestrator.Admins role in the orchestration database. The account is automatically added to this role during the installation process.

### Orchestrator Runbook Server Monitor service account

The Runbook Server Monitor is installed on the management server and is responsible for monitoring the health of runbook servers. It uses the same account as the Orchestrator Management Service and requires the same permissions.

### Orchestrator Runbook Service account

The Runbook Server Service is installed on each runbook server. If you installed the management server and the runbook server on the same computer at the same time, this is the same account used by the Management Server Service and Runbook Server Service on each computer to access system resources. If you installed the runbook server after you already installed the management server, or if you installed the runbook server on a different computer, you can use different accounts. The service is responsible for running runbooks and for communicating with the orchestration database.

By default, all activities in a runbook run under the service account of the runbook server on which they're running. Some activities can specify different credentials to be used for individual actions as required. Because runbook activities often access resources on other computers, it's recommended that the account used for the Orchestrator Runbook Service is an Active Directory domain account so that it can be granted access to these external resources.

The account for the Orchestrator Runbook Service must have the following permissions:

- Permission to log on to the runbook server as a service.

- Depending on the resources that the activities in your runbooks access, the service account might require additional credentials on remote computers. Specific activities can also be configured with alternate credentials if the service account doesn't have access to particular resources.

::: zone-end

::: zone pivot="orchestrator-user-group"

## Orchestrator Users Group

Users gain access to Orchestrator through membership in the Orchestrator Users group. Any user account added to this group is granted permission to use the Runbook Designer and Deployment Manager tools. By default, users in this group have the authority to perform the following actions:

- Create new runbooks. View, change, and run existing runbooks.
- Deploy new runbook servers
- Deploy new Runbook Designers
- Register and deploy integration packs
- View and change global settings for a management server

The Orchestrator Users group has the following permissions in the management server DCOM component:

- Local and Remote Launch
- Local and Remote Activation
- Local and Remote Access

If you enable remote access for the user group (by selecting Remote Permissions during installation), the user group is added to the machine limits – Local and Remote launch, activation, and access.

You specify the Orchestrator Users group during the Orchestrator installation process. Because the Orchestrator web service uses the same group for authorization, you must use a domain group in Active Directory if the Orchestration console isn't installed on the management server. If the Orchestration console is installed on the management server, the group can be a local group on the management server.

The decision of which to use depends on where you want to manage the group’s users. Typically using an Active Directory group provides better centralized access to the group as opposed to managing it locally on the management server.

>[!Note]
>A member of the Orchestrator Users group can grant access to other users to view and run runbooks from the Orchestration console without having to add those users to the group. Those who only use the Orchestration console are referred to as operators. They typically require the ability to run runbooks, but not to create them. For information about setting permissions for individual runbooks, see [Runbook Permissions](/previous-versions/system-center/system-center-2012-r2/hh403774(v=sc.12)) in [Using Runbooks in System Center - Orchestrator](/previous-versions/system-center/system-center-2012-r2/hh403791(v=sc.12)).

::: zone-end

::: zone pivot="orchestrator-database-security"

## Orchestrator Database Security

The following sections provide information about securing the orchestration database in Orchestrator:

- Database roles

- Securing SQL server connections

- Encryption keys

### Database roles

Security to the orchestrator database is implemented through database roles in the supported versions of Microsoft SQL Server. The following table lists the roles that are created in the orchestrator database and the permissions granted to each. These roles are configured and populated with the required members during the installation process, so there's typically no requirement to work directly with them. The information provided here is to help the administrator better understand the security behind the configuration and prepare for possible custom scenarios.

|**Account**|**Database role**|
|---|---|
|Management Service Account|Microsoft.SystemCenter.Orchestrator.Admins|
|Member of Orchestrator Admins Group|Microsoft.SystemCenter.Orchestrator.Admins|
|Orchestrator Runbook Service Account|Microsoft.SystemCenter. Orchestrator.Runtime|
|Orchestrator Runbook Server Monitor Service Account|Microsoft.SystemCenter. Orchestrator.Runtime|
|Orchestrator Web Service User Account|Microsoft.SystemCenter. Orchestrator.Operators|

|**Role**|**Permission**|**Object**|
|---|---|---|
|Microsoft.SystemCenter. Orchestrator.Operators|SELECT|[Microsoft.SystemCenter.Orchestrator.Runtime].[Jobs],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[RunbookInstances],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[RunbookInstanceParameters],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[RunbookServers],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[ActivityInstances],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[ActivityInstanceData],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[Events],<br><br>[Microsoft.SystemCenter.Orchestrator.Statistics].[Statistics]|
|Microsoft.SystemCenter. Orchestrator.Operators|EXECUTE|[Microsoft.SystemCenter.Orchestrator].[GetSecurityToken],<br><br>[Microsoft.SystemCenter.Orchestrator].[AccessCheck],<br><br>[Microsoft.SystemCenter.Orchestrator].[ComputeAuthorizationCache],<br><br>[Microsoft.SystemCenter.Orchestrator.Statistics.Internal].[GetStatisticsSummary],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[CreateJob],<br><br>[Microsoft.SystemCenter.Orchestrator.Runtime].[CancelJob]|
|Microsoft.SystemCenter. Orchestrator.Runtime|SELECT|All tables,<br><br>dbo.[POLICIES_VIEW],<br><br>dbo.[POLICY_REQUEST_HISTORY]|
|Microsoft.SystemCenter. Orchestrator.Runtime|INSERT|dbo.[OBJECT_AUDIT]|
|Microsoft.SystemCenter. Orchestrator.Runtime|INSERT,<br>UPDATE|dbo.[OBJECTS],<br><br>dbo.[ACTIONSERVERS],<br><br>dbo.[POLICYINSTANCES],<br><br>dbo.[OBJECTINSTANCES],<br><br>dbo.[OBJECTINSTANCEDATA]|
|Microsoft.SystemCenter. Orchestrator.Runtime|INSERT,<br>DELETE|dbo.[COUNTERINSTANCES],<br><br>dbo.[POLICYRETURNDATA]|
|Microsoft.SystemCenter. Orchestrator.Runtime|UPDATE|dbo.[POLICY_PUBLISH_QUEUE]|
|Microsoft.SystemCenter. Orchestrator.Runtime|CONTROL|[ORCHESTRATOR_ASYM_KEY],<br><br>[ORCHESTRATOR_SYM_KEY]|
|Microsoft.SystemCenter. Orchestrator.Runtime|EXECUTE|dbo.sp_insertevent,<br><br>dbo.sp_PublishPolicy,<br><br>dbo.sp_UnpublishPolicy,<br><br>dbo.sp_UnpublishPolicyRequest,<br><br>dbo.fn_GetPolicyInstanceStatus,<br><br>dbo.fn_NumFailedInstancesPerServer,<br><br>dbo.fn_NumInstancesPerServer,<br><br>dbo.fn_NumRunningInstancesPerServer,<br><br>[Microsoft.SystemCenter.Orchestrator.Cryptography].[Encrypt],<br><br>[Microsoft.SystemCenter.Orchestrator.Cryptography].[Decrypt],<br><br>[Microsoft.SystemCenter.Orchestrator.Internal].[RethrowError]|
|Microsoft.SystemCenter. Orchestrator.Admins|SELECT,<br>INSERT,<br>UPDATE,<br>DELETE,<br>ALTER,<br>CREATE<br>TABLE|SCHEMA::dbo|
|Microsoft.SystemCenter. Orchestrator.Admins|REFERENCES|dbo.[OBJECTS]|
|Microsoft.SystemCenter. Orchestrator.Admins|SELECT|dbo.[POLICIES_VIEW], GRANT SELECT ON dbo.<br>[POLICY_REQUEST_HISTORY]|
|Microsoft.SystemCenter. Orchestrator.Admins|CONTROL|[ORCHESTRATOR_ASYM_KEY],<br><br>[ORCHESTRATOR_SYM_KEY]|
|Microsoft.SystemCenter. Orchestrator.Admins|EXECUTE|[Microsoft.SystemCenter.Orchestrator.Cryptography].[CreateOrchestratorKeys],<br><br>[Microsoft.SystemCenter.Orchestrator.Cryptography].[DropOrchestratorKeys],<br><br>[Microsoft.SystemCenter.Orchestrator.Cryptography].[Encrypt],<br><br>[Microsoft.SystemCenter.Orchestrator.Cryptography].[Decrypt],<br><br>[Microsoft.SystemCenter.Orchestrator.Internal].[RethrowError],<br><br>dbo.sp_CustomLogCleanup,<br><br>dbo.sp_GetLogEntriesForDelete_FilterByDays,<br><br>dbo.sp_GetLogEntriesForDelete_FilterByEntries,<br><br>dbo.sp_GetLogEntriesForDelete_FilterByEntriesAndDays,<br><br>dbo.sp_insertevent,<br><br>dbo.sp_PublishPolicy,<br><br>dbo.sp_UnpublishPolicy,<br><br>dbo.sp_UnpublishPolicyRequest,<br><br>dbo.fn_GetPolicyInstanceStatus,<br><br>dbo.fn_NumFailedInstancesPerServer,<br><br>dbo.fn_NumInstancesPerServer,<br><br>dbo.fn_NumRunningInstancesPerServer,<br><br>[Microsoft.SystemCenter.Orchestrator.Internal].AddUserToRole,<br><br>[Microsoft.SystemCenter.Orchestrator].[SetPermissions],<br><br>[Microsoft.SystemCenter.Orchestrator.Internal].[SetProductInfo]|

The Database Configuration Utility (**DBSetup.exe**) requires permissions as a user on the computer where the management server is installed and is a member of either the Administrators or Orchestrator Users Group to access the `settings.dat` file. Custom tools that connect to the database directly through `DBDataStore.dll` require the same permissions.

>[!Important]
>When you install Orchestrator, ensure that the account used to connect to SQL server has minimum privileges on the SQL server to avoid a potential elevation of privileges.

### Secure SQL server connections

The SQL server connections in a default deployment of Orchestrator aren't secure. The exception to this is when Orchestrator stores or retrieves sensitive data. In this case, Orchestrator creates a secure connection to SQL server with a self-signed certificate. This certificate doesn't provide strong security and is susceptible to man-in-the-middle attacks.

- For more information on encrypting connections to SQL Server, see [Encrypting Connections to SQL Server (configuring SSL)](https://go.microsoft.com/fwlink/p/?linkid=147732).
- For more information on how to enable connections to the database engine, go to [How to: Enable Encrypted Connections to the Database Engine (SQL Server Configuration Manager)](https://go.microsoft.com/fwlink/p/?linkid=234182).

### Encryption keys

As part of your security planning, you must plan for rotating your encryption keys at a regular interval. The National Institute of Standards and Technology(NSIT) recommends that keys be rotated at least once every two years. For more information about NSIT security standards, see [NSIT Computer Security Division Computer Security Resource Center](https://go.microsoft.com/fwlink/p/?linkid=235).

#### Rotate encryption keys

1. From the Runbook Designer, export all of your runbooks, global settings, variables, schedules, and so on.
      You must provide a password for the export.

      During export, all the encrypted data is decrypted and re-encrypted with a new key created by the password.

2. If you want, change the SQL Server Master Database key.

      Orchestrator encrypts data using both the SQL Server Master Database key and the master database key for the orchestration database.

      For information on how to change the SQL Server Master Database key, see [SQL Server and Database Encryption Keys (Database Engine)](https://go.microsoft.com/fwlink/p/?linkid=235869).

3. Reinstall the management server and create a new database.

      For more information on how to install the management server, see [How to Install a Management Server](/previous-versions/system-center/system-center-2012-r2/hh420384(v=sc.12)).

      Don't connect to the existing database. A new cryptographic key is generated when a new database is created.

4. From the Runbook Designer, reimport the runbooks and any other data you exported.

      Provide the password used for the export. The data in the export file is decrypted using the password, and encrypted as it is imported to the database using the new Orchestrator master database key.

::: zone-end

::: zone pivot="runbook-security"

## Runbook security

All elements of a runbook are accessible to all Runbook Designers, and to any runbook servers in your environment. You can modify the permissions for runbook elements (such as a folder), but any permissions you set aren't enforced.

::: zone-end

::: zone pivot="web-service-console-security"

## Orchestrator Web Service and Orchestration Console Security

If you plan to install the Orchestrator web service and orchestration console, you should choose a secure protocol such as HTTPS to secure communication and prevent malformed requests from a man-in-the-middle attack. For more information on securing your Orchestrator web service and the Orchestration console, go to [How to Configure the Orchestrator Web Service to use HTTPS](/previous-versions/system-center/system-center-2012-r2/hh529160(v=sc.12)).

In the default configuration of an Orchestrator deployment, web service calls aren't logged. This applies to requests made with the Orchestration console and the Orchestration Integration Toolkit (OIT). The result is that a user can start a job and pass parameters into a runbook with no record of who started the job.

To record all requests to your Orchestrator web service, you should enable audit trail logging with `atlc.exe.` For more information about logging using `atlc.exe`, go to [Audit Trail](/previous-versions/system-center/system-center-2012-r2/hh488400(v=sc.12)).

::: zone-end

::: zone pivot="use-windows-firewall"

## Use Windows Firewall with Orchestrator

Windows Firewall with Advanced Security is enabled by default on all Windows 2008 R2 computers, and blocks all incoming traffic unless it's a response to a request by the host or it's specifically allowed by a firewall rule to allow the traffic. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.

When you configure a Runbook Designer or a runbook server outside of a firewall, certain rules must be enabled on the management server computer to allow the Runbook Designer and the runbook server to communicate with the management. Additionally, for some activities such as the Monitoring Activities, if the target computer is outside the firewall, you must enable certain firewall rules to allow WMI communication.

### Configuration of Orchestrator computers

When a Runbook Designer or a runbook server is installed behind a firewall, specific firewall rules are required between the management server and the remote computers.

Enable the following rules as they apply to your configuration.

#### Enable access to your SQL server

On the remote computer where a Runbook Designer or a runbook server is installed, open a port to connect to your SQL server. The default SQL port is TCP:1433.

#### Enable access between the Runbook Designer and the management server

On the computer running the Management Server Service, add a firewall rule to allow Runbook Designer or runbook server to access `ManagementService.exe`.

##### Location of Orchestrator Management Service

|Operating system|Firewall rule|
|---|---|
|64-bit|%ProgramFiles(x86)%\Microsoft System Center 2012\Orchestrator\Management Server\ManagementService.exe|

#### Grant privilege to the Runbook Server Service account

On the remote runbook server computer, confirm that the Runbook Server Service account has the **Logon as service** privilege.

#### Allow remote deployments with the Deployment Manager

On the remote computer where you deployed the runbook server or the Runbook Designer, add a rule to allow the Deployment Manager to access the Orchestrator Remoting Service.

##### Location of Orchestrator Remoting Service

|Operating system|File location|
|---|---|
|64-bit|%SystemRoot%\SysWOW64\OrchestratorRemotingService.exe|
|32-bit|%SystemRoot%\System32\OrchestratorRemotingService.exe|

For more information about adding firewall rules, see [Add or Edit a Firewall Rule](https://go.microsoft.com/fwlink/p/?linkid=201019).

### Firewall rules for activities

Any activities that use WMI communication, such as any of the Monitoring Activities, require certain Windows Firewall rules to function correctly.

For Windows Server 2008 R2, enable the following rules to allow any activity that uses WMI to function correctly:

- Windows Management Instrumentation (Async-In)

- Windows Management Instrumentation (DCOM-In)

- Windows Management Instrumentation (WMI-In)

::: zone-end

::: zone pivot="security-scenarios"

## Orchestrator Security Scenarios

The following information provides best practices for using Orchestrator securely. This information is provided in the format of scenarios. The following scenarios are available:

- Scenario: Securely transitioning from development to test to production environments

- Scenario: Effectively managing Orchestrator Users group membership

### Scenario: Securely transitioning from development to test to production environments

The Orchestrator password data contained in runbooks can be securely shared between different instances of Orchestrator. For example, one may wish to export runbooks built in a development environment and import them into a test environment or export tested runbooks into a production environment. This export and import process would need to secure the encrypted data in each phase of the export in such a way that the exported data could be imported into a different Orchestrator environment.

This is accomplished using the Import/Export functionality available in the Runbook Designer. The export and import features are available from the **Actions** item on the Runbook Designer menu bar or by right-clicking a runbook folder. The export feature is also available by right-clicking a runbook tab, a feature commonly referred to as a **single runbook export**.

Regardless of how a runbook is exported, the encrypted data contained in runbooks will be stored securely in the resulting XML export file. This is accomplished by providing a password upon export. When Orchestrator exports the runbooks and their related configuration, any encrypted data contained in Runbooks is decrypted and encrypted again upon export using the provided password.

>[!Note]
>1. The encryption key used for the export is different from that used to store the data in the Orchestrator database. Essentially, the "export" feature decrypts the encrypted data and re-encrypts it in the export file. The export file contains the encrypted password.
>2. The export process doesn't protect the runbook itself nor the non-encrypted data contained in Runbooks. The export only protects encrypted data contained in Runbooks.

When an export file is reimported the import requires a password be provided. If the password matches, then the encrypted data contained in export will be imported and re-encrypted for storage in the Orchestrator database by using the encryption key.

>[!Note]
>1. The Export/Import password feature doesn't support password complexity rules that may be required by your organization. A blank value for the password is permitted, although not recommended for exports that contain sensitive data that has been encrypted.
2. If the password for your export is lost one can still perform an import of the runbooks and their related configuration. On the Import screen, clear the **Import Orchestrator encrypted data** option. Any Orchestrator platform-encrypted data won't be imported and created with blank values in the Orchestrator database.

### Scenario: Effectively managing Orchestrator Users group membership

Orchestrator has two core user roles: Runbook Authors and Operators. These user roles have different rights in Orchestrator. Runbook Authors are individuals that have rich administrative access to Orchestrator including its database and configuration. Runbook Authors grant access to Runbook Operators. Runbook Operators have access to the Orchestration Console and Web Service based on rights granted to them by Runbook Authors.

|User Role|Identified by|Rights|
|---|---|---|
|Runbook Author|Membership in the Orchestrator Users Group (see below)|- Administrators of Orchestrator<br>- Read, write, update Orchestrator configuration<br>- Full control of the Orchestrator database<br>- Full encrypt/decrypt rights<br>- Access to Runbook Activities that can interact with external systems via Integration Packs|
|Runbook Operator|Runbook Folder permissions granted by Runbook Authors in the Runbook Designer|- Nonadministrative rights to Orchestrator<br>- Access to the Orchestration Console and Web Service<br>- View and invoke runbooks based on rights granted by Runbook Authors<br>- No access to the Orchestrator database<br>- No encrypt/decrypt rights|

>[!Note]
>Placing a user account in the Orchestrator Users group identifies this user account as being an administrator of Orchestrator. All Orchestrator users are essentially equally-privileged administrators with full access to Orchestrator and the data contained in the database. This would include access to encrypt and decrypt data contained in the Orchestrator database.

Orchestrator manages security through membership in two security groups created at installation time. These are the Orchestrator Users group and the Orchestrator System group. Membership in either or both of these groups identifies accounts that are considered administrators of Orchestrator ("trusted personas"). Administrative rights include the ability to update runbooks and their related configuration data, update the configuration of runbook servers, interact with external systems via integration packs, install and deploy integration packs, interact programmatically with the Orchestrator database, update the database configuration and encrypt/decrypt encrypted data stored in the Orchestrator database.

>[!Note]
>Membership in either or both of these groups grants full administrative access to Orchestrator including access to all data contained in the Orchestrator database and full encrypt/decrypt rights.

|Security group|Associated persona|Security group purpose|
|---|---|---|
|Orchestrator Users Group|Runbook authors and anyone who deploys integration packs|This security group defines user accounts that will be able to launch the Runbook Designer, Deployment Manager and Data Store Configuration utility.<br>Membership in this group grants privileged access to the Orchestrator database. This would include the ability to read and update the database configuration as well as access and decrypt encrypted data.|
|Orchestrator System Group|None (used for service accounts)|This security group defines the service accounts that require privileged access to the Orchestrator database. This would include the ability to read and update the database configuration as well as access and decrypt encrypted data.|

The following user roles are considered trusted/untrusted personas in Orchestrator.

|Security domain|Context|Cryptography rights|Identified by|Trusted persona|
|---|---|---|---|---|
|Run Time|Orchestrator Services<br><br>**Invoke Runbook** Alternate Credentials|Full encrypt & decrypt|Orchestrator Systems Group in Active Directory / Credentials on **Invoke Runbook** Runbook Activity|Yes|
|Design Time|Runbook Designer<br><br>Deployment Manager<br><br>Data Store Configuration|Full encrypt & decrypt|Orchestrator Users Group in Active Directory|Yes|
|Operator|Orchestration Console<br>Web Service|No explicit access to encrypted or decrypted data.|User rights defined in the Runbook Designer by the Runbook Author role|No|
|Database Administrator|MS SQL Server 20008 R2|Full Encrypt & decrypt|Rights to SQL Server as a DBA with rights to the Orchestrator database|Yes|
|Windows Administrator|Windows Server 2008 R2|No explicit rights are granted, however Windows administrators are considered trusted personas.|Rights to Windows|Yes|

::: zone-end

::: zone pivot="data-encryption"

## Orchestrator Data Encryption

This article provides information about data encryption in Orchestrator.

### Best practices for encrypted variables

Encrypted variables in Orchestrator allow you to more securely use variables to provide sensitive data to runbook activities. Encrypted variables are used exactly like standard global variables; that is, with a subscription. If you subscribe to these variables in activity fields that get republished, the variable contents can be exposed on the data bus. Due to this, encrypted variables should be subscribed to only in fields that are not republished. This best practice isn't enforced by Orchestrator, but it must be a part of your planning process.

However, if encrypted data must be published on the data bus in order to be sent to another system (for example, a product that runs on a different server), you must ensure that the channel to that product is secure. For example, BMC Remedy supports a secure mode for connection, and products with web interfaces typically allow using the Secure Sockets Layer connection (using the HTTPS protocol).

### Data encrypted and decrypted in Orchestrator

Orchestrator provides a code set of encryption and decryption services that are used to generate Orchestrator platform-encrypted data. These services are used to secure data flagged for encryption in the Orchestrator database and decrypt the data to plain-text so it can be used as part of a runbook. These core encryption services are managed by the Orchestrator database and management server. Rights to these services are granted through membership in the Orchestrator Users group or the Orchestrator System group.

>[!Note]
>Orchestrator runbooks could contain data encrypted by an external encryption service and used as runbook Published data. Orchestrator would not handle data from such an external system any differently than any other piece of data.

Orchestrator uses encryption in the following product feature areas:

|Feature area|Description|
|---|---|
|Runbook activities|Any property masked out when one type in the field is an encrypted property. This would include passwords on the **Security Credentials** tab but can include other properties as well.|
|Options menu|The **Options** menu is used to store credentials and other information used to configure integration packs. Properties of connection settings can contain encrypted properties.|
|Variables|Variables that have the **Encrypted Variable** checkbox selected will be encrypted.|

>[!Note]
>Encrypted variables are intended to be used via subscription in properties that require an encrypted value such as a password used in a runbook activity. If an encrypted variable is subscribed to in a non-encrypted field the encrypted value will be provided. The plain-text value is only available when used in an encrypted property.

### Manage encrypted data in Orchestrator

Orchestrator has a core cryptographic service whose design is based on AES using SQL Server cell-level encryption. As such, all encryption and decryption is performed centrally by SQL Server. Encryption keys are centrally managed by SQL Server. Both the SQL Server Service Master Key and the Orchestrator Database Master Key are required to encrypt and decrypt data.

Orchestrator uses cryptography in both the Run Time and Design Time experiences. Runbook authors interact with runbook activities in the Runbook Designer and often these activities interact with external systems to **discover** property grids, list values, and other properties. Likewise, when a runbook is tested in the Runbook Tester the encrypted data provided in protected fields needs to be decrypted so it can be passed to the target system. Finally, the Runbook Servers need to be able to decrypt encrypted data to allow runbooks to interact with external systems. As such, the database cryptographic services need to be accessed from the Runbook Servers, Runbook Designer and Runbook Tester.

Since the core cryptographic services reside in the Orchestrator database, access to the database essentially defines access to the unencrypted data.

- Runbook servers access the database directly. As such they directly access the crypto services provided by SQL Server. Run Time access to the crypto services provided by SQL Server are limited to members of the Orchestrator System Group.

- Runbook Designers and the Runbook Tester access the database indirectly through the management server. The management server offers a new service that services requests for encryption/decryption from the Runbook Designer and Runbook Tester. The management server passes through the security context of the runbook author and these credentials are used to access the crypto services. Design Time access to the crypto services provided by SQL Server are limited to members of the Orchestrator Users group.

Access to encrypted data from Orchestrator is managed by the Orchestrator Users group and the Orchestrator Systems group. Members of these two security groups essentially have rich administrative access to Orchestrator including rights to access the core cryptographic services and decrypt data stored encrypted in the database.

### Move encrypted data between Orchestrator instances

When the Orchestrator database is installed a database master encryption key is created. This database master key is used with the SQL Server master key to encrypt and decrypt data stored in the Orchestrator database. This means encrypted data is essentially **keyed** to the instance of SQL Server 2008 R2 where the data was encrypted. For example, one can't **copy** an encrypted string from a column of one instance of SQL Server 2008 R2 and **paste** the value into another instance of an Orchestrator database and decrypt the data unless both the database master key and server master key matched that of the system where the data was encrypted.

Moving encrypted data between Orchestrator instances requires one of two scenarios:

1. Both the SQL Server service master key and the Orchestrator database master key are the same as the keys on the system where the data was originally encrypted.

2. Export the runbooks and related encrypted data and Import into the new system.

Essentially, the Export functionality creates an export file whose encrypted data has been encrypted a password provided by the user during export. This export file contains encrypted data that can be decrypted by providing the same password during import. The data is encrypted and stored into the database by using the encryption keys for the new database.

::: zone-end

## Next steps

[System requirements for System Center Orchestrator](/system-center/orchestrator/system-requirements-orch).
