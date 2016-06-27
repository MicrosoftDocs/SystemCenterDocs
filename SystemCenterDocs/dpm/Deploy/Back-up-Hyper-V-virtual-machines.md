---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Back up Hyper V virtual machines
ms.technology:  data-protection-manager
ms.assetid:  3a5b0841-04c8-4ffa-8375-ef12b7b459bb
---

# Back up Hyper-V virtual machines

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

DPM protects Hyper-V virtual machines by backing up virtual machines data. You can back data up at the Hyper-V host level to enable VM-level and file-level data recovery, or back up at the guest-level to enable application-level recovery.

## Supported scenarios
DPM can back up virtual machines running on Hyper-V host servers in the following scenarios:

-   **Virtual machines with local or direct storage**—Back up virtual machines hosted on Hyper-V host standalone servers that have local or directly attached storage. For example a hard drive, a storage area network (SAN) device, or a network attached storage (NAS) device. The DPM protection agent must be installed on all hosts.

-   **Virtual machines in a cluster with CSV storage**—Back up virtual machines hosted on a Hyper-V cluster with Cluster Shared Volume (CSV) storage. DPM 2012 SP1 introduced express full backup, parallel backups, and cluster query improvements for CSV backup. The DPM protection agent is installed on each cluster node.

-   **Virtual machines with SMB storage**—Back up virtual machines hosted on a Hyper-V standalone server or cluster with SMB 3.0 file server storage. SMB shares are supported on a standalone file server or on a file server cluster. If you’re using an external SMB 3.0 file server the DPM protection agent should be installed on it. If the storage server is clustered, the agent should be installed on each cluster node. You’ll need full-share and folder-level permissions for the machine$ account of the application server on the SMB share.

