---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-30
title:  Back up client computers with DPM
ms.technology:  data-protection-manager
ms.assetid:  0e12f557-0396-465d-b60f-7695b44bbd12
---

# Back up client computers with DPM

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

You can deploy DPM to back up client computers.   Depending on the client operating system you can back up volumes, shares, folders, files, bare metal and system state, and deduped volumes.

## Prerequisites and limitations
.Before you deploy DPM to protect client computer data verify the deployment prerequisites:

-   Read about the client operating systems you can support in [What can DPM back up?](../get-started/What-can-DPM-back-up-.md)

-   Review the [release notes](http://technet.microsoft.com/en-us/library/jj860394.aspx) and read about any client protection issues in [What's supported and what isn't for DPM?](../get-started/What-s-supported-and-what-isn-t-for-DPM-.md)

-   Make sure that client machines you want to back up  are in the DPM server domain, or in a domain with a two-way trust relationship with the DPM domain.

-   To set up client machines for protection you install the DPM protection agent on them. If Windows Firewall is configured on the client computer, the agent installation will set up the firewall exceptions it needs. If you need to reset the firewall, you can reconfigure it by running SetDpmServer.exe.  If you are using a firewall other than Windows Firewall, you'll need to open the necessary ports. Learn more in [Deploy the DPM protection agent](Deploy-the-DPM-protection-agent.md).

-   DPM  can back up client computers that are physically or wirelessly connected to the local area network (LAN)or back up over VPN. For VPN backup the ICMP should be enabled on the client computer.

-   Each DPM server can protect up to 3000 client computers

-   You can tweak the performance of client data backup as follows:

    -   If client data backup is slow you can set this key to a lower value:  HKLM\Software\Microsoft\Microsoft Data Protection Manager\Agent\ClientProtection\WaitInMSPerRequestForClientRead to a lower value.

    -   To scale up client performance you can tweak these registry keys:

        -   Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: 9037ebb9-5c1b-4ab8-a446-052b13485f57

        -   Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: 3d859d8c-d0bb-4142-8696-c0d215203e0d

        -   Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: c4cae2f7-f068-4a37-914e-9f02991868da

        -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Collocation\Client. Value: DSCollocationFactor

## Before you start

1.  **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't see:

    -   System requirements for DPM

    -   [What can DPM back up?](../get-started/What-can-DPM-back-up-.md)

    -   [What's supported and what isn't for DPM?](../get-started/What-s-supported-and-what-isn-t-for-DPM-.md)

    -   [Get DPM installed](../get-started/Get-DPM-installed.md)

2.  **Set up storage** - You can store backed up data on disk, on tape, and in the cloud with Azure.
      Read more in [Prepare data storage](../get-started/Prepare-data-storage.md).

3.  **Set up the DPM protection agent** - The agent needs to be installed on client computers you want to protect.  Read [Deploy the DPM protection agent](Deploy-the-DPM-protection-agent.md).

## Back up client computers

1.  Click **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2.  In **Select protection group** type click **Clients**. You only select clients if you want to back up data on a Windows computer running a Windows client operating system. For all other workloads select server. Learn more in [Deploy protection groups](Deploy-protection-groups.md)

3.  In **Select Group Members** click **Add Multiple Computers**. You can add the client computers you want to back up in a text file. In the file  you'll need to enter each computer on a new line. We recommend that you provide the FQDN target computers. For example, enter multiple computers in a .txt file as follows:

    -   Comp1.abc.domain.com

    -   Comp2.abc.domain.com

    -   Comp3.abc.domain.com

    Note that if DPM can't find the text file or any of the computers it will add them to the log file. Click **Failed to add machines**to open the log file. To add new client computers to an existing protection group you right-click the group name and select **Add client computers**.

    -   On the **Specify Inclusions and Exclusions** page, specify the folders to include or exclude for protection on the selected computers. To select from a list of well-known folders, such as **Documents**, click the drop-down list. Note that:

        -   When you exclude a folder, and then specify a separate inclusion rule for a subfolder, DPM doesn't back up the subfolder. The exclusion rule overrides the inclusion rule.

        -   When you include a folder, and then specify a separate exclude rule for a subfolder, DPM backs up the entire folder, except for the excluded subfolder.

        -   When you include a well-known folder such as **Documents**, DPM locates the **Documents** folder for all users on the computer, and then applies the rule. For example, if the user profile for computer **Comp1** contains the **Documents** folder for both User1 and User2, DPM will back up both folders.

        -   In the **Folder** column you type the folder names using variables such as *programfiles*, or you can use the exact folder name. Select **Include** or **Exclude** for each entry in the **Rule** column.

        -   You can select **Allow users to specify protection members** to give your end users the choice to add more folders on the computer that they want to back up. However, the files and folders you have explicitly excluded as an administrator cannot be selected by the end user.

        -   Under **File type exclusions** you can specify the file types to exclude using their file extensions.

4.  In **Select data protection method**  specify how you want to handle short and long-term backup. Short-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short or long-term). As an alternative to long-term backup to the cloud you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5.  In **Select short-term goals** specify how you want to back up to short-term storage on disk.   In Retention range you specify how long you want to keep the data on disk. In **Synchronization frequency** you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

