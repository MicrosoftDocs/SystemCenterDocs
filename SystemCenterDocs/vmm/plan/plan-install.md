---
title: Plan VMM installation
description: This article provides planning information for setting up VMM
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-10-12
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Plan VMM installation

>Applies To: System Center 2016 - Virtual Machine Manager

This article helps you to plan all the elements required for a successful System Center 2016 - Virtual Machine Manager (VMM) installation.

## Installation and upgrade requirements

This table summarizes what you'll need for VMM 2016 installation.

**Requirement** | **Version** | **Details**
--- | --- | ---
**VMM server operating system** | Windows Server 2016 | Server Core is supported
**SQL Server** | SQL Server 2014 onwards | Enterprise edition, 64-bit is required<
**Command line utilities for SQL Server** | [SQL Server 2014 feature pack](https://www.microsoft.com/download/details.aspx?id=42295), ]2012 feature pack](https://www.microsoft.com/download/details.aspx?id=29065) | If you want to deploy VMM services using SQL Server data-tier apps, install the related command-line utilities on the VMM management server. The version you install should match the SQL Server version. You don't have to install these to install VMM.
**Client (to run VMM console)** | Windows 8.1 onwards, Windows Server 2012 R2 onwards | To run the console the machine must be in an Active Directory domain.
**Windows Assessment and Deployment Kit (ADK)** | Windows ADK for Windows 10 |  You can install from setup, or you can [download it](https://msdn.microsoft.com/windows/hardware/dn913721.aspx). You only need the **Deployment Tools** and **Windows Preinstallation Environment** options.
**VMM library** | Windows Server 2012 onwards | Required operating systems if you're installing the library on a remote server
**Virtualization hosts** | Windows Server 2012 onwards | Nano is supported in Windows Server 2016
**Guest operating system** | Windows operating systems [supported by Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)<br/><br/> Linux (CentOS, RHEL, Debian, Oracle Linux, SUSE, Ubuntu)
**PowerShell**: PowerShell 4.0<br/><br/> PowerShell 5.0 |
**.NET** | 4.5, 4.5.1, 4.5.2, 4.6 | Required for VMM console
**.NET** | 4.5.1, 4.5.2, 4.6 | Required for VMM management server
**Host agent** | VMM 2016 | Needed for hosts managed in the VMM compute Fabric
**Monitoring** | System Center Operations Manager 2016 | You also need SQL Server Analysis Services 2014 or later
**VMware** | vCenter 5.1, 5.5, 5.8, 6.0<br/><br/> ESX 5.5, ESX 6.0 | vCenter and ESX servers running these versions can be managed in the VMM Fabric
**Update servers** | WSUS 2012 R2 or later | Used to manage updates in the VMM Fabric
**Bare metal provisioning** | System Management Architecture for Server Hardware (SMASH) v1 or higher over WS-MAN<br/><br/> Intelligent Platform Interface 1.5 or higher<br/><br/> Data Center Manager Interface (DCMI) 1.0 or higher | Required to discover physical bare metal servers and set up an operating system and Hyper-V.
**PXE/WDS Server** | Windows Server 2008 R2 or later | Used for bare metal provisioning


## VMM management server

- You can't run the VMM management server on a Nano server
- The management server computer name cannot exceed 15 characters.
- Don’t install the VMM management server, or other System Center components other than agents, on servers running Hyper-V.
- You can install the VMM management server on a VM. If you do, and you use the Dynamic Memory feature of Hyper-V, then you must set the startup RAM for the virtual machine to be at least 2,048 megabytes (MB).
- If you want to manage more than 150 hosts, we recommend that you use a dedicated computer for the VMM management server and do the following:
    - Add one or more remote computers as library servers, and do not use the default library share on the VMM management server.
    - Don't run the SQL Server instance on the VMM management server.
- For high availability, the VMM management server can be installed on a failover cluster. [Learn more](../plan/plan-ha-deployment.md).

## SQL Server and database

- The instance of SQL Server that you are using must allow for case-insensitive database objects.

- The SQL Server’s computer name cannot exceed 15 characters in length.

- If the VMM management server and the SQL Server computer are not members of the same Active Directory domain, then a two-way trust must exist between the two domains.

- When you install SQL Server, select the **Database Engine Services** and **Management Tools - Complete** features.

- You can perform an in-place upgrade to a supported version of SQL Server (without moving the VMM database). Make sure no jobs are running when you perform the upgrade, or jobs may fail and may need to be restarted manually.

- For the VMM database, for better performance, do not store database files on the disk that is used for the operating system.

- If you are using Software Defined Networking (SDN) in VMM, then all networking information is stored in the VMM database. Because of this, you might want to consider high availability for the VMM database, using the following guidelines:

    - Failover clustering is supported and is the recommended configuration for availability within a single geographical area or datacenter. [Read more](http://technet.microsoft.com/library/ms189134.aspx).

    - Use of AlwaysOn Availability Groups in Microsoft SQL Server is supported, but it's important to review the differences between the two availability modes, synchronous-commit and asynchronous-commit. [Learn more](http://msdn.microsoft.com/library/ff877884.aspx#AvailabilityModes).

        - With asynchronous-commit mode, the replica of the database can be out of date for a period of time after each commit. This can make it appear as if the database were back in time which might cause loss of customer data, inadvertent disclosure of information, or possibly elevation of privilege.

        - You can use synchronous-commit mode as a configuration for remote-site availability scenarios.

- The SQL Server service must use an account that has permission to access Active Directory Domain Services (AD DS). For example, you can specify the Local System Account, or a domain user account. Do not specify a local user account.

- You don't need to configure collation. During deployment, Setup automatically configures CI collation according to the language of the server operating system.

- Dynamic port is supported.
- If you want to create the VMM database prior to VMM installation:
	- Make sure you have permissions or create a SQL database, or ask the SQL Server admin to do it.
	- Configure the database as follows:

		1. Create a new database with settings: Name: VirtualManagerDB; Collation: Latin1_General_100_CI_AS, but aligned with the specific SQL Server instance collation.
		2. Grant db_owner permissions for the database to the VMM service account.
		3. In VMM setup you'll select the option to use an existing database and specify the database details and VMM service account as the database user.


        br/><br/> The SQL Server computer name shouldn't be longer than 15 characters. and the instance should allow for case-insensitive database objects.<br/><br/> THe Server Server can be in the same domain, or in domains with a two-way trust.




## Library server

- If you run the library server on the VMM management server, then you must provide additional hard disk space to store objects. The space required varies, based on the number and size of the objects you store.
- The library server is where VMM stores items such as virtual machine templates, virtual hard disks, virtual floppy disks, ISO images, scripts, and stored virtual machines. The optimal hardware requirements that are specified for a VMM library server vary, depending on the quantity and size of these files. You will need to check CPU usage, and other system state variables to determine what works best in your environment.
- If you want to manage Virtual hard disks in the .vhdx file format, the VMM library server must run Windows Server 2012 or later.
- VMM does not provide a method for replicating physical files in the VMM library or a method for transferring metadata for objects that are stored in the VMM database. Instead, if necessary, you need to replicate physical files outside of VMM, and you need to transfer metadata by using scripts or other means.
- VMM does not support file servers that are configured with the case-sensitive option for Windows Services for UNIX, because the Network File System (NFS) case control is set to **Ignore**.





## Account and domain requirements

When you install VMM you need to configure the VMM service  to use either the Local System account or a domain account. Note the following before you prepare an account:

- It is not supported to change the identity of the Virtual Machine Manager service account after installation. This includes changing from the local system account to a domain account, from a domain account to the local system account, or changing the domain account to another domain account. To change the Virtual Machine Manager service account after installation, you must uninstall VMM (selecting the Retain data option if you want to keep the SQL Server database), and then reinstall VMM by using the new service account.
- If you specify a domain account, the account must be a member of the local Administrators group on the computer.
- If you specify a domain account, it is strongly recommended that you create an account that is specifically designated to be used for this purpose. When a host is removed from the VMM management server, the account that the System Center Virtual Machine Manager service is running under is removed from the local Administrators group of the host. If the same account is used for other purposes on the host, this can cause unexpected results.
- If you plan to use shared ISO images with Hyper-V virtual machines, you must use a domain account.
- If you are using a disjointed namespace, you must use a domain account. For more information about disjointed namespaces, see Naming conventions in Active Directory for computers, domains, sites, and OUs.
- If you are installing a highly available VMM management server, you must use a domain account.
- The computer on which you install the VMM management server must be a member of an Active Directory domain. In your environment you might have user accounts in one forest and your VMM servers and host in another. In this environment, you must establish a two-way trust between the two cross-forest domains. One-way trusts between cross-forest domains are not supported in VMM.

## Distributed key management

 When you install VMM you need to decide where to store the keys to encrypted data on the local computer or configure distributed key management.

	- By default, VMM encrypts some data in the VMM database by using the Data Protection Application Programming Interface (DPAPI). For example, VMM encrypts Run As account credentials and passwords in guest operating system profiles. VMM also encrypts product key information in virtual hard disk properties for virtual machine role scenarios and configuration. The encryption of this data is tied to the specific computer on which VMM is installed and the service account that VMM uses. Therefore, if you move your VMM installation to another computer, VMM will not retain the encrypted data. In that case, you must enter this data manually to fix the VMM objects.
	- Distributed key management, however, stores the encryption keys in AD DS. Therefore, if you must move your VMM installation to another computer, VMM will retain the encrypted data because the other computer will have access to the encryption keys in AD DS.
	- Note that for VMs, if the encrypted data isn't retained you won't be able to enter it manually, so you will not be able to manage the VMs.
	- If you want to enable distributed key management, coordinate with your Active Directory admin. Note that:

		- You must create a container in AD DS before you install VMM. You can create the container by using Active Directory Service Interfaces Editor (ADSI Edit). To install ADSI Edit, in Server Manager add the feature AD DS Tools under Remote Server Administration Tools. After installation, ADSI Edit is listed on the Tools menu in Server Manager.
		- You must create the container in the same domain as the user account with which you are installing VMM. Also, if you specify a domain account that the VMM service will use, that account must also be in the same domain.
		- For example, if the installation account and the service account are both in the corp.contoso.com domain, you must create the container in that domain. So, if you want to create a container that is named VMMDKM, you specify the container location as CN=VMMDKM,DC=corp,DC=contoso,DC=com.
		- After the AD DS administrator has created the container, the account with which you are installing VMM must have Full Control permissions to the container in AD DS. Also, the permissions must apply to this object and all descendant objects of the container.
		- If you are installing a highly available VMM management server, you must use distributed key management to store encryption keys in AD DS.
		- Distributed key management is required in this scenario because when the Virtual Machine Manager service fails over to another node in the cluster, the Virtual Machine Manager service still needs access to the encryption keys in order to access data in the VMM database. This access is possible only if the encryption keys are stored in a central location like AD DS.
		- For future upgrades that involve virtual machine roles, we recommend that you use distributed key management during setup. This will help ensure that virtual machine roles are properly upgraded, and that you can manage them after the upgrade.
		- On the Configure service account and distributed key management page, you must type the location of the container in AD DS, for example: CN=VMMDKM,DC=corp,DC=contoso,DC=com








## Next steps

[Install VMM](../deploy/deploy-install.md)
