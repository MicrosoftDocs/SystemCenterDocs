---
title: Preparing your environment for System Center 2016 - Virtual Machine Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43a08da5-1386-4e74-917d-7beef92de154
---
# Preparing your environment for System Center 2016 - Virtual Machine Manager
Here are the system requirements and considerations to keep in mind before you deploy the [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)] version of [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)].

If you’re evaluating your environment, see LINK\_HERE.

## VMM management server

-   **Windows ADK software**: The  Windows ADK for [!INCLUDE[winthreshold_client_2](../Token/winthreshold_client_2_md.md)] must be installed on the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server. A link to Windows ADK for [!INCLUDE[winthreshold_client_2](../Token/winthreshold_client_2_md.md)] is available from Setup, or you can download it from the [Microsoft Download Center](https://msdn.microsoft.com/windows/hardware/dn913721.aspx). When you install Windows ADK, select the **Deployment Tools** and **Windows Preinstallation Environment** features.

-   **Command Line Utilities for SQL Server**: If you plan to deploy VMM services that use SQL Server data\-tier applications, install the related command\-line utilities on your VMM management server. Install the version of command\-line utilities that matches the version of SQL Server that you are using. The Command Line Utilities are available in the following feature packs:

    -   [Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065)

    -   [Microsoft SQL Server 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295)

    > [!NOTE]
    > If you do not install these utilities, this will not block the installation. These utilities are required if you plan to deploy services that use SQL Server data\-tier applications \(.dacpac files\).

-   **Clustering**: For high availability, the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server can be installed on a failover cluster.

-   **Domain requirements**: The computer on which you install the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server must be a member of an Active Directory domain. In your environment you might have user accounts in one forest and your VMM servers and host in another. In this environment, you must establish a two\-way trust between the two cross\-forest domains. One\-way trusts between cross\-forest domains are not supported in VMM.

-   **Computer name length**: The management server’s computer name cannot exceed 15 characters.

-   **Library server disk space**: If you use the VMM management server also as a library server, then you must provide additional hard disk space to store objects. The space required varies, based on the number and size of the objects you store.

-   **Avoiding installation on a Hyper\-V host**: Don’t install the VMM management server, or other System Center components other than agents, on servers running Hyper\-V. You can install System Center components in virtual machines.

-   **Installing in a virtual machine**: Installing the VMM management server in a virtual machine can help you reduce the number of physical servers that you maintain, and simplify some management tasks. For information about memory and other requirements, see [Minimum Hardware Recommendations for System Center Technical Preview](../Topic/Minimum-Hardware-Recommendations-for-System-Center-Technical-Preview.md).

-   **Dynamic Memory \(for installation as a virtual machine\)**: If you install the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server on a virtual machine and you use the Dynamic Memory feature of Hyper\-V, then you must set the startup RAM for the virtual machine to be at least 2,048 megabytes \(MB\).

-   **Management of more than 150 hosts**: For better performance when you manage more than 150 hosts, we recommend that you use a dedicated computer for the VMM management server and do the following:

    -   Add one or more remote computers as library servers, and do not use the default library share on the VMM management server.

    -   For the VMM database, do not use a SQL Server instance that runs on the same computer on which you install the VMM management server.

For information about how to install a [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, see [How to Install a VMM Management Server](../Topic/How-to-Install-a-VMM-Management-Server.md) and [Installing a Highly Available VMM Management Server](../Topic/Installing-a-Highly-Available-VMM-Management-Server.md).

## [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console
The computer on which you install the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console must be a member of an Active Directory domain.

For information about how to install the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]console, see [Installing and Opening the VMM Console](../Topic/Installing-and-Opening-the-VMM-Console.md).

## SQL Server and database

-   The instance of SQL Server that you are using must allow for case\-insensitive database objects.

-   The SQL Server’s computer name cannot exceed 15 characters in length.

-   If the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server and the SQL Server computer are not members of the same Active Directory domain, then a two\-way trust must exist between the two domains.

-   When you install SQL Server, select the **Database Engine Services** and **Management Tools \- Complete** features.

-   You can perform an in\-place upgrade to a supported version of SQL Server \(without moving the VMM database\). Make sure no jobs are running when you perform the upgrade, or jobs may fail and may need to be restarted manually. For procedures, see the SQL Server documentation, for example, [Upgrade to SQL Server 2014](https://msdn.microsoft.com/library/bb677622(v=sql.120).aspx).

-   For the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database, for better performance, do not store database files on the disk that is used for the operating system. For SQL Server best practices for placement of data and log files, see [Place Data and Log Files on Separate Drives](https://msdn.microsoft.com/library/bb402876(v=sql.120).aspx).

-   If you are using Software Defined Networking \(SDN\) in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], then all networking information is stored in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database. Because of this, you might want to consider high availability for the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database, using the following guidelines:

    -   Failover clustering is supported and is the recommended configuration for availability within a single geographical area or datacenter. For more information, see [AlwaysOn Failover Cluster Instances (SQL Server)](http://technet.microsoft.com/library/ms189134.aspx).

    -   Use of AlwaysOn Availability Groups in Microsoft SQL Server is supported, but it's important to review the differences between the two availability modes, synchronous\-commit and asynchronous\-commit. For a description of the two modes, see the [Availability Modes section in the Overview of AlwaysOn Availability Groups](http://msdn.microsoft.com/library/ff877884.aspx#AvailabilityModes).

        -   With asynchronous\-commit mode, the replica of the database can be out of date for a period of time after each commit. This can make it appear as if the database were back in time which might cause loss of customer data, inadvertent disclosure of information, or possibly elevation of privilege. For more information, see [Reviewing Availability and Recovery Options for Protecting the VMM Database](../Topic/Reviewing-Availability-and-Recovery-Options-for-Protecting-the-VMM-Database.md).

        -   You can use synchronous\-commit mode as a configuration for remote\-site availability scenarios. For more information, see [Overview of AlwaysOn Availability Groups (SQL Server)](http://technet.microsoft.com/library/ff877884.aspx) and [Getting Started with AlwaysOn Availability Groups (SQL Server)](http://technet.microsoft.com/library/gg509118.aspx).

-   The SQL Server service must use an account that has permission to access Active Directory Domain Services \(AD DS\). For example, you can specify the Local System Account, or a domain user account. Do not specify a local user account.

-   You do not need to configure collation. During deployment, Setup automatically configures CI collation according to the language of the server operating system.

-   Dynamic port is supported.

For detailed information about SQL Server and [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)], see[SQL Server Requirements](http://technet.microsoft.com/library/dn281933.aspx) for [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)].

## VMM library
The library server is where VMM stores items such as virtual machine templates, virtual hard disks, virtual floppy disks, ISO images, scripts, and stored virtual machines. The optimal hardware requirements that are specified for a [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server vary, depending on the quantity and size of these files. You will need to check CPU usage, and other system state variables to determine what works best in your environment.

-   To store virtual hard disks in the .vhdx file format, the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server must run Windows Server 2012, [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], or [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)].

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not provide a method for replicating physical files in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library or a method for transferring metadata for objects that are stored in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database. Instead, if necessary, you need to replicate physical files outside of [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], and you need to transfer metadata by using scripts or other means.

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support file servers that are configured with the case\-sensitive option for Windows Services for UNIX, because the Network File System \(NFS\) case control is set to **Ignore**. For more information about the NFS case control, see [Windows Services for UNIX 2.0 NFS Case Control](http://support.microsoft.com/kb/276015).

For more information about library servers in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], see [Configuring the VMM library](../Topic/Configuring-the-VMM-library.md).

## Virtual machine hosts
[!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] supports Microsoft Hyper\-V and VMware ESX as virtual machine hosts.

### Hyper\-V hosts
[!INCLUDE[scvm_threshold_1](../Token/scvm_threshold_1_md.md)] can manage a variety of Hyper\-V hosts. For the complete list of Windows Server Hyper\-V hosts see [Operating Systems Compatibility for System Center Technical Preview](../Topic/Operating-Systems-Compatibility-for-System-Center-Technical-Preview.md).

> [!NOTE]
> The following list describes some features that require hosts that run [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)]:
> 
> -   If you want to use the new networking features in [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] and [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)], the hosts must run [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] \(another choice for the hosts is [!INCLUDE[winthreshold_MSHVS_2](../Token/winthreshold_MSHVS_2_md.md)]\).
> -   If you want to use the new storage features in [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] and [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)], the hosts and any file servers \(such as Scale\-Out File Server clusters\) must run [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] \(another choice for the hosts is [!INCLUDE[winthreshold_MSHVS_2](../Token/winthreshold_MSHVS_2_md.md)]\).

For more information about:

-   Which guest operating systems are supported by Hyper\-V: see [Supported Windows Guest Operating Systems](https://technet.microsoft.com/library/mt126119.aspx) .

-   How to manage Hyper\-V hosts in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]: see [Adding Windows servers as Hyper-V hosts or host clusters in VMM](../Topic/Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

### VM Ware ESX hosts
[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports the following VMware virtualization software:

|Software|Notes|
|------------|---------|
|vCenter Server:<br /><br />-   VMware vCenter Server 5.8<br />-   VMware vCenter Server 5.5<br />-   VMware vCenter Server 5.1|For more information about the requirements for vCenter Server, refer to the VMware product documentation.|
|Virtual machine hosts and host clusters that run any of the following versions of VMware:<br /><br />-   VMware ESXi 5.8<br />-   VMware ESXi 5.5<br />-   VMware ESXi 5.1|The host or host clusters must be managed by a vCenter Server, which is managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|

For more information, see [VMM support for VMware](../Topic/VMM-support-for-VMware.md).

## Bare\-metal deployment of Hyper\-V hosts or additional Scale\-Out File Server nodes
You can use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to find physical computers on the network, automatically install the Windows operating system on these computers, and then convert them into any of the following:

-   Managed Hyper\-V hosts or host clusters

-   Managed Scale\-Out File Server clusters

-   Additional nodes in an existing cluster, either a Hyper\-V host cluster or a Scale\-Out File Server cluster

These physical computers can be computers on which no operating system is installed, often referred to as “bare\-metal" computers. Or these can be computers on which you want to overwrite an existing operating system.

For more information, see [How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM](../Topic/How-to-add-existing-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

|System role|System requirement|
|---------------|----------------------|
|Physical computer to be discovered|Must have a baseboard management controller \(BMC\) with a supported out\-of\-band management protocol. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]supports the following out\-of\-band management protocols:<br /><br />-   Intelligent Platform Management Interface \(IPMI\) versions 1.5 or 2.0<br />-   Data Center Management Interface \(DCMI\) version 1.0<br />-   System Management Architecture for Server Hardware \(SMASH\) version 1.0 over WS\-Management \(WS\-Man\)<br />-   Custom protocols such as Integrated Lights\-Out \(iLO\).<br /><br />Make sure that you use the latest version of firmware for the baseboard management controller \(BMC\) model.|
|PXE Server that is used to initiate the operating system installation on the physical computer.|A server with the Windows Deployment Services role installed. The server can run any of the following:<br /><br />-   [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)]<br />-   [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)]<br />-   Windows Server 2012<br />-   Windows Server 2008 R2<br /><br />The PXE server needs to be in the same subnet as the out\-of\-band computer.|
|Image operating system for provisioning non\-clustered hosts from bare metal|-   [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] operating system image<br />-   [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] operating system image<br />-   A Windows Server 2012 operating system image<br />-   A Windows Server 2008 R2 Service Pack 1 operating system image<br /><br />The operating system image must support the option to boot from virtual hard disk.<br /><br />You can create the virtual hard disk by running the System Preparation Tool \(Sysprep.exe\). Use Sysprep.exe with both the \/generalize and the \/oobe options on a virtual machine that runs the operating system that will be on the image.|
|Image operating system for creating a cluster from bare metal, either a host cluster or a Scale\-Out File Server Cluster|-   [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] operating system image<br />-   [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] operating system image<br />-   Windows Server 2012 operating system image<br /><br />The operating system image must support the option to boot from virtual hard disk.<br /><br />You can create the virtual hard disk by running the System Preparation Tool \(Sysprep.exe\). Use Sysprep.exe with both the \/generalize and the \/oobe options on a virtual machine that runs the operating system that will be on the image.|

## Update management
In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] you can use a Windows Server Update Services \(WSUS\) server to manage updates for the following computers in your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] environment:

