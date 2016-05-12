---
title: Update rollups for System Center 2012 R2 - DPM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7c9111-6738-45e4-9bec-81c5cf58ecbd
---
# Update rollups for System Center 2012 R2 - DPM
This topic summarizes update rollups for System Center 2012 R2 – DPM.

-   [Update rollup 5—February 2015](#BKMK_Update5)

-   [Update rollup 4 – October 2014](#BKMK_Update4)

-   [Update rollup 3—July 2014](#BKMK_UR3)

-   [Update rollup 2—April 2014](#BKMK_UR2)

-   [Update rollup 1—February 2014](#BKMK_UR1)

## <a name="BKMK_Update5"></a>Update rollup 5 – February 2015
This update rollup fix includes:

-   Bugs listed in KB [3021791](http://go.microsoft.com/fwlink/?LinkId=524772).

-   Ability to protect SharePoint with SQL Server Always On—From Update rollup 5 onwards DPM can protection SharePoint farm SQL Server databases that have Always On enabled.

-   Increased support for DPM backup to Azure. We’ve added:

    -   The ability to enable online backup for additional data that’s protected by DPM, including support for backing up protected client computer file data, and SharePoint and Exchange workloads. For more details see [Prerequisites for DPM backup to Azure](https://msdn.microsoft.com/library/azure/dn337337.aspx).

    -   Support to add multiple retention ranges to specify how long backed up DPM data can be stored in Azure— When you’re backing up DPM\-protected data with Azure Backup, you can now configure multiple backup scheduling options and granular retention ranges for the data. This enables you to store data in Azure for long periods \(up to years\), providing an alternative to long\-term tape storage. For details see [Back up DPM workloads with Azure Backup](http://go.microsoft.com/fwlink/?LinkId=524773).

    -   Support to perform offline initial replication of DPM data stored in Azure using the Azure Import feature— If you enable online backup for DPM protection groups that contain large amounts of data, from Update Rollup 5 onwards you can select to do initial replication of the data offline using the Azure Import tool. You copy the data to a hard drive and then send that drive to a Microsoft datacenter where it’s uploaded to your Azure storage account. Read more in [Set up DPM to back up to Azure](http://go.microsoft.com/fwlink/?LinkId=524774).

-   Support for running DPM as a Windows virtual machine in VMWare to protect supported workloads that are also running as VMWare virtual machines. For details of supported workloads see the [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4).

-   In DPM monitoring a new SLA alerts job keeps you up\-to\-date if backup and scheduling service\-level agreements \(SLAs\) aren’t on track. At 12.00 AM on a daily basis the Missed SLA Alerts job runs and collects information for the previous day. For example if you configure a backup every day to run every 8 hours and none of the backups run as expected, three Missed SLA alerts will be issued for that day.

-   A new Operations Manager Management Pack and updated versions of existing Management Packs—This update provides a new DPM Reporting Management Pack. This pack provides a number of predefined views that report on DPM disk and tape management and utilization, performance of backup SLAs, and backup and recovery jobs. Alternatively you can generate reports based on custom queries and views. For an overview see [Monitor DPM with Operations Manager](assetId:///d134518a-83c8-4ff0-bd85-407dd709db43). More detailed documentation is available when you download the management pack.

This update is available through Microsoft Update or by manual download. You can download the package and find installation instructions and information about agent updates in KB [3021791](http://go.microsoft.com/fwlink/?LinkId=524772).

## <a name="BKMK_Update4"></a>Update rollup 4 – October 2014
This update rollup fix includes:

-   Bugs listed in KB [3009516](http://go.microsoft.com/fwlink/?LinkId=518078)

-   Ability to protect SQL Server 2012 SP2 and SQL Server 2014.

-   Ability to run SQL Server 2012 SP2 as the DPM database.

-   Simplified registration process when running DPM with Azure Backup. For details see [Configure Azure storage](assetId:///badf8928-9678-46c3-b444-5ab4ad01596f).

This update is available through Microsoft Update or by manual download You can download the package and find installation instructions in KB [3009516](http://go.microsoft.com/fwlink/?LinkId=518078).

## <a name="BKMK_UR3"></a>Update rollup 3—July 2014
This update rollup fix includes:

-   Bugs listed in KB [2966014](http://go.microsoft.com/fwlink/?LinkId=404310).

-   Ability to deploy and run DPM as an Azure virtual machine. See [Install DPM as an Azure virtual machine](assetId:///ae43b358-bab6-42b8-94b0-ac216cb9ea43).

-   [Scalable virtual machine backup](#BKMK_UR3Scale)

-   [Backup and consistency check scheduling windows](#BKMK_Window)

-   [New certification process](#BKMK_Cert)

This update is available through Microsoft Update or by manual download You can download the package and find installation instructions in KB [2966014](http://go.microsoft.com/fwlink/?LinkId=404310).

### <a name="BKMK_UR3Scale"></a>Scalable virtual machine backup
Update rollup 3 scales backups for Hyper\-V virtual machines using Cluster Shared Volume \(CSV\) storage and scale\-out file server storage. You can run a backup of up to 512 virtual machines on a single DPM server once a day with an SLA of at least 95%.

In order to use this feature you’ll need to install KB [2919355](http://go.microsoft.com/fwlink/?LinkId=404311) on the Hyper\-V host server. If you’re running Hyper\-V in a cluster:

-   Upgrade the DPM agent to the latest version for DPM 2012 R2 Update Rollup 3 on all nodes of the cluster

-   Install KB 2919355 on each cluster node. You’ll need to restart the node after the installation.

### <a name="BKMK_Window"></a>Define backup and consistency check windows
When you scale up backup of virtual machines you need to be able to isolate backup and production windows to make best use of resources. Update rollup 3 allows you to create protection and synchronization windows for virtual machines only. You can create specific time windows that restrict start and finish times for backups and consistency checks. Pending unscheduled jobs outside the window will be cancelled, and in\-progress jobs will be allowed to continue. For instructions see [Configure backup windows for virtual machines](Configure-and-run-backups.md#BKMK_VM).

### <a name="BKMK_Cert"></a>Certification process
Update rollup 3 introduces a certification process for 3rd party tape devices over synthetic fiber channel\-to\-tape. This process is similar to the existing tape certification process for DPM.

## <a name="BKMK_UR2"></a>Update rollup 2—April 2014
This update rollup includes:

-   Bug fixes listed in KB [2958100](http://go.microsoft.com/fwlink/?LinkId=397434).

-   Support for protecting servers running Windows Server 2003.

-   Support for SQL Server 2012 databases deployed in a cluster that are configured to use AlwaysOn availability groups.

### Known issues

-   After installing the protection agent on servers running Windows Server 2003 you might need to perform an agent refresh on the DPM server.

-   If you run the Uninstall Agents wizard to stop protection of a Windows Server 2003 server that is online, the wizard will fail with error 33241: “Microsoft .NET Framework 4 not installed on this computer”. If this occurs do either of the following:

    -   On the protected server manually uninstall the DPM agent using Add\/Remove Programs. Then on the DPM server open an elevated command prompt, navigate to **C:\\Program Files\\Microsoft Data Protection Manager\\DPM\\bin**, and run command: **Remove\-protectionserver.ps1**. Specify the FQDN of the protected server to remove the agent.

    -   Alternatively, manually uninstall the DPM agent on the protected server, shutdown the Windows Server 2003 server or remove it from the network, then run the Unstall Agent wizard and select to remove the DPM record from the DPM database.

-   You’ll need to restart the DPM server after installing the update.

### Set up protection for servers running Windows Server 2003
After you install the update rollup you’ll need to complete a few steps to start protecting servers running Windows Server 2003:

1.  Install the DPM protection agent on the Windows Server 2003 server. The installer is located on the DPM server as follows:

    -   64\-bit agent**—<DPMInstallationLocation>\\DPM\\agents\\RA\\4.2.1224.0\\amd64\\1033\\DPMAgentInstaller\_Win2K3\_AMD64.exe**

    -   32\-bit agent—<**DPMInstallationLocation>\\DPM\\agents\\RA\\4.2.1224.0\\i386\\1033\\DPMAgentInstaller\_Win2K3\_i386.exe**

2.  Open an elevated command prompt and navigate to location: **C:\\Program Files\\Microsoft Data Protection Manager\\DPM\\bin**.

3.  Run the command: **SetDpmServer.exe –dpmservername \[DPM\_SERVERNAME\]**

4.  Attach the protection agent running on the Windows Server 2003 server to the DPM server using either of the following methods:

    -   Run the Protection Agent Installation Wizard. On the **Select Agent Deployment Method** page select **Attach Agents**, and in the **Select Computers** page select the Windows Server 2003 server.

    -   Alternatively, run this Windows PowerShell script on the DPM server: **.\\Attach\-ProductionServer.ps1 <DPMServerName> <Production Server Name> <User Name> <Password> <Domain>**. A password isn’t required.

As an alternative you can perform steps 1 to 3 with a silent install at an elevated command prompt: **\[Installer\].exe \/q \[DPM\_SERVERNAME\] \/IAcceptEULA**. \[DPM\_SERVERNAME\] is optional.

## <a name="BKMK_UR1"></a>Update rollup 1—February 2014
This update rollup includes fixes for:

-   Error 0x80070057—This error occurs when a session is closed prematurely and is caused by a consistency check failure.

-   Slow SQL Server performance—This issue occurs when lots of concurrent calls to the SQL Server from the DPM console cause slow SQL Server performance. The DPM console runs out of connection and might hang or crash.

-   DPM console crash with error “Paths that begin with \\\\?\\GlobalRoot are internal to the kernel and should not be opened by managed applications.

You can get update rollup 1 in Microsoft KB [2904687](http://go.microsoft.com/fwlink/?LinkId=397433).


