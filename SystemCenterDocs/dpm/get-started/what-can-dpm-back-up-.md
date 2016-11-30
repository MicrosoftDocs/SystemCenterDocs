---
description: A complete matrix of all workloads, data types, and installations that DPM 2016 protects.  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 11/29/2016
title:  What can DPM back up
ms.technology:  data-protection-manager
ms.assetid:  2ddbf72a-a82a-497e-afe1-672c8b253ed4
ms.author: markgal
---

# What can DPM back up?

>Applies To: System Center 2016 - Data Protection Manager

## Protection support matrix

|Workload|Version|DPM installation|DPM - System Center 2016|DPM - System Center 2012 R2|Protection and recovery|
|------------|-----------|--------------------|--------------------------------------------|--------------------------------|---------------------------|
|System Center VMM|VMM 2016,<br/>VMM 2012, SP1, R2|Physical server<br /><br />Hyper-V virtual machine|Y|Y|All deployment scenarios: Database|
|Client computers (64-bit and 32-bit)|Windows 10|Physical server<br /><br />Hyper-V virtual machine<br /><br />VMware virtual machine|Y|Y<br />From Update rollup 7 onwards|Files<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8.1|Physical server<br /><br />Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS. FAT and FAT32 aren't supported.<br /><br />Volumes must be at least 1 GB. DPM uses Volume Shadow Copy Service (VSS) to take the data snapshot and the snapshot only works if the volume is at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8.1|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y<br /><br />From Update Rollup 5 onwards|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 8|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y<br /><br />From Update Rollup 5 onwards|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 7|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows 7|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from Update Rollup 5 onwards)|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows Vista with SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows Vista with SP1|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows Vista|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Files<br /><br />Protected volumes must be NTFS and at least 1 GB.|
|Client computers (64-bit and 32-bit)|Windows Vista|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal), deduped volumes|
|Servers (32-bit and 64-bit)|Windows Server 2016|Azure virtual machine (when workload is running as Azure virtual machine)<br /><br />Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)<br /><br />Physical server<br /><br />On-premises Hyper-V virtual machine|Y<br /><br />Not Nano server|N|Volume, share, folder, file, system state/bare metal), deduped volumes|
|Servers (32-bit and 64-bit)|Windows Server 2012 R2 - Datacenter and Standard|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|Volume, share, folder, file<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012 R2 - Datacenter and Standard|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal)<br /><br />DPM must be running on Windows Server 2012 or 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 Update Rollup 3 onwards)|Volume, share, folder, file<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2012/2012 with SP1 - Datacenter and Standard|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal<br /><br />DPM must be running on at least Windows Server 2012 R2 to protect Windows Server 2012 deduped volumes.|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Physical server<br /><br />On-premises Hyper-V virtual machine|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855)|Y|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Azure virtual machine (when workload is running as Azure virtual machine)|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855)|Y (from DPM 2012 R2 Update Rollup 3 onwards)|Volume, share, folder, file|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2 SP1 - Standard and Enterprise|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y<br /><br />You need to be running SP1 and install [Windows Management Frame 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855)|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Azure virtual machine (when workload is running as Azure virtual machine)|N|Y (from DPM 2012 R2 Update Rollup 3 onwards)|Volume, share, folder, file|
|Servers (32-bit and 64-bit)|Windows Server 2008 R2|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|N|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008|Physical server<br /><br />On-premises Hyper-V virtual machine|N|Y (from DPM 2012 R2 with [Update Rollup 2](http://blogs.technet.com/b/dpm/archive/2014/06/11/details-on-protecting-windows-server-2003-computers-using-data-protection-manager-2012-r2.aspx))|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Server 2008|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Storage Server 2008|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y (from DPM 2012 R2 with [Update Rollup 2](http://blogs.technet.com/b/dpm/archive/2014/06/11/details-on-protecting-windows-server-2003-computers-using-data-protection-manager-2012-r2.aspx))|Volume, share, folder, file, system state/bare metal|
|Servers (32-bit and 64-bit)|Windows Storage Server 2008|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Volume, share, folder, file, system state/bare metal|
|SQL Server|SQL Server 2016|Physical server and Azure virtual machine|N|N|All scenarios|
|SQL Server|SQL Server 2014|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2014|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y (from DPM 2012 R2 with [Update rollup 4](http://go.microsoft.com/fwlink/?LinkId=518078))|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2012 with SP2|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2012, SQL Server 2012 with SP1|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2008 R2|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2008|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2005 with SP2|Physical server<br /><br />On-premises Hyper-V virtual machine|N|Y|All deployment scenarios: database|
|SQL Server|SQL Server 2005 with SP2|Azure virtual machine (when workload is running as Azure virtual machine)|N|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|All deployment scenarios: database|
|SQL Server|SQL Server 2005 with SP2|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|N|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|All deployment scenarios: database|
|Exchange|Exchange 2016|Physical server<br/><br/> On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2016|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2013|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2013|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios): Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2010|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover  (all deployment scenarios):  Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2010|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios): Standalone Exchange server, database under a database availability group (DAG)<br /><br />Recover (all deployment scenarios):  Mailbox, mailbox databases under a DAG|
|Exchange|Exchange 2007|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios):  Storage group<br /><br />Recover (all deployment scenarios):  Storage group, database, mailbox|
|Exchange|Exchange 2007|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios):  Storage group<br /><br />Recover (all deployment scenarios):  Storage group, database, mailbox|
|SharePoint|SharePoint 2016|Physical server and virtual machine deployment|N|N|No scenarios are supported.|
|SharePoint|SharePoint 2013|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />Note that protecting a SharePoint farm that's using the SQL Server 2012 AlwaysOn feature for the content databases isn't supported.|
|SharePoint|SharePoint 2013|Azure virtual machine (when workload is running as Azure virtual machine) - DPM 2012 R2 Update Rollup 3 onwards|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />Note that protecting a SharePoint farm that's using the SQL Server 2012 AlwaysOn feature for the content databases isn't supported.|
|SharePoint|SharePoint 2013|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server<br /><br />Note that protecting a SharePoint farm that's using the SQL Server 2012 AlwaysOn feature for the content databases isn't supported.|
|SharePoint|SharePoint 2010|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2010|Azure virtual machine (when workload is running as Azure virtual machine)|Y|Y (from DPM 2012 R2 with Update Rollup 3 onwards)|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2010|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios): Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios): Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2007|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server|
|SharePoint|SharePoint 2007|Windows virtual machine in VMWare (protects workloads running in Windows virtual machine in VMWare)|Y|Y (from DPM 2012 R2 with Update Rollup 5 onwards)|Protect (all deployment scenarios):  Farm, SharePoint search, frontend web server content<br /><br />Recover (all deployment scenarios):  Farm, database, web application, file or list item, SharePoint search, frontend web server|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2016|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|N|Protect: Hyper-V computers, cluster shared volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2012 R2 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, cluster shared volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2012 - Datacenter and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, cluster shared volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2008 R2 SP1 - Enterprise and Standard|Physical server<br /><br />On-premises Hyper-V virtual machine|Y|Y|Protect: Hyper-V computers, cluster shared volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Hyper-V host - DPM protection agent on Hyper-V host server, cluster, or VM|Windows Server 2008|Physical server<br /><br />On-premises Hyper-V virtual machine|N|N|Protect: Hyper-V computers, cluster shared volumes (CSVs)<br /><br />Recover: Virtual machine, Item-level recovery of files and folder, volumes, virtual hard drives|
|Linux|Linux running as Hyper-V guest|On-premises Hyper-V virtual machine|Y|Y|Hyper-V must be running on Windows Server 2012 R2 or Windows Server 2016. Protect: Entire virtual machine<br /><br />Recover: Entire virtual machine|

## Cluster support
DPM can protect data in the following clustered applications:

-   File servers

-   SQL Server

-   Hyper-V - But if you're protecting a Hyper-V cluster using scaled-out DPM protection, you can't add secondary protection for the protected Hyper-V workloads.

    For Hyper-V running on Windows Server 2008 R2 make sure you have the updated described in KB [975354](https://support.microsoft.com/en-us/kb/975354) installed.
    For Hyper-V running on Windows Server 2008 R2 in a cluster configuration make sure you have SP2 and KB [971394](https://support.microsoft.com/en-us/kb/971394) installed.

-   Exchange Server - DPM can protect non-shared disk clusters for supported Exchange Server versions (cluster continuous replication), and can also protect Exchange Server configured for local continuous replication.

-   SQL Server - Note that DPM doesn't support the protection of SQL Server databases hosted on cluster-shared volumes (CSVs).

DPM can protect cluster workloads that are located in the same domain as the DPM server, and in a child or trusted domain. If you want to protect data source in untrusted domains or workgroups you'll need to use NTLM or certificate authentication for a single server, or certificate authentication only for a cluster.