-   Virtual machine hosts

-   Library servers

-   VMM management server

-   PXE servers

-   The WSUS server

-   Infrastructure servers running [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)]. For example, you could add a DHCP server as an infrastructure server in your VMM environment, and update it when you update other servers in your environment.

You can configure the update baselines, scan computers for compliance, and perform update remediation.

|Supported WSUS servers|Notes|
|--------------------------|---------|
|-   [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)], Windows Server Update Services \(WSUS\)  server role<br />-   [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], WSUS server role|-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports using a WSUS server that is part of a Configuration Manager environment, but additional configuration steps are required. For more information, see[How to Integrate Fabric Updates with Configuration Manager](http://technet.microsoft.com/library/hh341476.aspx).|

-   There must be full trust between the WSUS management server and the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server domains.

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can use either a WSUS root server or a downstream WSUS server. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support using a WSUS replica server.

-   The WSUS server can either be dedicated to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] or can be a WSUS server that is already in use in your environment.

-   If [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will process a very large volume of updates, consider installing the WSUS server on a separate computer from the VMM management server.

-   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can also work with System Center Updates Publisher, but only full content updates are supported. Metadata\-only updates cannot be added to an update baseline.

For more information about update management in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], see [Managing fabric updates in VMM](../Topic/Managing-fabric-updates-in-VMM.md).

## Monitoring and reporting
[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can monitor the health and performance of virtual machines and their hosts. To do so, VMM integrates with Operations Manager and enables Performance and Resource Optimization \(PRO\). VMM also provides the capability to use the reporting functionality of Operations Manager.

[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)] supports the following versions of Operations Manager:

-   Operations Manager in [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)]

-   Operations Manager in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)]

Requirements:

-   Operations Manager must use SQL Server 2012 SP2 or SQL Server 2014 with reporting services enabled. To use the forecasting reports, SQL Server Analysis Services must be installed on the Operations Manager reporting server.

-   The version of the Operations Manager operations console that is installed on the VMM management server must match the version of Operations Manager with which you intend to integrate.

-   The version of the Operations Manager agent should be supported by the respective version of Operations Manager.

For more information, see [Configuring Operations Manager Integration with VMM](https://technet.microsoft.com/library/hh427287.aspx).

