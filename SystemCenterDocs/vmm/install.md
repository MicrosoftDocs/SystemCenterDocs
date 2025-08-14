---
ms.assetid: 362eb695-e4da-4470-ab02-3799faad279d
title: Install VMM
description: This article provides installation instructions for VMM
author: jyothisuri
ms.author: jsuri
ms.date: 04/04/2025
ms.update-cycle: 180-days
ms.topic: install-set-up-deploy
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency.5, intro-installation, engagement-fy23, engagement-fy24
---

# Install VMM

This article describes how to install the System Center Virtual Machine Manager (VMM) management server.

## Before you start

- Review the system requirements and [planning information](plan-install.md). Learn about [system requirements](system-requirements.md).
- Ensure that you have at least local admin permissions on the computer before you run the setup.
- The account being used for install must have SA rights on the SQL instance used to host the SCVMM database

- The service account should be an administrator on the VMM server.
::: moniker range="sc-vmm-2025"
- Ensure you have the installer downloaded from one of the following procurement channels (not exhaustive):
  - [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/download-system-center-2025?msockid=0c55acf0521869ad1f07bf4d534a68ab).
  - [Downloads & Keys - Visual Studio Subscriptions](https://my.visualstudio.com/Downloads?q=System%20Center%202025).
  - [Evaluation (VHDX) from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=106280).
  - Any other procurement channels such as Microsoft Admin Center or from Microsoft partners.
::: moniker-end
::: moniker range="sc-vmm-2022"
- Ensure you have the installer downloaded from one of the following procurement channels (not exhaustive):
  - [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/download-system-center-2022?msockid=0c55acf0521869ad1f07bf4d534a68ab).
  - [Downloads & Keys - Visual Studio Subscriptions](https://my.visualstudio.com/Downloads?q=System%20Center%202022).
  - [Evaluation (VHDX) from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=104040&msockid=0c55acf0521869ad1f07bf4d534a68ab).
  - Any other procurement channels such as Microsoft Admin Center or from Microsoft partners.
::: moniker-end


>[!NOTE]
>During VMM Installation, ensure that the SQL Database isn't part of any Availability Group.

::: moniker range=">=sc-vmm-2019"

[!INCLUDE [validation-virtual-machine-manager.md](../includes/validation-virtual-machine-manager.md)]

::: moniker-end

## Run setup

>[!NOTE]
>The service account for VMM can be:
> - A local account.
> - A user account used for service.
> -	A group managed service account.
> - If you're using a local account, you can't have VMM in a highly available configuration.
> - If you're using gMSA account, the format should be *domainFQDN\gMSAAccount$*.

1. Close any open programs and ensure that no restarts are pending on the computer.
2. To start the Virtual Machine Manager Setup wizard, on your installation media, right-click **setup.exe** and then select **Run as administrator**.
3. In the main setup page, select **Install**.
4. On the **Select features to install** page, </br>
     Select the **VMM management server** checkbox, and then select **Next**. 
         The VMM console installs automatically. If you're installing on a cluster node, you'll be asked if you want to make the management server highly available.
1. On the **Product registration information** page, provide the appropriate information and select **Next**. If you don't enter a product key, VMM installs as an evaluation version that expires in 180 days after installation.
1. On the **Please read this license agreement** page, </br>
     Review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** checkbox, and then select **Next**.
1. On the **Diagnostic and Usage Data** page, </br>
     Review Microsoft's data collection policy and how to disable data collection. Then select **Next**.
1. If the **Microsoft Update** page appears, </br>
     Select whether you want to use Microsoft Update, and then select **Next**. 
         If you've already chosen to use Microsoft Update on this computer, the page won't appear.
1. On the **Diagnostic and Usage Data** page, </br>
     Review Microsoft's data collection policy and how to disable data collection and then select **Next**.
1. On the **Installation location** page, </br>
     Use the default path or enter a different installation path for the VMM program files, and then select **Next**. 
         The setup program checks the computer on which you're installing the VMM management server to ensure that the computer meets the appropriate hardware and software requirements. If the computer doesn't meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.
1. On the **Database configuration** page,
    - If you're using a remote SQL instance, specify the name of the computer that's running the SQL Server. 
    - If you're installing the VMM management server on the same computer that's running the SQL Server, then in the **Server name** box, either enter the name of the computer (for example, **vmmserver01**) or **localhost**. 
    - If the SQL Server is in a cluster, enter the cluster name.
1. Don't specify a **Port** value if you don't have a remote instance of the SQL Server or if you have a remote SQL Server that uses the default port (1433).
1. Specify the SQL Server instance name and whether to use an existing or new database. You need an account with permissions to connect to the instance.
1. On the **Configure service account and distributed key management** page, </br>
     Specify the account that the VMM service uses. You can't change the identity of the VMM service account after installation. Learn more about distributed key management [here](plan-install.md#distributed-key-management).
1. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory or not.
1. On the **Port configuration** page, </br>
     Use the default port number for each feature or provide a unique port number that's appropriate in your environment. 
         You can't change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, don't configure any feature to use port 5986 because that port number is preassigned.
1. On the **Library configuration** page, </br>
     Select whether to create a new library share or to use an existing library share on the computer. 
         The default library share that VMM creates is named *MSSCVMMLibrary*, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you can't remove it. 
         After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
1. On the **Installation summary** page, </br>
     Review your selections and then select **Install**. The **Installing features** page appears and displays the installation progress.
1. On the **Setup completed successfully** page, 
    1. Select **Close** to finish the installation. 
    1. To open the VMM console, ensure that **Open the VMM console when this wizard closes** is checked or select the **Virtual Machine Manager Console** icon on the desktop.

::: moniker range="sc-vmm-2022"
> [!NOTE]
> If VMM 2022 and SQL 2019 are installed on the same machine, the following error appears:
> Reboot the machine for successful installation.

 :::image type="error" source="media/install/error.png" alt-text="Screenshot showing error.":::
::: moniker-end

During Setup, VMM enables the following firewall rules. These rules remain in effect even if you later uninstall VMM.

-   Windows Remote Management

-   Windows Standards-Based Storage Management

> [!NOTE]
> If Setup doesn't finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

::: moniker range="sc-vmm-2019"
> [!NOTE]
> If you run into ADK file path issue while installing VMM, copy the files from the *amd64* folder in ADK root folder to the ADK root folder itself. The default ADK folder path is *C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\WSIM*, but it can be different based on your choice of folder path during ADK installation.
::: moniker-end

::: moniker range="sc-vmm-2022"
> [!NOTE]
> If you run into ADK file path issue while installing VMM, copy the files from the *amd64* folder in ADK root folder to the ADK root folder itself. The default ADK folder path is *C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\WSIM*, but it can be different based on your choice of folder path during ADK installation.
::: moniker-end

## Install VMM from a command prompt

You can install VMM from a command prompt. The installation media contains `.ini` files for all the VMM features:

- **VMServer.ini**: Settings for the VMM management server.
- **VMClient.ini**: Settings for the VMM console.
- **VMServerUninstall.ini**: Uninstallation settings for the VMM management server.

Each of these files contains key/value pairs with default values. These entries are commented out. Remove the comment symbol (#) and change the value.

1. Edit the `VMServer.ini` file with the options in the table below this procedure.
2. After you edit, open an elevated command prompt and run setup.exe with the following parameters. For example, to use a `VMServer.ini` file that is stored in C:\Temp with a SQL Server administrator account of *contoso\SQLAdmin01* and a VMM service account of *contoso\VMMadmin14*, use the following command:
**setup.exe /server /i /f C:\Temp\VMServer.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123 /VmmServiceDomain contoso /VmmServiceUserName VMMadmin14 /VmmServiceUserPassword password456 /IACCEPTSCEULA**

### VMServer.ini values

| **Option** | **Values** | **Default** |
|---|---|---|
| ProductKey | Product key in the format: xxxxx-xxxxx-xxxxx-xxxxx-xxxxx | xxxxx-xxxxx-xxxxx-xxxxx-xxxxx |
| UserName | Optional display name for the user who is installing the features. UserName isn't the user account for the installation. | Administrator |
| CompanyName | Optional display name for the organization that is installing the features. | Microsoft Corporation |
| ProgramFiles | Location for VMM files. | C:\Program Files\Microsoft System Center\Virtual Machine Manager |
| CreateNewSqlDatabase | 0: Use an existing Microsoft SQL Server database.<br/><br/> 1: Create a new SQL Server database. | 1 |
| SqlInstanceName | Name of the new or existing instance of SQL Server. | MICROSOFT$VMM$ |
| SqlDatabaseName | Name of the new or existing SQL Server database. | VirtualManagerDB |
| RemoteDatabaseImpersonation | 0: Don't impersonate the administrator account for SQL Server. The user that runs setup.exe must be an administrator for the server that is hosting the SQL Server.<br/><br/> 1: Impersonate the administrator account for SQL Server by using the provided credentials. The user who runs setup.exe must provide values for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters. | 0 |
| SqlMachineName | Name of the server that is hosting SQL Server. Don't specify localhost. Instead, specify the actual name of the computer. | \<sqlmachinename\> |
| (various ports) | Ports used by VMM | IndigoTcpPort: 8100<br/><br/> IndigoHTTPSPort: 8101<br/><br/> IndigoNETTCPPort: 8102<br/><br/> IndigoHTTPPort: 8103<br/><br/> WSManTcpPort: 5985<br/><br/> BitsTcpPort: 443 |
| CreateNewLibraryShare | 0: Use an existing library share.<br/><br/> 1: Create a new library share. | 1 |
| LibraryShareName | Name of the file share to be used or created. | MSSCVMMLibrary |
| LibrarySharePath | Location of the existing file share or the new file share to be created. | C:\ProgramData\Virtual Machine Manager Library Files |
| LibraryShareDescription | Description of the share. | Virtual Machine Manager Library Files |
| SQMOptIn | 0: Don't opt in for **Diagnostic and Usage Data**.<br/><br/> 1: Opt in for **Diagnostic and Usage Data**. | 1 |
| MUOptIn | 0: Don't opt in to Microsoft Update.<br/><br/> 1: Opt in to Microsoft Update. | 0 |
| VmmServiceLocalAccount | 0: Use a domain account for the VMM service (scvmmservice).<br/><br/> 1: Use the Local System account for the VMM service.<br/><br/> To use a domain account, when you run setup.exe, provide values for the VMMServiceDomain, VMMServiceUserName, and VMMServiceUserPassword parameters. | 0 |
| TopContainerName | Container for Distributed Key Management (DKM); for example, *CN=DKM,DC=contoso,DC=com*. | VMMServer |
| HighlyAvailable | 0: Don't install as highly available.<br/><br/> 1: Install as highly available. | 0 |
| VmmServerName | Clustered service name for a highly available VMM management server. Don't enter the name of the failover cluster or the name of the computer on which the highly available VMM management server is installed. | \<VMMServerName\> |
| VMMStaticIPAddress | IP address for the clustered service name for a highly available VMM management server if you're not using Dynamic Host Configuration Protocol (DHCP). Both IPv4 and IPv6 are supported. | \<comma-separated-ip-for-HAVMM\> |
| Upgrade | 0: Don't upgrade from a previous version of VMM.<br/><br/> 1: Upgrade from a previous version. | 1 |

### Setup-exe parameters

| Parameter | Details |
|---|---|
| /server | Specifies installation of the VMM management server. |
| /i or /x | Specifies whether to install (/i) or uninstall (/x) the server. |
| /f \<filename\> | Specifies the .ini file to use. Be sure that this parameter points to the correct .ini file. If setup.exe doesn't find an .ini file, it performs the installation by using its own default values. |
| /VmmServiceDomain \<domainName\> | Specifies the domain name for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini. |
| /VmmServiceUserName \<userName\> | Specifies the username for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini. |
| /VmmServiceUserPassword \<password\> | Specifies the password for the account that is running the VMM service (scvmmservice). Use this parameter only if you set VmmServiceLocalAccount to 0 in VMServer.ini. |
| /SqlDBAdminDomain \<domainName\> | Specifies the domain name for the administrator account for the SQL Server database. Use this parameter if the current user doesn't have administrative rights to SQL Server. |
| /SqlDBAdminName \<userName\> | Specifies the username for the administrator account for the SQL Server database. Use this parameter if the current user doesn't have administrative rights to SQL Server. |
| /SqlDBAdminPassword \<password\> | Specifies the password for the administrator account for the SQL Server database. Use this parameter if the current user doesn't have administrative rights to SQL Server. |
| /IACCEPTSCEULA | Notes acceptance of the Microsoft Software License Terms. This is a mandatory parameter.<br/><br/> For example, to use a VMServer.ini file that is stored in C:\Temp with a SQL Server administrator account of contoso\SQLAdmin01 and a VMM service account of contoso\VMMadmin14, use the following command: **setup.exe /server /i /f C:\Temp\VMServer.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123 /VmmServiceDomain contoso /VmmServiceUserName VMMadmin14 /VmmServiceUserPassword password456 /IACCEPTSCEULA** |

## Uninstall VMM or the VMM console

1. Ensure that the VMM console and VMM command shell are closed.
2. On the computer on which the VMM management server is installed, select **Start** and then select **Control Panel**.
3. Under **Programs**, select **Uninstall a program**. Under **Name**, right-click **Microsoft System Center Virtual Machine Manager**.
4. On the **What would you like to do?** page, select **Remove features**.
5. On the **Select features to remove** page, select the **VMM management server** checkbox, and then select **Next**. If you want to uninstall the VMM console, select the **VMM console** checkbox.

     > [!NOTE]
     > If you've a highly available VMM deploy, you must remove both the VMM server and the VMM console.

6. On the **Database options** page, select whether you want to retain or remove the VMM database, and, if necessary, credentials for the database, and then select **Next**.
7. On the **Summary** page, review your selections and select **Uninstall**. The **Uninstalling features** page appears, and uninstallation progress is displayed.
8. After the VMM management server is uninstalled, on the **The selected features were removed successfully** page, select **Close**.


The following firewall rules, which were enabled during VMM Setup, remain in effect after you uninstall VMM:

-   File Server Remote Management

-   Windows Standards-Based Storage Management firewall rules

If there's a problem with setup completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

### Uninstall VMM from the command line

To uninstall VMM, edit the *VMServerUninstall.ini* file as described.
Then run setup.exe for the uninstall. For example, to uninstall using an ini file stored in C:\Temp with an account contoso.SQLAdmin01 type: **setup.exe /server /x /f C:\Temp\VMServerUninstall.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123**


#### VMServerUnisntall.ini

| Option | Details | Default value |
|---|---|---|
| RemoteDatabaseImpersonation | 0: Local SQL Server installation.<br/><br/> 1: Remote SQL Server installation.<br/><br/> When you run setup.exe, provide a value for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters unless the user who is running setup.exe is an administrator for SQL Server. | 0 |
| RetainSqlDatabase | 0: Remove the SQL Server database.<br/><br/> 1: Don't remove the SQL Server database<br/><br/> To remove the SQL Server database, when you run setup.exe, provide a value for the SqlDBAdminName, SqlDBAdminPassword, and SqlDBAdminDomain parameters unless the user who is running Setup is an administrator for SQL Server. | 0 |
| ForceHAVMMUninstall | 0: Don't force uninstallation if setup.exe can't verify whether this node is the final node of the highly available installation.<br/><br/> 1: Force the uninstallation. |

## Support for gMSA account
Group Managed Service Account (gMSA) helps improve the security posture and provides convenience  through automatic password management, simplified service principle name (SPN) management, and the ability to delegate the management to other administrators.

VMM supports the use of gMSA for *Management server service account*.

>[!NOTE]
> gMSA, when used as VMM Service account, needs to have *logon as a service* and *Replace a process level token* permissions.

**Prerequisites**

1. Review [this article](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts) and create gMSA as per the guidance available in the article.
2. Ensure that the servers on which VMM Management service would be installed have permissions to retrieve the password of the gMSA account.

     > [!NOTE]
     > You don't need to specify the SPN when creating the gMSA. VMM service sets the appropriate SPN on the gMSA.

**Use the following steps:**

1. Start the VMM installation setup.
2. On the **Service account configuration** page, select **Group Managed Service Account** as the option for VMM service account.
3. Enter the gMSA account details in *Domain\gMSA account* format.



## Next Step

[Install the VMM Console](install-console.md).
