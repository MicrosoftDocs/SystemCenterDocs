---
ms.assetid: b6c7614a-e5af-42ae-b88d-9810b42a35f6
title: Plan VMM installation
description: This article provides planning information for setting up VMM
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency.5, engagement-fy24
---

# Plan VMM installation

::: moniker range=">= sc-vmm-2019 <= sc-vmm-2022"
This article helps you to plan all the elements required for a successful System Center - Virtual Machine Manager (VMM) installation and includes information for releases VMM 2016 and later. Use these requirements as applicable for the VMM version you plan to install.
::: moniker-end

::: moniker range="sc-vmm-2025"
This article helps you to plan all the elements required for a successful System Center - Virtual Machine Manager (VMM) installation and includes information for releases VMM 2019 and later. Use these requirements as applicable for the VMM version you plan to install.
::: moniker-end

For more information on the supported versions of hardware and software, see the system requirements article for the version you install.

## Deployment requirements

Verify the following [system requirements](system-requirements.md):

- **VMM management server**: Verify hardware and operating system requirements.
- **SQL Server**: Review supported SQL Server versions.
- **VMM console**: Review operating system requirements and if you want to run the VMM console on a separate computer.
- **VMM library**: Review the hardware requirements for remote VMM library shares.
- **Virtualization hosts**: Review the supported operating systems for Hyper-V and SOFS servers in the VMM fabric. Review requirements for VMware servers.
- **Other fabric servers**: Review the supported operating systems for update and PXE (used for bare-metal deployment) servers.

## Additional deployment requirements

