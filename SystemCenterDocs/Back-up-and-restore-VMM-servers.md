---
title: Back up and restore VMM servers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9ed546c-b12b-4a2c-9668-3dc23963114e
---
# Back up and restore VMM servers
DPM can back up the SQL Server instances that's being used as the System Center VMM database in a couple of ways:

-   You can do a regular SQL Server backup.

-   You can backup the SQL Server database using the VMM Express Writer component that appears under the VMM server in the DPM console.  The main advantage to this method is that you don't need to set up any special permissions on the SQL Server.

DPM can back up the VMM database using the  VMM Express Writer component when VMM  is running on System Center 2012 onwards as a physical\/virtual machine in the following deployment scenarios:

-   A standalone VMM host \+ standalone SQL Server \(default and named, local and remote\)

-   A standalone VMM host \+ clustered SQL Server \(default and named, remote\)

-   A clustered VMM host \+ standalone SQL Server \(default and named, local and remote\)

-   A clustered VMM host \+ clustered SQL Server \(default and named, remote\)

## Prerequisites and limitations
Before setting up a DPM backup for VMM using VMM Express Writer note the following:

-   DPM only backs up the DPM SQL Server database. It doesn't back up all configuration files in the VMM library.

-   DPM supports initial replication and express full backups for VMM machines. Incremental backup isn't supported.

-   DPM can't back up the VMM database if you specified a static IP address for the SQL Server when you set up VMM. DPM also can't back up if you specified "localhost" for the database.

-   If you're using Distributed Key Management \(DKM\) encryption \(key stored in AD\) then DPM won't back up the key. You'll need to protect that as part of your AD backup. If the key's stored locally it's backed up as part of the database.

-   In case of a failover, DPM will continue backing up when the VMM node comes back online. This allows you to perform scheduled failovers without losing protection. But if the node is lost, you have to configure backup for the new one.

-   DPM supports recovery to original location for VMM hosts. Recovery to an alternate location isn't supported.

## Before you start

-   Review the [release notes](http://technet.microsoft.com/en-us/library/jj860394.aspx) and read about any VMM backup issues in [What's supported and what isn't for DPM?](../Topic/What-s-supported-and-what-isn-t-for-DPM-.md)

-   Make sure that the VMM machines you want to back up  are in the DPM server domain, or in a domain with a two\-way trust relationship with the DPM domain.

-   **Set up storage**—You can store backed up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](../Topic/Prepare-data-storage.md).

-   You'll need to deploy the DPM  protection agent on the VMM server.  Learn more in [Deploy the DPM protection agent](../Topic/Deploy-the-DPM-protection-agent.md).

## Back up VMM

1.  Click **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2.  In **Select protection group** type click **Clients**. You only select clients if you want to back up data on a Windows computer running a Windows client operating system. For all other workloads select server. Learn more in [Deploy protection groups](../Topic/Deploy-protection-groups.md)

3.  In **Select Group Members** expand the VMM machine and select **VMM Express Writer**

4.  In **Select data protection method**  specify how you want to handle short and long\-term backup. Short\-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup \(for short or long\-term\). As an alternative to long\-term backup to the cloud you can also configure long\-term back up to a standalone tape device or tape library connected to the DPM server.

5.  In **Select short\-term goals** specify how you want to back up to short\-term storage on disk.   In Retention range you specify how long you want to keep the data on disk. In **Synchronization frequency** you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

6.  If you want to store data on tape for long\-term storage in **Specify long\-term goals** indicate how long you want to keep tape data \(1\-99 years\). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1–99 years, you can select backups to occur daily, weekly, bi\-weekly, monthly, quarterly, half\-yearly, or yearly.

    -   When the retention range is 1–11 months, you can select backups to occur daily, weekly, bi\-weekly, or monthly.

    -   When the retention range is 1–4 weeks, you can select backups to occur daily or weekly.

    On a stand\-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page specify the tape\/library to use, and whether data should be compressed and encrypted on tape.

7.  In **Review disk allocation** page review the storage pool disk space allocated for the protection group. **Data size** shows the size of the data you want to back up, and **Disk space** shows the space that DPM recommends for the protection group. Select **Automatically grow the volumes** to automatically increase size when more disk space is required for backing up data.

8.  In **Choose replica creation method** select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off\-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don’t want to configure automatic consistency checking, you can run a manual check at any time by right\-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

11. In **Specify online backup schedule** specify how often incremental backups to Azure should occur. You can schedule backups to run every day\/week\/month\/year and the time\/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

12. In **Specify online retention policy** you can specify how the recovery points created from the daily\/weekly\/monthly\/yearly backups are retained in Azure.

13. In **Choose online replication** specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup \(offline seeding\). Offline backup uses the Azure Import feature. [Read more](https://azure.microsoft.com/en-in/documentation/articles/backup-azure-backup-import-export/).

14. On the  **Summary** page review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

