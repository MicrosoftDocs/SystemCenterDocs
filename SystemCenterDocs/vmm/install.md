---
ms.assetid: 362eb695-e4da-4470-ab02-3799faad279d
title: Install VMM
description: This article provides installation instructions for VMM
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Install VMM



Use this article to install the System Center - Virtual Machine Manager (VMM) management server.

## Before you start

- Review the [system requirements](system-reqs.md) and [planning information](install.md)
- Make sure you have at least local admin permissions on the computer before you run setup.

## Run setup

1. Close any open programs and ensure that no restarts are pending on the computer.
2. To start the Virtual Machine Manager Setup wizard, on your installation media, right-click **setup.exe**, and then click **Run as administrator**.
3. In the main setup page, click **Install**.
4. On the **Select features to install** page, select the **VMM management server** check box, and then click **Next**. The VMM console will be automatically installed. If you're installing on a cluster node you'll be asked if you want to make the management server highly available.
5. On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, VMM will be installed as an evaluation version that expires in 180 days after installation.
6. On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.
7. On the **Diagnostic and Usage Data** page, review Microsoft's data collection policy and how to disable data collection. Then click **Next**.
8. If the **Microsoft Update** page appears, select whether you want to use Microsoft Update, and then click Next. If you've already chosen to use Microsoft Update on this computer the page won't appear.
9. On the **Diagnostic and Usage Data** page, review Microsoft's data collection policy and how to disable data collection. Then click **Next**
10. On the **Installation location** page, use the default path or type a different installation path for the VMM program files, and then click **Next**. The setup program checks the computer on which you are installing the VMM management server to ensure that the computer meets the appropriate hardware and software requirements. If the computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.
11. On the **Database configuration** page,  if you're using a remote SQL instance specify the name of the computer that is running SQL Server. If you are installing the VMM management server on the same computer that is running SQL Server, then in the **Server name** box, either type the name of the computer (for example, **vmmserver01**) or type **localhost**. If the SQL Server is in a cluster, type the cluster name.
12. Don't specify a **Port** value if you don't have a remote instance of SQL Server, or if you have a remote SQL Server that uses the default port (1443).
13. Specify the SQL Server instance name and whether to use an existing or new database. You'll need an account with permissions to connect to the instance.
14. On the **Configure service account and distributed key management** page, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation. Learn more about distributed key management [here](plan-install.md#distributed-key-management).
15. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory.
16. On the **Port configuration** page, use the default port number for each feature or provide a unique port number that is appropriate in your environment. You cannot change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, do not configure any feature to use port 5986, because that port number is preassigned.
17. On the **Library configuration** page, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
18. On the **Installation summary** page, review your selections and then click **Install**. The **Installing features** page appears and displays the installation progress.
19. On the **Setup completed successfully** page, click **Close** to finish the installation. To open the VMM console, you can ensure that **Open the VMM console when this wizard closes** is checked, or you can click the **Virtual Machine Manager Console** icon on the desktop.

During Setup, VMM enables the following firewall rules. These rules remain in effect even if you later uninstall VMM.

-   Windows Remote Management

-   Windows Standards-Based Storage Management

> [!NOTE]
> If Setup does not finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.


## Install VMM from a command prompt

You can install VMM from a command prompt. The installation media contains .ini files for all VMM features:

- **VMServer.ini**: Settings for the VMM management server.
- **VMClient.ini**: Settings for the VMM console.
- **VMServerUninstall.ini**: Uninstallation settings for the VMM management server.

Each of these files contain key/value pairs with default values. These entries are commented out. Remove the comment symbol(#) and change the value.

1. Edit the VMServer.ini file with the options in the table below this procedure
2. After you edit open an elevated command prompt and run setup.exe with the parameters below. For example, to use a VMServer.ini file that is stored in C:\Temp with a SQL Server administrator account of contoso\SQLAdmin01 and a VMM service account of contoso\VMMadmin14, use the following command:
**setup.exe /server /i /f C:\Temp\VMServer.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123 /VmmServiceDomain contoso /VmmServiceUserName VMMadmin14 /VmmServiceUserPassword password456 /IACCEPTSCEULA**

### VMServer.ini values

**Option** | **Values** | **Default**
--- | --- | ---
ProductKey | Product key in the format: xxxxx-xxxxx-xxxxx-xxxxx-xxxxx | xxxxx-xxxxx-xxxxx-xxxxx-xxxxx
UserName | Optional display name for the user who is installing the features. This is not the user account for the installation. | Administrator
CompanyName | Optional display name for the organization that is installing the features. | Microsoft Corporation
ProgramFiles | Location for VMM files. | C:\Program Files\Microsoft System Center 2012\Virtual Machine Manager
CreateNewSqlDatabase | 0: Use an existing Microsoft SQL Server database.<br/><br/> 1: Create a new SQL Server database. | 1
SqlInstanceName | Name of the new or existing instance of SQL Server. | MICROSOFT$VMM$
SqlDatabaseName | Name of the new or existing SQL Server database. | VirtualManagerDB
RemoteDatabaseImpersonation | 0: Do not impersonate the administrator account for SQL Server. The user that runs setup.exe must be an administrator for the server that is hosting SQL Server.<br/><br/> 1: Impersonate the administrator account for SQL Server by using the provided credentials. The user who runs setup.exe must provide values for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters. | 0
SqlMachineName | Name of the server that is hosting SQL Server. Do not specify localhost. Instead, specify the actual name of the computer. | <sqlmachinename>
(various ports) | Ports used by VMM | IndigoTcpPort: 8100<br/><br/> IndigoHTTPSPort: 8101<br/><br/ IndigoNETTCPPort: 8102<br/><br/ IndigoHTTPPort: 8103<br/><br/ WSManTcpPort: 5985<br/><br/ BitsTcpPort: 443
CreateNewLibraryShare | 0: Use an existing library share.<br/><br/> 1: Create a new library share. | 1
LibraryShareName | Name of the file share to be used or created. | MSSCVMMLibrary
LibrarySharePath | Location of the existing file share or the new file share to be created. | C:\ProgramData\Virtual Machine Manager Library Files
LibraryShareDescription | Description of the share. | Virtual Machine Manager Library Files
SQMOptIn | 0: Do not opt in for "Diagnostic and Usage Data".<br/><br/> 1: Opt in for "Diagnostic and Usage Data | 1
MUOptIn | 0: Do not opt in to Microsoft Update.<br/><br/> 1: Opt in to Microsoft Update. | 0
VmmServiceLocalAccount | 0: Use a domain account for the VMM service (scvmmservice).<br/><br/> 1: Use the Local System account for the VMM service.<br/><br/> To use a domain account, when you run setup.exe, provide values for the VMMServiceDomain, VMMServiceUserName, and VMMServiceUserPassword parameters. | 0
TopContainerName | Container for Distributed Key Management (DKM); for example, “CN=DKM,DC=contoso,DC=com”. | VMMServer
HighlyAvailable | 0: Do not install as highly available.<br/><br/> 1: Install as highly available. | 0
VmmServerName | Clustered service name for a highly available VMM management server. Do not enter the name of the failover cluster or the name of the computer on which the highly available VMM management server is installed. | <VMMServerName>
VMMStaticIPAddress | IP address for the clustered service name for a highly available VMM management server, if you are not using Dynamic Host Configuration Protocol (DHCP). Both IPv4 and IPv6 are supported. | <comma-separated-ip-for-HAVMM>
Upgrade | 0: Do not upgrade from a previous version of VMM.<br/><br/> 1: Upgrade from a previous version. | 1

### Setup-exe parameters

Parameter | Details
--- | ---
/server | Specifies installation of the VMM management server.
/i or /x | Specifies whether to install (/i) or uninstall (/x) the server.
/f <filename> | Specifies the .ini file to use. Be sure that this parameter points to the correct .ini file. If setup.exe does not find an .ini file, it will perform the installation by using its own default values.
/VmmServiceDomain <domainName> | Specifies the domain name for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini.
/VmmServiceUserName <userName> | Specifies the user name for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini.
/VmmServiceUserPassword <password> | Specifies the password for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini.
/SqlDBAdminDomain <domainName> | Specifies the domain name for the administrator account for the SQL Server database. Use this parameter if the current user does not have administrative rights to SQL Server.
/SqlDBAdminName <userName> | Specifies the user name for the administrator account for the SQL Server database. Use this parameter if the current user does not have administrative rights to SQL Server.
/SqlDBAdminPassword <password> | Specifies the password for the administrator account for the SQL Server database. Use this parameter if the current user does not have administrative rights to SQL Server.
/IACCEPTSCEULA | Notes acceptance of the Microsoft Software License Terms. This is a mandatory parameter.<br/><br/> For example, to use a VMServer.ini file that is stored in C:\Temp with a SQL Server administrator account of contoso\SQLAdmin01 and a VMM service account of contoso\VMMadmin14, use the following command: **setup.exe /server /i /f C:\Temp\VMServer.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123 /VmmServiceDomain contoso /VmmServiceUserName VMMadmin14 /VmmServiceUserPassword password456 /IACCEPTSCEULA**

## Uninstall VMM or the VMM console

1.  Make sure the VMM console and VMM command shell are closed.
2. On the computer on which the VMM management server is installed, click **Start**, and then click **Control Panel**.
3.  Under **Programs**, click **Uninstall a program**. Under **Name**, double-click **Microsoft System Center 2016 Virtual Machine Manager**.
4.  On the **What would you like to do?** page, click **Remove features**.
5.  On the **Select features to remove** page, select the **VMM management server** check box, and then click **Next**. If you want to uninstall the VMM console, select the **VMM console** check box. Note that if you have a highly available VMM deploy, you must remove both the VMM server and VMM console.
6.  On the **Database options** page, select whether you want to retain or remove the VMM database, and, if necessary, credentials for the database, and then click **Next**.
7.  On the **Summary** page, review your selections and click **Uninstall**. The **Uninstalling features** page appears and uninstallation progress is displayed.
8.  After the VMM management server is uninstalled, on the **The selected features were removed successfully** page, click **Close**.



The following firewall rules, which were enabled during VMM Setup, remain in effect after you uninstall VMM:

-   File Server Remote Management

-   Windows Standards-Based Storage Management firewall rules

If there is a problem with setup completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

### Uninstall VMM from the command line

To uninstall VMM edit the VMServerUninstall.ini file as described below.
Then run setup.exe for the uninstall. For example, to uninstall using an ini file stored in C:\Temp with an account contoso.SQLAdmin01 type: **setup.exe /server /x /f C:\Temp\VMServerUninstall.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123**


#### VMServerUnisntall.ini

Option | Details | Default value
--- | --- | ---
RemoteDatabaseImpersonation | 0: Local SQL Server installation.<br/><br/> 1: Remote SQL Server installation.<br/><br/> When you run setup.exe, provide a value for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters unless the user who is running setup.exe is an administrator for SQL Server. | 0
RetainSqlDatabase | 0: Remove the SQL Server database.<br/><br/> 1: Do not remove the SQL Server database<br/><br/> To remove the SQL Server database, when you run setup.exe, provide a value for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters unless the user who is running Setup is an administrator for SQL Server. | 0
ForceHAVMMUninstall | 0: Do not force uninstallation if setup.exe cannot verify whether this node is the final node of the highly available installation.<br/><br/> 1: Force the uninstallation.