::: moniker range="sc-vmm-2016"
**Component** | **Details**
--- | ---
**Command-line utilities for SQL Server** | [SQL Server 2014 feature pack for release earlier to 2019, 2016/2017 feature pack for 2019](https://www.microsoft.com/download/details.aspx?id=57474)<br/><br/> If you want to deploy VMM services using SQL Server data-tier apps, install the related command-line utilities on the VMM management server. The version you install should match the SQL Server version.
**Windows Assessment and Deployment Kit (ADK)** | Windows ADK for Windows 10.<br/><br/> You can install from setup, or [download it](/windows-hardware/get-started/adk-install). You only need the **Deployment Tools** and **Windows Preinstallation Environment** options.
**Guest operating system** | Windows operating systems [supported by Hyper-V](/windows-server/virtualization/hyper-v/Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows).<br/><br/> Linux (RHEL, Debian, Oracle Linux, SUSE, Ubuntu)
**PowerShell** | [Supported versions](system-requirements.md)
**.NET** | [Supported versions](system-requirements.md)
**Host agent** | VMM 2016/2019<br/><br/> Needed for hosts managed in VMM.
**Monitoring** | System Center Operations Manager 2016. <br/><br/> You also need SQL Server Analysis Services 2014 or a later version.
**VMware** | vCenter 5.1, 5.5, 5.8, 6.0, 6.5<br/>vCenter 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/> ESXi 5.5, 6.0, 6.5<br/>ESXi 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/>vCenter and ESXi servers running these versions can be managed in VMM.
**Bare metal provisioning** | System Management Architecture for Server Hardware (SMASH) (v1 or higher) over WS-MAN.<br/><br/> Intelligent Platform Interface 1.5 or higher<br/><br/> Data Center Manager Interface (DCMI) 1.0 or higher. <br/><br/> Required to discover and deploy physical bare-metal servers.
::: moniker-end

::: moniker range="sc-vmm-2019"
**Component** | **Details**
--- | ---
**Command-line utilities for SQL Server** | [SQL Server 2014 feature pack for release earlier to 2019, 2016/2017 feature pack for 2019](https://www.microsoft.com/download/details.aspx?id=57474)<br/><br/> If you want to deploy VMM services using SQL Server data-tier apps, install the related command-line utilities on the VMM management server. The version you install should match the SQL Server version.
**Windows Assessment and Deployment Kit (ADK)** | Windows ADK for Windows 10.<br/><br/> You can install from setup, or [download it](/windows-hardware/get-started/adk-install). You only need the **Deployment Tools** and **Windows Preinstallation Environment** options.<br/><br/>If you run into ADK file path issue while installing VMM, copy the files from the *amd64* folder in ADK root folder to the ADK root folder itself. The default ADK folder path is *C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\WSIM*, but it can be different based on your choice of folder path during ADK installation.
**Guest operating system** | Windows operating systems [supported by Hyper-V](/windows-server/virtualization/hyper-v/Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows).<br/><br/> Linux (RHEL, Debian, Oracle Linux, SUSE, Ubuntu)
**PowerShell** | [Supported versions](system-requirements.md)
**.NET** | [Supported versions](system-requirements.md)
**Host agent** | VMM 2016/2019<br/><br/> Needed for hosts managed in VMM.
**Monitoring** | System Center Operations Manager 2016. <br/><br/> You also need SQL Server Analysis Services 2014 or a later version.
**VMware** | vCenter 5.1, 5.5, 5.8, 6.0, 6.5<br/>vCenter 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/> ESXi 5.5, 6.0, 6.5<br/>ESXi 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/>vCenter and ESXi servers running these versions can be managed in VMM.
**Bare metal provisioning** | System Management Architecture for Server Hardware (SMASH) (v1 or higher) over WS-MAN.<br/><br/> Intelligent Platform Interface 1.5 or higher<br/><br/> Data Center Manager Interface (DCMI) 1.0 or higher. <br/><br/> Required to discover and deploy physical bare-metal servers.
::: moniker-end

::: moniker range="sc-vmm-2022"
**Component** | **Details**
--- | ---
**Command-line utilities for SQL Server** | [SQL Server 2014 feature pack for release earlier to 2019, 2016/2017 feature pack for 2019](https://www.microsoft.com/download/details.aspx?id=57474)<br/><br/> If you want to deploy VMM services using SQL Server data-tier apps, install the related command-line utilities on the VMM management server. The version you install should match the SQL Server version.
**Windows Assessment and Deployment Kit (ADK)** | Windows ADK for Windows 10.<br/><br/> You can install from setup, or [download it](/windows-hardware/get-started/adk-install). You only need the **Deployment Tools** and **Windows Preinstallation Environment** options.<br/><br/>If you run into ADK file path issue while installing VMM, copy the files from the *amd64* folder in ADK root folder to the ADK root folder itself. The default ADK folder path is *C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\WSIM*, but it can be different based on your choice of folder path during ADK installation.
**Guest operating system** | Windows operating systems [supported by Hyper-V](/windows-server/virtualization/hyper-v/Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows).<br/><br/> Linux (RHEL, Debian, Oracle Linux, SUSE, Ubuntu)
**PowerShell** | [Supported versions](system-requirements.md)
**.NET** | [Supported versions](system-requirements.md)
**Host agent** | VMM 2016/2019<br/><br/> Needed for hosts managed in VMM.
**Monitoring** | System Center Operations Manager 2016. <br/><br/> You also need SQL Server Analysis Services 2014 or a later version.
**VMware** | vCenter 5.1, 5.5, 5.8, 6.0, 6.5<br/>vCenter 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/> ESXi 5.5, 6.0, 6.5<br/>ESXi 7.0 and 8.0 (Supported from 2022 UR1 and 2019 UR5)<br/><br/>vCenter and ESXi servers running these versions can be managed in VMM.
**Bare metal provisioning** | System Management Architecture for Server Hardware (SMASH) (v1 or higher) over WS-MAN.<br/><br/> Intelligent Platform Interface 1.5 or higher<br/><br/> Data Center Manager Interface (DCMI) 1.0 or higher. <br/><br/> Required to discover and deploy physical bare-metal servers.
::: moniker-end

::: moniker range="sc-vmm-2025"
**Component** | **Details**
--- | ---
**Command-line utilities for SQL Server** | If you want to deploy VMM services using SQL Server data-tier apps, install the related command-line utilities on the VMM management server. The version you install should match the SQL Server version.
**Windows Assessment and Deployment Kit (ADK)** | Windows ADK for Windows 10 and 11.<br/><br/> You can install from setup, or [download it](/windows-hardware/get-started/adk-install). You only need the **Deployment Tools** and **Windows Preinstallation Environment** options.<br/><br/>If you run into ADK file path issue while installing VMM, copy the files from the *amd64* folder in ADK root folder to the ADK root folder itself. The default ADK folder path is *C:\Program Files (x86)\Windows Kits\10\Assessment and Deployment Kit\Deployment Tools\WSIM*, but it can be different based on your choice of folder path during ADK installation.
**Guest operating system** | Windows operating systems [supported by Hyper-V](/windows-server/virtualization/hyper-v/Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows).<br/><br/> Linux (RHEL, Debian, Oracle Linux, SUSE, Ubuntu, Rocky Linux)
**PowerShell** | [Supported versions](system-requirements.md)
**.NET** | [Supported versions](system-requirements.md)
**Host agent** | VMM 2019/2022<br/><br/> Needed for hosts managed in VMM.
**Monitoring** | System Center Operations Manager 2025. <br/><br/> You also need SQL Server Analysis Services 2014 or a later version.
**VMware** | vCenter 7.0 and 8.0 <br/><br/> ESXi 7.0 and 8.0 <br/><br/>vCenter and ESXi servers running these versions can be managed in VMM.
**Bare metal provisioning** | System Management Architecture for Server Hardware (SMASH) (v1 or higher) over WS-MAN.<br/><br/> Intelligent Platform Interface 1.5 or higher<br/><br/> Data Center Manager Interface (DCMI) 1.0 or higher. <br/><br/> Required to discover and deploy physical bare-metal servers.
::: moniker-end

### SPN

If the VMM user installing VMM, or running VMM setup, doesn't have permissions to write the service principal name (SPN) for the VMM server in Active Directory, setup will finish with a warning. If the SPN isn't registered, other computers running the VMM console won't be able to connect to the management server, and you won't be able to deploy a Hyper-V host on a bare metal computer in the VMM fabric. To avoid this issue, you need to register the SPN as a domain administrator before you install VMM, as follows:

1. Run these commands from \<SystemDrive\>\Windows\System32>, as a domain administrator:

    - ``setspn -u -s SCVMM/<MachineBIOSName> <VMMServiceAccount>``
    - ``setspn -u -s SCVMM/<MachineFQDN> <VMMServiceAccount>``

    For a cluster, \<MachineBIOSName\> should be \<ClusterBIOSName\> and \<MachineFQDN\> should be \<ClusterFQDN\>

2. On the VMM server (or on each node in a cluster), in the registry, navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Setup**.
3. Set **VmmServicePrincipalNames** to **SCVMM/\<MachineBIOSName\>,SCVMM/\<MachineFQDN\>**. For a cluster: **SCVMM/\<ClusterBIOSName\>,SCVMM/\<ClusterFQDN\>**.

If you can't do this, you can also register the SPN during VMM installation. A domain administrator can provide the SPN write permissions to VMM service user or setup user. 

> [!NOTE]
> This approach isn't the preferred one. The permission allows the delegated user to register any servicePrincipalName with no restrictions.

Hence, the delegated user should be highly trusted, and the account credentials must be kept secure. To do this:

1. Run adsiedit as a domain administrator.
2. Navigate to find the VMM service user. Right-click **Properties** > **Security** > **Advanced**. Then select **Add**, and in **Select a principal**, specify the user who will be granted the  permissions.
3. Select **Write servicePrincipalName** > **OK**.

When you install VMM with this user account, SPN will be registered.

## VMM management server

- You can't run the VMM management server on Nano server (applicable to Windows Server releases prior to 2019).
- The management server computer name can't exceed 15 characters.
- Don’t install the VMM management server, or other System Center components other than agents, on servers running Hyper-V.
- You can install the VMM management server on a VM. If you do, and you use the Dynamic Memory feature of Hyper-V, then you must set the startup RAM for the virtual machine to be at least 2,048 megabytes (MB).
::: moniker range=">= sc-vmm-2019"
- We recommend that you use a dedicated SCVMM management server and not install any other System Center components and management tools on the same server.
- If you want to manage more than 150 hosts, we recommend the following:
     -  Add one or more remote computers as library servers, and don't use the default library share on the VMM management server.
     -  Don't run the SQL Server instance on the VMM management server.
::: moniker-end
::: moniker range="sc-vmm-2016"
- If you want to manage more than 150 hosts, we recommend that you use a dedicated computer for the VMM management server and do the following:
     -  Add one or more remote computers as library servers, and don't use the default library share on the VMM management server.
     -  Don't run the SQL Server instance on the VMM management server.
::: moniker-end
- For high availability, the VMM management server can be installed on a failover cluster. [Learn more](~/vmm/plan-ha-install.md).

## SQL Server and database

- The instance of SQL Server that you're using must allow for case-insensitive database objects.
- The SQL Server’s computer name can't exceed 15 characters in length.
- If the VMM management server and the SQL Server computer aren't members of the same Active Directory domain, then a two-way trust must exist between the two domains.
- When you install SQL Server, select the **Database Engine Services** and **Management Tools - Complete** features.
- You can perform an in-place upgrade to a supported version of SQL Server (without moving the VMM database). Ensure that no jobs are running when you perform the upgrade, or jobs can fail and need to be restarted manually.
- For the VMM database, for better performance, don't store database files on the disk that is used for the operating system.
- If you're using Software Defined Networking (SDN) in VMM, then all networking information is stored in the VMM database. Because of this, you might want to consider high availability for the VMM database, using the following guidelines:
  - Failover clustering is supported and is the recommended configuration for availability within a single geographical area or datacenter. [Read more](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).
  - Use of Always On Availability Groups in Microsoft SQL Server is supported, but it's important to review the differences between the two availability modes, synchronous-commit and asynchronous-commit. [Learn more](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server#AvailabilityModes).
    - With asynchronous-commit mode, the replica of the database can be out of date for a period of time after each commit. This can make it appear as if the database were back in time, which might cause loss of customer data, inadvertent disclosure of information, or possibly elevation of privilege.
    - You can use synchronous-commit mode as a configuration for remote-site availability scenarios.
- The SQL Server service must use an account that has permission to access Active Directory Domain Services (AD DS). For example, you can specify the Local System Account or a domain user account. Don't specify a local user account.
- You don't need to configure collation. During deployment, Setup automatically configures CI collation according to the language of the server operating system.

- Dynamic port is supported.
- If you want to create the VMM database prior to VMM installation:
  - Ensure that you have permissions or create a SQL database, or ask the SQL Server admin to do it.
  - Configure the database as follows:

    1. Create a new database with settings: Name: VirtualManagerDB; Collation: Latin1_General_100_CI_AS, but aligned with the specific SQL Server instance collation.
    2. Grant db_owner permissions for the database to the VMM service account.
    3. In VMM setup, you'll select the option to use an existing database and specify the database details and VMM service account as the database user.

## Library server
- If you run the library server on the VMM management server, then you must provide additional hard disk space to store objects. The space required varies based on the number and size of the objects you store.
- The library server is where VMM stores items such as virtual machine templates, virtual hard disks, virtual floppy disks, ISO images, scripts, and stored virtual machines. The optimal hardware requirements that are specified for a VMM library server vary, depending on the quantity and size of these files. You'll need to check CPU usage and other system state variables to determine what works best in your environment.
- If you want to manage Virtual hard disks in the .vhdx file format, the VMM library server must run Windows Server 2012 or later.
- VMM doesn't provide a method for replicating physical files in the VMM library or a method for transferring metadata for objects that are stored in the VMM database. Instead, if necessary, you need to replicate physical files outside of VMM, and you need to transfer metadata by using scripts or other means.
- VMM doesn't support file servers that are configured with the case-sensitive option for Windows Services for UNIX because the Network File System (NFS) case control is set to **Ignore**.

## Account and domain requirements

::: moniker range=">sc-vmm-2016"
When you install VMM, you must configure the VMM service to use any one of the following accounts:

- The Local System account (can't be used for a highly available VMM deployment) or
- A domain user account or 
- A Group Managed Service Account (gMSA)

::: moniker-end

::: moniker range="sc-vmm-2016"

When you install VMM, you must configure the VMM service to use any one of the following accounts:

- The Local System account (can't be used for a highly available VMM deployment) or
- A domain user account

::: moniker-end
Ensure the following before you prepare an account:

::: moniker range=">=sc-vmm-2019"

- VMM service account should have *log on as a service* permission on the VMM server.
::: moniker-end

- You can't change the identity of the Virtual Machine Manager service account after installation. This includes changing from the local system account to a domain account, from a domain account to the local system account, or changing the domain account to another domain account. To change the Virtual Machine Manager service account after installation, you must uninstall VMM (selecting the Retain data option if you want to keep the SQL Server database), and then reinstall VMM by using the new service account.
- If you specify a domain account, the account must be a member of the local Administrators group on the computer.
- If you specify a domain account, it's recommended that you create an account that is designated to be used for this purpose. When a host is removed from the VMM management server, the account that the System Center Virtual Machine Manager service is running under is removed from the local Administrators group of the host. If the same account is used for other purposes on the host, this can cause unexpected results.
- If you plan to use shared ISO images with Hyper-V virtual machines, you must use a domain account.
- If you're using a disjointed namespace, you must use a domain account. For more information about disjointed namespaces, see Naming conventions in Active Directory for computers, domains, sites, and OUs.
- If you're installing a highly available VMM management server, you must use a domain account.
- The computer on which you install the VMM management server must be a member of an Active Directory domain. In your environment, you might have user accounts in one forest and your VMM servers and host in another. In this environment, you must establish a two-way trust between the two cross-forest domains. One-way trusts between cross-forest domains aren't supported in VMM.

::: moniker range=">=sc-vmm-2019"

- To create and use gMSA, review the article on gMSA and create the gMSA as per the guidance available. Ensure that the servers on which the VMM Management service would be installed have permissions to retrieve the password of gMSA account.  

    > [!NOTE]
    > You do not need to specify the ‘Service Principle Name (SPN)’ when creating gMSA. VMM service sets the appropriate SPN for gMSA.

::: moniker-end

## Distributed key management

By default, VMM encrypts some data in the VMM database by using the Data Protection Application Programming Interface (DPAPI). For example, Run As account credentials, passwords in guest operating system profiles, and product key information in virtual hard disks properties. Data encryption is tied to the specific computer on which VMM is installed, and the service account that VMM uses. If you move your VMM installation to another computer, VMM won't retain the encrypted data, and you'll need to enter it manually.

To ensure that VMM retains encrypted data across moves, you can use distributed key management to store encryption keys in Active Directory. If you move your VMM installation, VMM retains the encrypted data because the new VMM computer has access to the encryption keys in Active Directory. To set up distributed key management, you should coordinate with your Active Directory administrator.

> [!NOTE]
> - You must create a container in AD DS before you install VMM. You can create the container by using ADSI Edit (installed from **Server Manager** > **Remote Server Administration Tools**.)
> - You create the container in the same domain as the user account with which you're installing VMM. If you specify that the VMM service uses a domain account, that account must be in the same domain. For example, if the installation account and the service account are both in the corp.contoso.com domain, you must create the container in that domain. So, if you want to create a container that is named VMMDKM, you specify the container location as CN=VMMDKM,DC=corp,DC=contoso,DC=com. The account with which you're installing VMM needs Full Control permissions to the container in AD DS. The permissions must apply to this object and to all descendant objects.
- If you're installing a highly available VMM management server, you must use distributed key management to store encryption keys in Active Directory. You need distributed key management because if VMM fails over to a node, that node will need access to the encryption keys.
- When you configure the service account and distributed key in setup, you must type the location of the container in AD DS, for example: CN=VMMDKM,DC=corp,DC=contoso,DC=com

## Next steps

[Install VMM](install.md)