-   **[Back up virtual machines configured for live migration](#BKMK_Live)**—Live migration allows you to move virtual machines from one location to while providing uniterrupted access. You can migrate virtual machines between two standalone servers, within a single cluster, or between standalone and cluster nodes. Multiple live migrations can run concurrently. You can also perform a live migration of virtual machine storage so that virtual machines can be moved to new storage locations while they continue to run.  DPM can back up virtual machines that are configured for live migration. Read more.

-   **[Back up replica virtual machines](#BKMK_Replica)**—Back up replica virtual machines running on a secondary server (DPM 2012 R2 only)

Learn about supported DPM and Hyper-V versions in [What can DPM back up?](../get-started/What-can-DPM-back-up-.md) .

## <a name="BKMK_Online"></a>Host v guest backup
DPM can perform a host or guest-level backup of Hyper-V VMs. At the host level the DPM protection agent is installed on the Hyper-V host server or cluster and protects the entire VMs and data files running on that host.   At the guest level the agent is installed on each virtual machine and protects the workload present on that machine.

Both methods have pros and cons:

-   Host-level backups are flexible because they work regardless of the type of OS running on the guest machines and don't require the installation of the DPM protection agent on each VM. If you deploy host level back you’ll be able to recover an entire virtual machine, or files and folders (item-level recovery).

-   Guest-level back is useful if you want to protect specific workloads running on a virtual machine. At host-level you can recover an entire VM or specific files, but it won't provide recover in the context of a specific application. For example to be able to recover specific SharePoint items from a backed up VM then you should do guest-level backup of that VM. Note that you must use guest-level backup if you want to protect data stored on passthrough disks. Passthrough allow the virtual machine to directly access the storage device and don’t store virtual volume data in a VHD file.

## Online and offline backup
DPM works seamlessly with the Hyper-V Volume Shadow Copy Services (VSS)  writer to ensure that consistent versions of virtual machines are captured and protected without affecting virtual machine access. The ability to back up open files is critical for business continuity. By default DPM performs online backups that don’t affect the availability of virtual machines. To perform an online backup the following is required:

-   The Backup integration service must be enabled, so the operating system running on the virtual machine running must support Hyper-V integration services.

-   The guest operating system must support VSS (Windows 2003 server or later). Online backup isn’t supported if virtual machines are running Linux.

-   There should be no dynamic disks on the virtual machine.

-   All volumes must be NTFS

-   The VSS storage assigment for the volumes shouldn’t be modified.

-   The virtual machine must be running, and if the virtual machine is in a cluster the cluster resource group should be online. A Shadow Storage assignment of a volume inside the virtual machine mustn’t be explicitly set to a different volume other than itself.

If these conditions aren’t met DPM will perform an offline backup where the virtual machine is paused and placed in a saved state while the snapshot is taken, and then the virtual machine is resumed. This means the virtual machine is unavailable during the backup, usually a short period of less than a minute for many environments.

## Backup process
DPM performs backup with VSS as follows:

1.  The DPM block-based synchronization engine makes an initial copy of the protected virtual machine and ensures that the copy of the virtual machine is complete and consistent.

2.  After the initial copy is made and verified, DPM captures backups by using the Hyper-V VSS writer. The VSS writer provides a data-consistent set of disk blocks that are synchronized with the DPM server. This approach provides the benefit of a "full backup" with the DPM server while it minimizes the amount of backup data that have to be transferred across the network.

3.  The DPM protection agent on a server that is running Hyper-V uses the existing Hyper-V APIs to determine whether a protected virtual machine also supports VSS.

    -   If a virtual machine complies with the requirements for online backup and has the Hyper-V integration services component installed, then the Hyper-V VSS writer recursively forwards the VSS request through to all VSS-aware processes on the virtual machine. This operation occurs without the DPM protection agent being installed on the virtual machine. This recursive VSS request allows the Hyper-V VSS writer to ensure that disk write operations are synchronized so that a VSS snapshot is captured without the loss of data.

        The Hyper-V integration services component invokes the Hyper-V VSS writer in Volume Shadow Copy Services (VSS) on virtual machines to ensure that their application data is in a consistent state.

    -   If the virtual machine doesn’t comply with online backup requirements, DPM automatically uses the Hyper-V APIs to pause the virtual machine before they capture data files.

4.  After the initial baseline copy of the virtual machine synchronizes with the DPM server, all changes that are made to the virtual machine resources are captured in a new recovery point. The recovery point represents the consistent state of the virtual machine at a specific time. Recovery point captures can occur at least one time a day. When a new recovery point is created, DPM uses block-level replication in conjunction with the Hyper-V VSS writer to determine which blocks have been altered on the server that is running Hyper-V after the last recovery point was created. These data blocks are then transferred to the DPM server and are applied to the replica of the protected data.

5.  The DPM server uses VSS on the volumes that host recovery data so that multiple shadow copies are available. Each of these shadow copies provides a separate recovery. VSS recovery points are stored on the DPM server. The temporary copy that is made on the server that is running Hyper-V is only stored for the duration of the DPM synchronization.

## Backup prerequisites
These are the prerequisites for backing up 
Hyper-V virtual machines with DPM.

|||
|-|-|
|DPM prerequisites|-   If you want to perform item-level recovery for virtual machines (recover files, folders, volumes) then you’ll need to install the Hyper-V role on the DPM server.  If you only want to recover the virtual machine and not item-level then the role isn’t required.<br />-   You can protect up to 800 virtual machines of 100 GB each on one DPM server and allows multiple DPM servers that support larger clusters.<br />-   DPM excludes the page file from incremental backups to improve virtual machine backup performance.<br />-   DPM can backup a Hyper-V server or cluster in the same domain as the DPM server, or in a child or trusted domain. If you want to backup Hyper-V in a workgroup or an untrusted domain  you’ll need to set up authentication. For a single Hyper-V server you can use NTLM or certificate authentication. For a cluster you can use certificate authentication only.<br />-   Using host-level backup to back up virtual machine data on passthrough disks isn’t supported. In this scenario we recommend you use host-level back to backup VHD files and guest-level back to back up the other data that isn’t visible on the host.<br />-   When protecting a Hyper-V cluster using scaled-out DPM protection (multiple DPM server protecting a large Hyper-V cluster) you can’t add secondary protection for the protected Hyper-V workloads.<br />-   You can only backup replica virtual machines if DPM is running System Center 2012 R2 and the Hyper-V host is running on Windows Server 2012 R2.<br />-   You can back up deduplicated volumes.|
|Hyper-V VM prerequisites|-   The version of Integration Components that is running on the virtual machine should be the same as the version of Hyper-V on the server that is running Hyper-V.<br />-   For each virtual machine backup you’ll need free space on the volume hosting the virtual hard disk files to allow Hyper-V enough room for differencing disks (AVHD’s) during backup. The space must be at least equal to the calculation **Initial disk size\*Churn rate\*Backup** window time. If you’re running multiple backups on a cluster, you’ll need enough storage capacity to accommodate the AVHDs for each of the virtual machines using this calculation.<br />-   If you want to backup virtual machines located on a Hyper-V host servers running Windows Server 2012 R2, the virtual machine should have a SCSI controller specified, even if it’s not connected to anything. This is because for online backup in Windows Server 2012 R2 the Hyper-V host mounts a new VHD in the VM and then dismounts it later. Only the SCSI controller can support this and thus is required for online backup of the virtual machine. The SCSI controller doesn’t  it became clear why we need this SCSI controller. Without this setting, event ID 10103 will be issued when you try to back up the virtual machine.|
|Linux prerequisites|-   You can backup Linux virtual machines using DPM 2012 R2. Only file-consistent snapshots are supported.|
|Back up VMs with CSV storage|-   For CSV storage, install the Volume Shadow Copy Services (VSS) hardware provider on the Hyper-V server. Contact your storage area network (SAN) vendor for the VSS hardware provider.<br />-   If a single node shuts down unexpectedly in a CSV cluster, DPM will perform a consistency check against the virtual machines that were running on that node.<br />-   If you need to restart a Hyper-V server that has BitLocker Drive Encryption enabled on the CSV cluster, you must run a consistency check for Hyper-V virtual machines.|
|Back up VMs with SMB storage|-   Turn on auto-mount on the server that is running Hyper-V to enable virtual machine protection.<br />    •<br />-   Disable TCP Chimney Offload.<br />-   Ensure that all Hyper-V machine$ accounts have full permissions on the specific remote SMB file shares.<br />-   Ensure that the file path for all virtual machine components during recovery to alternate location is less than 260 characters. If not, recovery might succeed, but Hyper-V cannot mount the virtual machine.<br />-   The following scenarios are not supported:<br />     Deployments where some components of the virtual machine are on local volumes and some components are on remote volumes; an IPv4 or IPv6 address for storage location file server., and recovery of a virtual machine to a computer that uses remote SMB shares.<br />-   You'll need to enable the File Server VSS Agent service on each SMB server—Add it in **Add roles and features** > **Select server roles** > **File and Storage Services** > **File Services** > **File Service** > **File Server VSS Agent Service**.|

## Back up virtual machines

1.  Set up DPM and  storage.

2.  Set up [DPM](https://technet.microsoft.com/en-us/library/mt403314.aspx) and [storage](https://technet.microsoft.com/en-us/library/mt617323.aspx). You can use these storage capacity guidelines.

    |||
    |-|-|
    |Average virtual machine size|100 GB|
    |Number of virtual machines per DPM server|800|
    |Total size of 800 VMs|80 TB|
    |Required space for backup storage|80 TB|

3.  Set up the DPM protection agent on the Hyper-V server or Hyper-V cluster nodes. If you're doing guest-level backup you'll install the agent on the VMs you want to back up at the guest-level.

4.  In  the DPM Administrator console click **Protection** > **Create protection group** to open the **Create New Protection Group** wizard.

    -   On the **Select Group Members** page, select the VMs you want to protect from the Hyper-V host servers on which they're located. We recommend you put all VMs that will have the same protection policy into the same protection group. You can enable colocation for efficient use of space. Colocation allows you to locate data from different protection groups on the same disk or tape storage so that multiple data sources have a single replica and recovery point volume.

    -   On the **Select Data Protection Method** page, specify a protection group name. Select **I want short-term protection using Disk** and select **I want online protection** if you want to back up data to Azure using the Azure Backup service. If this option isn’t available complete the wizard to create the group and then modify the protection group settings to select this option. You can store data in Azure for up to 3360 days.

        If you have a standalone tape or tape library connected to the DPM server you’ll be able to select **I want long-term protection using tape**.

    -   In **Specify Short-Term Goals** > **Retention range**, specify how long you want to retain disk data. In **Synchronization frequency** specify how often incremental backups of the data should run. Alternatively, instead of selecting an interval for incremental backups you can enable **Just before a recovery point**. With this setting enabled DPM will run an express full back just before each scheduled recovery point.

        If you’re protecting application workloads, recovery points are create in accordance with Synchronization frequency if the application supports incremental backups. If it doesn’t then DPM runs an express full backup instead of incremental, and creates recovery points in accordance with the express backup schedule that you can configure.

    -   If you enable long-term storage to tape, in **Specify Long-Term Goals** > **Retention range**, specify how long you want to keep your tape data (1-99 years).
        In Frequency of backup  select the backup frequency that you want.

        The backup frequency is based on the specified retention range. When the retention range is 1–99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.
        When the retention range is 1–11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.
        When the retention range is 1–4 weeks, you can select backups to occur daily or weekly.

        On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. Data resources will be colocated on the tape if you enabled colocation.

        If you configured long-term storage to tape, on the **Select Tape and Library Details** page, specify the tape and library that’ll be used for back up of this protection group. You can also specify whether to compress or encrypt the backup data.

    -   On the **Review Disk Allocation** page recommended disk allocations are displayed. Recommendations are based on the retention range, the type of workload and the size of the protected data.
        Data size indicates the zize of data in protection group.
        Disk space indicates the amount of disk space DPM recommends for allocation to the protection group.
        If **Automatically grow** is enabled  you enable this setting, if data in the protected group outgrows the initial allocations, DPM will try to automatically increase the disk size by 25%
         if data outgrows the initial allocations.

    -   On the **Choose Replica Creation Method** page, specify how the initial replication of data in the protection group will be performed. If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

    -   On the **Consistency Check Options** page, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don’t want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group and selecting **Perform Consistency Check**.

    After you create the protection group initial replication of the data occurs in line with the method you selected. After initial replication backup takes place in line with the protection group settings. If you need to recover backed up data note the following:

## <a name="BKMK_Live"></a>Back up virtual machines configured for live migration
When virtual machines are involved in live migration DPM can continue to protect them as long as the DPM protection agent is installed on the Hyper-V host.  The way in which DPM protects them will depend on the type of live migration involved.

-   **Live migration within a cluster**— When a virtual machine is migrated within a cluster DPM detects the migration, and backs up the virtual machine from the new cluster node without any requirement for user intervention. Because the storage location hasn't changed, DPM continues with express full backups. In a scaled scenario with two DPM servers to protect the cluster, a virtual machine that is protected by DPM1 continues to be protected by DPM1, no matter where the virtual machine is migrated.

-   **Live migration outside the cluster**—When a virtual machine is migrated between stand-alone servers, different clusters, or between a stand-alone server and a cluster, DPM detects the migration, and can back up the virtual machine without user intervention.
                   But there are some requirements:

    -   The Hyper-V hosts for the virtual machines must be located in a System Center VMM cloud on a VMM server running at least System Center 2012 with SP1.

    -   The DPM protection agent must be installed on all Hyper-V hosts.

    -   DPM servers must be connected to the VMM server. All the Hyper-V host servers in the VMM cloud must also be connected to the DPM servers

        This allows DPM to communicate with the  VMM server to find out on which Hyper-V host server the virtual machine is currently running and to create a new backup from that Hyper-V server.  If a connection can't be established to the Hyper-V server the backup fails with a message that the DPM protection agent is unreachable.

    -   All DPM servers, VMM servers, and Hyper-V host servers should be in the same domain.

Note the following for  backup during live migration:

-   Live migration protection doesn't support backup to tape.

-   If a live migration transfers storage, DPM performs a full consistency check of the virtual machine, and then continues with express full backups. When live migration of storage occurs, Hyper-V reorganizes the virtual hard disk (VHD) or VHDX and therefore there is a one-time spike in the size of DPM backup data.

-   You'll need to turn on auto-mount on the virtual machine host to enable virtual protection, and disable TCP Chimney Offload.

-   If you want to change the default port of 6070 used by DPM to host the DPM-VMM Helper Service change the registry. Navigate to HKLM\Software\Microsoft\Microsoft Data Protection Manager\Configuration. Create a 32-bit DWORD value: DpmVmmHelperServicePort, and write the updated port number as part of the registry key.
    Open <Install directory>\Microsoft System Center 2012\DPM\DPM\VmmHelperService\VmmHelperServiceHost.exe.config and change the port number from 6070 to the new port. For example: <add baseAddress="net.tcp://localhost:6080/VmmHelperService/" \/>
    Restart the DPM-VMM Helper service and restart the DPM service.

Set up protection as follows:

-   Set up DPM and storage, and install the DPM protection agent on every Hyper-V host server or cluster node in the VMM cloud. If you're using SMB storage in a cluster, install the DPM protection able on all cluster nodes.

-   Install the VMM console as a client component on the DPM server so that DPM can communicate with the VMM server. The console should be the same version as that running on the VMM server.

-   Assign the  DPMMachineName$ account as a read-only administrator account on the VMM management server.

-   Connect all Hyper-V host servers to all DPM server with the  Set-DPMGlobalProperty PowerShell command .The cmdlet accepts multiple DPM server names.  Use the format: `Set-DPMGlobalProperty -dpmservername <dpmservername> -knownvmmservers <vmmservername>`. For more information see [Set-DPMGlobalProperty](http://technet.microsoft.com/library/hh881752.aspx).

-   After all virtual machines running on the Hyper-V hosts in the VMM clouds are discovered in VMM, set up a protection group and add virtual machines you want to protect.  Note that automatic consistency check should be enabled at the protection group level for protection under virtual machine mobility scenarios.

-   After settings are configured, when a virtual machine migrates from one cluster to another, all backups continue as expected. You can verify live migration is enabled as expected as follows:

    1.  Check the DPM-VMM Helper Service is running. If it isn’t start it.

    2.  Open Microsoft SQL Server Management Studio and connect to the instance that hosts the DPM database (DPMDB). On DPMDB run the following query: `SELECT TOP 1000 [PropertyName] ,[PropertyValue] FROM[DPMDB].[dbo].[tbl_DLS_GlobalSetting]`

        This query contains a property, called `KnownVMMServer`. This value should be the same as the value that you provided with the `Set-DPMGlobalProperty` cmdlet.

    3.  Run the following query to validate the *VMMIdentifier* parameter in the `PhysicalPathXML` for a particular virtual machine. Replace `VMName` with the name of the virtual machine.

        `select cast(PhysicalPath as XML) from tbl_IM_ProtectedObject where DataSourceId in (select datasourceid from tbl_IM_DataSource where DataSourceName like '%<VMName>%')`

    4.  Open the .xml file that this query returns and validate that the *VMMIdentifier* field has a value.

**Run manual migration**—After you’ve completed the steps migration is enabled after the DPM Summary Manager job runs. By default, this job starts at midnight and runs every morning. If you want to run a manual migration in the meantime to check everything is working as expected, do the following:

1.  Open SQL Server Management Studio and connect to the instance that hosts DPMDB.

2.  Run the following query: `select * from tbl_SCH_ScheduleDefinition where JobDefinitionID=’9B30D213-B836-4B9E-97C2-DB03C3EB39D7’`. Note that the query returns the **ScheduleID**.

3.  In SQL Server Management Studio, expand **SQL Server Agent**, and then expand **Jobs**. Right-click the **ScheduleID** that you noted, and select **Start Job at Step**.

Note that backup performance is affected when the job runs. The size and scale of your deployment determines how much time the job takes to finish.

## <a name="BKMK_Replica"></a>Back up replica virtual machines
You can back up replica virtual machines on a secondary server if DPM is running Windows Server 2012 R2. This is useful for a couple of reasons:

-   Reduces the impact of backups on running workload—Taking a backup of a virtual machine incurs some overhead as a snapshot is created. By offloading the backup process to a secondary remote site, the running workload is no longer impacted by the backup operation. Obviously this is applicable only to deployments where the backup copy is stored on a remote site. For example, you might take daily backups and store data locally to ensure quick restore times, but take monthly or quarterly backups from replica virtual machines stored remotely for long-term retention.

-   Saves bandwidth—In a typical remote branch office/headquarters deployment you’ll need an appropriate amount of bandwidth is provisioned by administrators to transfer backup data between sites. If you deploy some type of replication and failover strategy in addition to your data backup strategy, you might be sending copies of the same data over the network. By backing up the replica virtual machine data rather than the primary you’ll save the overhead of sending that backed up data over the network.

-   Enables hoster backup—Customers might use a datacenter hosted by a hoster as a replica site, with no secondary datacenter of their own. In this case the hoster SLA will require consistent backup of replica virtual machines.

A replica virtual machine is  turned off until a failover is initiated, and VSS can’t guarantee an application-consistent backup for a replica virtual machine. Thus the backup of a replica virtual machine will be crash-consistent only. If crash- consistency can’t be guaranteed then the backup will fail and this might occur in a number of conditions:

-   The replica virtual machine isn’t healthy and is in a critical state.

-   The replica virtual machine is resynchronizing (in the Resynchronization in Progress or Resynchronization Required state).

-   Initial replication between the primary and secondary site is in progress or pending for the virtual machine.

-   .hrl logs are being applied to the replica virtual machine, or a previous action to apply the .hrl logs on the virtual disk failed, or was cancelled or interrupted.
    .

-   Migration or failover of the replica virtual machine is in progress

## Recover backed up virtual machines
You can recover backed up virtual machines. In the DPM Administrator console you select the virtual machine, and specify the point from which you want to recover the data. In the Recovery Wizard you select recovery settings:

1.  Select the VMs you want to recover and on the calendar, click any date to see the recovery points available. Select the recovery point you want to use on the **Recovery time** menu. Then in **Actions** click **Recover**. Select where you want to restore the data.

    -   **Recover to original location**: When you recover to the original location the original VHD is deleted.  DPM will recover the VHD and other configuration files on the original location using Hyper-V VSS writer. At the end of the recovery process, virtual machines will still be highly available.
        The resource group must be present for recovery. If it isn’t available recover to an alternate location and then make the virtual machine highly available.

    -   **Recover to alternate location**: DPM supports alternate location recovery (ALR), which provides a seamless recovery of a protected Hyper-V virtual machine to a different Hyper-V host, independent of processor architecture. Hyper-V virtual machines that are recovered to a cluster node will not be highly available.

    -   **Item-level recovery**: DPM supports item-level recovery (ILR), which allows you to do item-level recovery of files, folders, volumes, and virtual hard disks (VHDs) from a host-level backup of Hyper-V virtual machines to a network share or a volume on a DPM protected server. The DPM protection agent doesn’t have to be installed inside the guest to perform item-level recovery.

In **Specify Recovery Options** you can configure the recovery options for SAN, network bandwidth usage throttling if you're recovering over low bandwidth, and email notifications to specify when the restore job finishes, and complete the wiard.



