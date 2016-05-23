---
title: What&#39;s supported and what isn&#39;t for DPM?
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29d977b5-56de-4bc4-ba0b-2d45d02516a4
---
# What&#39;s supported and what isn&#39;t for DPM?
This topic summarizes some of the common support information you might need when deploying and maintaining [!INCLUDE[scdp_threshold_1](../../Token/scdp_threshold_1_md.md)].

-   [Installation and deployment issues](#BKMK_Install)

-   [Storage issues](#BKMK_Storage)

-   [Deduplication issues](#BKMK_Dedup)

-   [Client and server protection issues](#BKMK_ClientServer)

-   [Data protection issues](#BKMK_Data)

-   [Exchange protection issues](#BKMK_Exchange)

-   [SharePoint protection issues](#BKMK_Sharepoint)

-   [SQL Server protection issues](#BKMK_SQL)

-   [Hyper-V and virtual machine protection issues](#BKMK_VM)

## <a name="BKMK_Install"></a>Installation and deployment issues

### DPM deployment options
**Issue**: DPM can be installed in physical and virtual environments.

**More information**: DPM 2012 can be installed as follows:

-   As a standalone physical server—DPM can’t be deployed in a physical cluster, but you can manage multiple DPM servers from a single location using Central Console in Operations Manager.

-   As an on\-premises virtual machine—You can deploy DPM as a Hyper\-V virtual machine as a single server or virtual machine cluster. You install DPM in the same way as a physical installation. Read [Install DPM as a virtual machine on an on-premises Hyper-V server](assetId:///52ba2825-72de-4079-8947-a2e7baf9602c).

-   As an Azure virtual machine—From DPM 2012 R2 Update 3 onwards you can install DPM as an Azure virtual machine. There are a number of restrictions in this deployment. Read more in [Install DPM as an Azure virtual machine](assetId:///ae43b358-bab6-42b8-94b0-ac216cb9ea43)

-   As a Windows virtual machine in VMWare—From DPM 2012 R2 Update 5 onwards you can install DPM on a Windows virtual machine in a VMWare environment. In this configuration DPM can protect Microsoft workloads that are all running as Windows virtual machines in VMWare.

### System Center 2012 – DPM can’t be installed on servers running Windows Server 2012
**Issue**: Operating system not supported.

**Workaround**: Install [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)] SP1 in order to get [!INCLUDE[dpm2012short](../../Token/dpm2012short_md.md)] running on a server running Windows Server 2012.

### System Center 2012 – DPM with SP1 can’t be installed on servers running Windows Server 2012 R2
**Issue**: Operating system not supported.

**Workaround**: You'll need to upgrade to System Center 2012  R2.

### Sharing a library between different DPM versions isn’t supported
**Issue**: Different versions of DPM \(for example DPM 2012 SP1 and DPM 2012 R2\) can’t function as clients sharing the same library.

**Workaround**: None. All DPM servers sharing a library must be running the same version of DPM.

### Upgrading System Center 2010 directly to System Center Technical Previewo isn’t supported
**Issue**: Upgrade isn’t supported.

**Workaround**: You’ll need to upgrade to DPM 2012 R2 first.

### DPM doesn’t run on the Turkish language version of Windows 2012 operating systems
**Issue**: No language support

**Workaround**: None

### DPM 2010 and later versions can’t run on a server running a 32\-bit operating system
**Issue**: Operating system limitation.

**Workaround**: Install on 64\-bit only. For a full list of system requirements, see [System Requirements for DPM in System Center 2012](http://technet.microsoft.com/library/hh757829.aspx).

### In\-place upgrade of the operating system on a server running DPM isn’t supported
**Issue**: In\-place upgrade isn’t supported.

**Workaround**: Do the following:

1.  Make a backup of the DPM database. You can use the DPMBackup.exe tool to do this. This tool does the following:

    -   Creates a mount point of the backup shadow copies of each replica volume on the DPM server, in the folder Program Files\\Microsoft Data Protection Manager\\DPM\\Volumes\\ShadowCopy\\.

    -   Creates database backups of the DPM database \(DPMDB.mdf\) and the Report database \(ReportServer.mdf\).

    The tool is located on the DPM server in the folder Program Files\\Microsoft Data Protection Manager\\DPM\\bin.  In order to run the tool the SQL Server 2012 SP1 management tools must be installed on the DPM server. The installation file for these is located at \\SCDPM\\SQLSVR2012SP1\\SQLManagementStudio\_X64\_ENU.EXE on the DPM installation media. Note that .NET 3.5 is required before installing these tools.

2.  Make a note of the DPM version and the last update that was installed.

3.  Uninstall DPM. Keep replica data.

4.  Upgrade the operating system and ensure that the DPM storage pool disks are imported.

5.  Install DPM 2012 SP1 or R2.

6.  Restore the DPM database using Dpmsymc –restore DB.

7.  Run DPMSync – Sync to create new mount points.

8.  Run a consistency check to get data sources into a green state.

### Underscore not supported in SQL Server name
**Issue**: If you specify a remote SQL Server that has an underscore in the name during DPM installation, the installation might fail.

**Workaround**: Specify a SQL Server name that doesn’t include the underscore \(“\_”\) character.

### NTFS compression isn’t supported on DPM volumes
**Issue**: NTFS not supported.

**Workaround**: None

### Renaming the DPM server isn’t supported
**Issue**: Renaming not supported.

**Workaround**: None

### Moving the DPM server domain isn’t supported
**Issue**: Moving the DPM server to a different domain after deployment isn’t supported.

**Workaround**: None

### DPM on a domain controller can only protect local data sources
**Issue**: Deployment not supported.

**Workaround**: If you want to install the DPM protection agent on other computers in order to protect them, don’t install DPM on a domain controller.

### DPM can’t use SQL Server running on a domain controller
**Issue**: Database deployment not supported.

**Workaround**: If you want to use a remote instance of SQL Server as your DPM database, ensure that the SQL Server instance isn’t running on a domain controller.

### Moving protected servers with DPM secondary servers
Moving protected servers between DPM servers that are under secondary protection isn’t supported. To illustrate this we have the following:

-   Server1

-   Server2

-   DPM1 acting as primary DPM server

-   DPM2 acting as another primary DPM server

-   DPM3 acting as secondary server for DPM1 and DPM2

Where:

-   Server1 is protected by DPM1

-   Server2 is protected by DPM2

-   DPM3 is a secondary server for DPM1 and DPM2 \(and thus protects Server1 and Server2.

The following occurs:

-   **Scenario 1**

    -   DPM1 fails or is removed from the infrastructure.

    -   You now want to protect Server1 with DPM2 \(with DPM3 acting as the secondary server\).

-   **Scenario 2**

    -   DPM1 fails or is removed from the infrastructure.

    -   You now want to protect Server1 with DPM3.

Both of these scenarios are unsupported. You can only select one of the following options:

-   **Option 1**—Use the “Switch Protection” option on DPM3 for Server1, and leave DPM3 in this mode going forward. Note that in this scenario you can’t add secondary protection for Server1 on another DPM server when you’re using switched protection mode.

-   **Option 2**—Rebuild DPM1 with the same name and restore the DPM database. This allows DPM to resume primary protection.

-   **Option 3**—Move protection for Server1 to a new DPM server \(DPM4\) that DPM3 doesn’t know about.

## <a name="BKMK_Storage"></a>Storage issues

### Using a virtual disk \(.vhd\/.vhdx\) in the DPM storage pool is supported in DPM 2012 R2 only
**Issue**: Storage scenario not supported.

**Workaround**: Install System Center 2012 R2 \- DPM.

### You can’t use Storage Spaces for the DPM disk storage pool
**Issue**: Storage Spaces unsupported.

**Workaround**: None

### References to old tape libraries aren’t removed from the DPM database
**Issue**: Obsolete tape library are still enumerated and listed in DPM PowerShell cmdlets such as get\-dpmlibrary.

**Workaround**: None

### Virtual tape library support
**Issue**: Are virtual tape libraries supported?

**Workaround**: Virtual tape libraries configured with a virtual fibre channel adapter are only supported if you’re running Data Protection Manager 2012 R2 UR3 or later with certified hardware. For a current list of supported hardware see [Compatible Tape Libraries for System Center 2012 DPM](http://go.microsoft.com/fwlink/?LinkID=389995). To check if your tape library is supported by the virtual fibre channel adapter, please contact your tape hardware vendor and ask them to [Verify tape library compatibility](assetId:///a34e5c2e-6216-400a-807b-d7d85c7c4f8b).

### USB or removable drives can’t be used in the DPM storage pool
**Issue**: USB and removable storage such as Firewire.

**Workaround**: None. This isn’t supported due to a limitation with Windows dynamic disks.

### Data on CSVs
Issue: DPM only supports the protection of Hyper\-V virtual machines on Cluster Shared Volumes \(CSVs\). Protecting other workloads hosted on CSVs isn’t supported.

Workaround:::

## <a name="BKMK_Dedup"></a>Deduplication issues

### Deduplicated volumes support
**Issue**: Deduplication support for DPM depends on operating system support.

|Operating system of protected server|Operating system of DPM server|DPM version|Dedup support|
|----------------------------------------|----------------------------------|---------------|-----------------|
|Windows 2012|Windows Server 2012|DPM 2012 with SP1, DPM 2012 R2|Y|
|Windows 2012|Windows Server 2012 R2|DPM 2012 R2|Y|
|Windows Server 2012 R2|Windows Server 2012 R2|DPM 2012 R2|Y|
|Windows Server 2012 R2|Windows Server 2012|DPM 2012 with SP1, DPM 2012 R2|N|

**Workaround**: Use within support limitations.

### Windows deduplication isn’t always supported on volumes hosting .VHD or .VHDX files
**Issue**: Dedupe support

**Workaround**: Deploy DPM as virtual machine.

You can enable deduplication for DPM storage when it runs in a Hyper\-V virtual machine and stored backup data to VHDs in shared folders on Windows File Servers with data deduplication enabled. For more information about this scenario read [Deduplicating DPM storage](assetId:///a681ca08-bf1c-40b6-a9b7-c6fbbc76aeb5).

### Dedup file system can’t be protected to a secondary DPM server
**Issue**: After a dedup file system is protected by a primary DPM server, it can’t be protected to a secondary DPM server.

**Workaround**: None.

### Item\-level recovery not supported
**Issue**: If you’re protecting virtual machines that contain deduped volumes, you can’t perform Item level recovery \(ILR\) from those VHD\/VHDX files.

**Workaround**: Restore the .VHD\/VHDX file that contains the deduped volume to a Windows 2012 R2 server that has the Data Deduplication role installed. Mount the .VHD file in disk management, and copy out the desired files.

## <a name="BKMK_ClientServer"></a>Client and server protection issues

### Support parameters for protecting computers running client operating systems with DPM 2012
**Issue**: The following protection scenarios are supported:

-   Windows 8.1 clients can be protected with DPM 2012 R2 or DPM 2012 with SP1.

-   Windows 8 clients can be protected with DPM 2012, DPM 2012 SP1, and DPM 2012 R2.

-   Windows 7 clients can be protected with DPM 2012, DPM 2012 SP1, and DPM 2012 R2.

-   Windows Vista with SP2 clients can be protected with DPM 2012, and DPM 2012 SP1.

-   Windows Vista or Windows Vista with SP1 clients can be protected with DPM 2012 only.

-   Windows XP SP2 clients can be protected with DPM 2012 only.

**Workaround**: Ensure you’re running the right version of DPM.

### Support for protecting computers running server operating systems with DPM 2012
**Issue**: The following protection scenarios are supported:

-   Windows Server 2012 R2 can be protected with DPM 2012 R2 only.

-   Windows Server 2012 or 2012 with SP1 can be protected with DPM 2012 R2, and DPM 2012 SP1.

-   Windows Server 2008 R2 with SP1, Windows Server 2008 R2 can be protected with DPM 2012, DPM 2012 SP1 and DPM 2012 R2.

-   Windows Server 2008 and Storage Server 2008 can be protected with DPM 2012 R2 running [Update Rollup 2](http://blogs.technet.com/b/dpm/archive/2014/06/11/details-on-protecting-windows-server-2003-computers-using-data-protection-manager-2012-r2.aspx) or later, DPM 2012 SP1, and DPM 2012.

-   Windows 2003 Server with SP2, Windows 2003 Server R2, Windows 2003 Server R2 with SP2 can be protected with DPM 2012 R2 running [Update Rollup 2](http://blogs.technet.com/b/dpm/archive/2014/06/11/details-on-protecting-windows-server-2003-computers-using-data-protection-manager-2012-r2.aspx) or later, DPM 2012 with SP1, And DPM 2012.

**Workaround**: Ensure you’re running the right version of DPM.

### DPM can’t protect SOFS shares
**Issue**: DPM can’t protect shares on SOFS.

**Workaround**: Ensure shares you want to protect aren’t located on SOFS.

## <a name="BKMK_Data"></a>Data protection issues

### Protection might fail when changing the path of a data source
**Issue**: When you protect a shared folder, the path to the shared folder includes the logical path on the volume. If you move the shared folder, protection will fail. In addition if you change the path of a protected data source on a volume that uses the Encrypting File System \(EFS\) and the new file path exceeds 5120 characters, data protection will fail.

**Workaround**: If you must move a protected shared folder, remove it from its protection group and then add it to protection after the move. For an encrypted volume ensure that the new file path of the protected data source uses fewer than 5120 characters.

### Change the domain of a protected resource
**Issue**: You can’t change the domain of a protected computer and continue protection without disruption. In addition you can’t change the domain of a protected computer and associate the existing replicas and recovery points with the computer when it is re\-protected.

**Workaround**: We recommend that you don’t change the domain of a protected computer. If you must change the name of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new name.

### Change the time zone of a protected resource
**Issue**: You can’t change the domain of a protected computer and continue protection without disruption. In addition you can’t change the domain of a protected computer and associate the existing replicas and recovery points with the computer when it is re\-protected.

**Workaround**: We recommend that you don’t change the domain of a protected computer. If you must change the name of a protected computer, then first remove the data sources on the computer from protection. Then protect the data source on the computer after it has a new name.

### Change the name of a protected resource
**Issue**: Ensure you update the time zone correctly if you change it for a protected resource.

**Workaround**: DPM automatically identifies the time zone of a protected computer during installation of the protection agent. If a protected computer is moved to a different time zone after protection is configured, ensure that you change the computer time in Control Panel. Then update the time zone in the DPM database.

### Some data types aren’t supported
**Issue**: DPM doesn’t support the following data types:

-   Hard links

-   Reparse points, including DFS links and junction points

-   Mount point metadata—A protection group can contain data with mount points. In this case DPM protects the mounted volume that is the target of the mount point, but it doesn’t protect the mount point metadata. When you recover data containing mount points, you’ll need to manually recreate your mount point hierarchy.

-   Data in mounted volumes within mounted volumes

-   Recycle Bin

-   Paging files

-   System Volume Information folder. To protect system information for a computer you’ll need to select the computer’s system state as the protect group member.

-   Non\-NTFS volumes

-   Files containing hard links or symbolic links from Windows Vista.

-   Files with any of the following combinations of attributes:

    -   Encryption and reparse

    -   Encryption and Single Instance Storage \(SIS\)

    -   Encryption and case\-sensitivity

    -   Encryption and sparse

    -   Case\-sensitivity and SIS

    -   Compression and SIS

**Workaround**: None

### Limitations on protecting computers in workgroups and untrusted domains
**Issue**: DPM caqn protect workloads in the same domain as the DPM server, or in child and trusted domains. You can also protect the following workloads in  workgroups and untrusted domains using NTLM or certificate authentication:

-   SQL Server

-   File Server

-   Hyper\-V

These workloads can be running on a single server or in a cluster configuration.

**Workaround**: If you want to protect a workload that isn’t in a trusted domain, see [Protect computers in workgroups and untrusted domains](assetId:///1e050ac1-20d7-44e5-97a5-45b245a4f9ee) for exact details of what’s supported and what authentication is required.

### Short\-term backup to tape isn’t supported
**Issue**: DPM doesn’t support short\-term backup \(incremental backup\) to tape for workload data \(Exchange, SQL Server, SharePoint, Hyper\-V\). Only file data \(volumes, shares, folders\) can be backed up incrementally.

**Workaround**: Use disk or a combination of disk and cloud storage \(Azure Backup\) for short\-term backup of these workloads.

### Multiple long\-term tape goals that use dataset\-copy jobs fail if you only have a single tape drive
**Issue**: DPM doesn’t support multiple long\-term backup goals if you only have a single tape drive.

**Workaround**: Add a second tape drive to DPM or to the tape library.

### Backing up data on UPDs \(User Profile Disks\) isn’t supported
**Issue**: Data on file shares hosting UPDs \(User Profile Disks\) can’t be protected by DPM.

**Workaround**: None.

## <a name="BKMK_Exchange"></a>Exchange protection issues

### Disk\-to\-tape backup isn’t supported for Exchange DAG
**Issue**: DPM doesn’t support short\-term or long\-term disk\-to\-tape \(D2T\) backup for Exchange DAG workloads.

**Workaround**: Use disk\-to\-disk\-to\-tape \(D2D2T\) for Exchange DAG workload.

## <a name="BKMK_Sharepoint"></a>SharePoint protection issues

### AlwaysOn not supported
**Issue**: From DPM 2012 R2 Update 5 onwards DPM can protect SharePoint farm SQL Server databases that have Always On enabled.

**Workaround**: None.

## <a name="BKMK_SQL"></a>SQL Server protection issues

### SQL Server 2014 support
**Issue**: You can protect SQL Server 2014 and SQL Server 2012 with SP2 with DPM 2012 R2 with [Update rollup 4](http://go.microsoft.com/fwlink/?LinkId=518078).

**Workaround**: Run the correct DPM version.

### AlwaysOn support
**Issue**: AlwaysOn was introduced in SQL Server 2012. It’s supported from DPM 2012 SP1 onwards in accordance with the [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4).

**Workaround**: None.

### AlwaysOn recovery to original location isn’t supported
**Issue**: When DPM is protecting SQL Server with AlwaysOn enabled data recovery to the original location isn’t supported.

**Workaround**: None.

### DPM can’t protect SQL Server on scale\-out file servers \(SOFS\)
**Issue**: DPM can’t protect SQL Server databases hosted on Windows Server 2012 SOFS.

**Workaround**: Move the SQL Server databases off the SOFS.

## <a name="BKMK_VM"></a>Hyper\-V and virtual machine protection issues

### Linux virtual machines backed up with file\-consistent snapshots only
**Issue**: You can backup Linux virtual machines using DPM 2012 R2. Only file\-consistent snapshots are supported.

**Workaround**: None.

### Backup of Hyper\-V servers and clusters in trusted and untrusted domains
**Issue**: In order to backup Hyper\-V server clusters they must be located in the same domain as the DPM server or in a trusted or child domain. You can back up servers and clusters in an untrusted domain or workload using NTLM or certificate authentication for a single server, or certificate authentication only for a cluster.

**Workaround**: None

### Backing up virtual machine data on pass\-through disks isn’t supported
Issue: DPM doesn’t support the backup of virtual machine data on pass\-through disks that present volumes to the virtual machine or that use a remote VHD.

Workaround: We recommend that in this scenario you use host\-level backup of the VHD files using DPM, and install and agent on the virtual machine to back up data that isn’t visible on the host.

### Secondary DPM protection of a Hyper\-V cluster isn’t supported for a scaled\-out DPM server deployment
**Issue**: When protecting a Hyper\-V cluster using scaled\-out DPM protection, you can’t add secondary protection for the protected Hyper\-V workloads.

**Workaround**: None

### Backup on Hyper\-V Replica servers
**Issue**: Support for backup up of primary and replica \(secondary\) virtual machines depends on the DPM version as summarized in this table.

||**Host operating system on replica \(secondary\/tertiary\) server**|**Host operating system on primary server**|
|-|-----------------------------------------------------------------------|-----------------------------------------------|
||**Windows Server 2012**|**Windows Server 2012 R2**|**Windows Server 2012**|**Windows Server 2012 R2**|
|DPM 2012, 2012 with SP1|Not supported|Not supported|Supported|Not supported|
|DPM 2012 R2|Not supported|Supported|Supported|Supported|

**Workaround**: Run a supported version of DPM for your scenario.

## DPM and Azure

### DPM as an Azure virtual machine
**Issue**: DPM can run as an Azure virtual machine from DPM 2012 R2 Update 3 onwards. Note:

-   On premise DPM Server can’t protect Azure based workloads.

-   DPM running on Azure as an Iaas virtual machine can protect some workloads running as Azure virtual machines. For details see the [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4).

-   DPM running as an Azure virtual machine can’t protect on\-premises workloads.

**Workaround**: For more information about this scenario see [Install DPM as an Azure virtual machine](assetId:///ae43b358-bab6-42b8-94b0-ac216cb9ea43).