6.  If you want to store data on tape for long-term storage in **Specify long-term goals** indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page specify the tape/library to use, and whether data should be compressed and encrypted on tape.

7.  In **Review disk allocation** page review the storage pool disk space allocated for the protection group. **Data size** shows the size of the data you want to back up, and **Disk space** shows the space that DPM recommends for the protection group. We recommend that you select **Colocate data** to back up multiple client data sources to one replica volume if you have a large number of client computers. You won't be able to protect 1000 or more client computers with one DPM server without co-locating your data. We recommend that you do not co-locate if you have less than ten client computers in a protection group. Select **Automatically grow the volumes** to automatically increase size when more disk space is required for protecting data on the client computers.

8.  In **Choose replica creation method** select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

11. In **Specify online backup schedule** specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

12. In **Specify online retention policy** you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

13. In **Choose online replication** specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](https://azure.microsoft.com/en-in/documentation/articles/backup-azure-backup-import-export/).

14. On the  **Summary** page review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Recover client data
You can recover client computer data using the Recovery Wizard. You can also set up end-user recovery so that  users can recover their own data.

### Allow clients to recover their own data
End-user recovery enables users to independently recover file data by retrieving recovery points of their files. Note that:

-   Users can only recover data stored on disk.

-   You'll need to modify the Active Directory schema to enable end-user recovery. DPM extends the schema, creates a container (MS-ShareMapConfiguration), grants the DPM server permissions to change the container contents, and adds mappings between source and replica shares. [View](https://technet.microsoft.com/en-us/library/hh758112.aspx) a detailed list of classes and attributes added to AD by DPM.

-   If you enable end-user recovery you can't specify on which file servers end-user recovery is enabled.

-   You can't control which Active Directory users or groups can perform end-user recovery.

To configure end-user recovery here's what you'll need to do:

1.  Configure Active Directory to support end-user recovery:

    1.  In the DPM console click **Options** > **End-user Recovery** > **Configure Active Directory**.

    2.  In  **Configure Active Directory** select **Use current credentials** or type in a user name and password with schema and domain admin permissions. Confirm your settings.

    3.  If you don't have an account that has schedule and domain admin permissions you can ask another user with those permissions to run <drive:>\Program Files\Microsoft Data Protection Manager\DPM\End User Recovery\DPMADSchemaExtension.exe on a computer in the same domain as the DPM server.   When the app runs the user should specify the name of the computer on which you want to enable end-user recovery and the DNS domain name of the DPM server.

        Note that if the protected computer and DPM reside in different domains, the schema needs to be extended by running the DPMADSchemaExtension.exe tool on the other domain.

2.  After AD settings are complete in the **End-user Recovery** tab click **Enable end-user recovery**.

### Recover data
Recover data from the DPM console as follows:

1.  In DPM console  click **Recovery** on the navigation bar. and browse for the data you want to recover. In the results pane, select the data.

2.  Available recovery points are indicated in bold on the calendar in the recovery points section. Select the bold date for the recovery point you want to recover.

3.  In the **Recoverable item** pane, click to select the recoverable item you want to recover.

4.  In the **Actions** pane, click **Recover**. DPM starts the Recovery Wizard.

5.  You can recover data as follows:

    1.  **Recover to the original location**. Note that this doesn't work if the client computer is connected over VPN. In this case use an alternate location and then copy data from that location.

    2.  **Recover to an alternate location**.

    3.  **Copy to tape**. This option copies the volume that contains the selected data to a tape in a DPM library. You can also choose to compress or encrypt the data on tape.

6.  Specify your recovery options:

    1.  **Existing version recovery behavior**. Select **Create copy**, **Skip**, or **Overwrite**. This option is enabled only when you're recovering to the original location.

    2.  **Restore security**. Select **Apply settings of the destination computer** or **Apply the security settings of the recovery point version**.

    3.  **Network bandwidth usage throttling**. Click **Modify** to enable network bandwidth usage throttling.

    4.  **Enable SAN based recovery using hardware snapshots**. Select this option to use SAN-based hardware snapshots for quicker recovery.

        This option is valid only when you have a SAN where hardware snapshot functionality is enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    5.  **Notification**. Click **Send an e-mail when the recovery completes**, and specify the recipients who will receive the notification. Separate the e-mail addresses with commas.

7.  Click **Next** after you have made your selections for the preceding options.

8.  Review your recovery settings, and click **Recover**. Note that any synchronization job for the selected recovery item will be canceled while the recovery is in progress.

End users should recover data as follows:

1.  Navigate to the protected data file. Right-click the file name > **Properties**.

2.  In **Properties** > **Previous Versions** select the version that you want to recover from.
