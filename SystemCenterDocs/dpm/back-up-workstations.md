---
description: You can use DPM to back up client computers.
ms.topic: how-to
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Back up client computers with DPM
ms.subservice: data-protection-manager
ms.assetid: 0e12f557-0396-465d-b60f-7695b44bbd12
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Back up client computers with DPM

You can deploy System Center Data Protection Manager (DPM) to back up client computers. Depending on the client operating system, you can back up volumes, shares, folders, files, and deduped volumes.

## Prerequisites and limitations

Before you deploy DPM to protect client computer data, verify the deployment prerequisites:

- Read about the client operating systems you can support in [What can DPM back up?](dpm-protection-matrix.md)

- Review the [release notes](dpm-release-notes.md) and read about any client protection issues in [What's supported and what isn't for DPM?](dpm-support-issues.md)

- Ensure that the client machines you want to back up are in the DPM server domain or in a domain with a two-way trust relationship with the DPM domain.

- To set up client machines for protection, install the DPM protection agent on them. If Windows Firewall is configured on the client computer, the agent installation will set up the firewall exceptions it needs. If you need to reset the firewall, you can reconfigure it by running SetDpmServer.exe. If you're using a firewall other than Windows Firewall, you'll need to open the necessary ports. Learn more in [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

- DPM can back up client computers that are physically or wirelessly connected to the local area network (LAN) or back up over VPN. For VPN backup, the ICMP should be enabled on the client computer.

- Each DPM server can protect up to 3000 client computers. When protecting client computers at scale, we recommend you create multiple protection groups and stagger the recovery point times for those protection groups. The more the number of clients that belong to a protection group, the longer it takes to enumerate the changes to the protection group.

- You can tweak the performance of client data backup as follows:

    - If client data backup is slow, you can set this key to a lower value:  `HKLM\Software\Microsoft\Microsoft Data Protection Manager\Agent\ClientProtection\WaitInMSPerRequestForClientRead to a lower value`.

    - To scale up client performance, you can tweak these registry keys:

        - `Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: 9037ebb9-5c1b-4ab8-a446-052b13485f57`

        - `Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: 3d859d8c-d0bb-4142-8696-c0d215203e0d`

        - `Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold. Value: c4cae2f7-f068-4a37-914e-9f02991868da`

        - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Collocation\Client. Value: DSCollocationFactor`

## Before you start

1. **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't, see:

    - System requirements for DPM

    - [What can DPM back up?](dpm-protection-matrix.md)

    - [What's supported and what isn't for DPM?](dpm-support-issues.md)

    - [Get DPM installed](install-dpm.md)

2. **Set up storage** - You can store backed-up data on disk, on tape, and in the cloud with Azure.
      Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3. **Set up the DPM protection agent** - The agent needs to be installed on client computers you want to protect. Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

## Well known folders to back up on client computers

If you're looking to back up certain common folders in your client machines, you can select these folders from the *Well Known Folder* list in DPM, and DPM will take backup of these folders on your client computers in subsequent backup cycles. Below is the list of the well known folders that you can back up with DPM:

| **Well Known Folder**    | **Location to all or every user on the client machine**                                  |
|--------------------------|------------------------------------------------------------------------------------------|
| AppData                  | C:\Users\USERNAME\AppData\Roaming                                                   |
| User Profiles            | C:\Users\USERNAME OR %SystemDrive%\Users                                              |
| Slide Shows              | C:\Users\USERNAME\Pictures                                                            |
| Quick Launch             | C:\Users\USERNAME\AppData\Roaming\Microsoft\Internet Explorer\Quick Launch        |
| Startup                  | C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup |
| Start Menu               | C:\ProgramData\Microsoft\Windows\Start Menu                                          |
| My Video                 | C:\Users\USERNAME\Videos                                                              |
| My Pictures              | C:\Users\USERNAME\Pictures                                                            |
| My Music                 | C:\Users\USERNAME\Music                                                               |
| My Documents             | C:\Users\USERNAME\Documents                                                           |
| Links                    | C:\Users\USERNAME\Links                                                               |
| Favorites                | C:\Users\USERNAME\Favorites                                                           |
| Downloads                | C:\Users\USERNAME\Downloads                                                           |
| Desktop                  | C:\Users\USERNAME\Desktop                                                             |
| Temporary Internet Files | C:\Users\USERNAME\AppData\Local\Microsoft\Windows\Inetcache                       |
| Program Files            | C:\Program Files                                                                        |
| System Drive             | C:\                                                                                     |

>[!NOTE]
>To backup *Links*, *Downloads*, *Slides Shows*, and *Quick Launch*, you need to add to the registry location
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders for every user.

The details of the registry entry are below. Modify the value USERNAME according to your username of the client computer.

- reg add `"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"/v Links /t REG_SZ /d C:\Users\USERNAME\Links`

- reg add `"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"/v Downloads /t REG_SZ /d C:\Users\USERNAME\Downloads`

- reg add `"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"/v “Slides Shows” /t REG_SZ /d C:\Users\USERNAME\Pictures`

- reg add `"HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"/v “Quick Launch” /t REG_SZ /d “C:\Users\USERNAME\AppData\Roaming\Microsoft\Internet Explorer\QuickLaunch”`

>[!NOTE]
>While creating a protection group of your client or workstation machine, DPM honors the folder hierarchy during backup. As an example, if you select backup of *User Profiles*, which represents the parent of *Desktop* folder, the *Desktop* folder will be included in backup.

## Back up client computers

1. Select **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2. In **Select protection group** type, select **Clients**. You only select clients if you want to back up data on a Windows computer running a Windows client operating system. For all other workloads, select server. Learn more in [Deploy protection groups](create-dpm-protection-groups.md)

3. In **Select Group Members**, select **Add Multiple Computers**. You can add the client computers you want to back up in a text file. In the file, you'll need to enter each computer on a new line. We recommend that you provide the FQDN target computers. For example, enter multiple computers in a .txt file as follows:

    - Comp1.abc.domain.com

    - Comp2.abc.domain.com

    - Comp3.abc.domain.com

    If DPM can't find the text file or any of the computers, it will add them to the log file. Select **Failed to add machines** to open the log file. To add new client computers to an existing protection group, right-click the group name and select **Add client computers**.

    - On the **Specify Inclusions and Exclusions** page, specify the folders to include or exclude for protection on the selected computers. To select from a list of well-known folders, such as **Documents**, select the dropdown list.

    >[!NOTE]
    >- When you exclude a folder and then specify a separate inclusion rule for a subfolder, DPM doesn't back up the subfolder. The exclusion rule overrides the inclusion rule.
    >- When you include a folder and then specify a separate exclude rule for a subfolder, DPM backs up the entire folder, except for the excluded subfolder.
    >- When you include a well-known folder such as **Documents**, DPM locates the **Documents** folder for all users on the computer and then applies the rule. For example, if the user profile for computer **Comp1** contains the **Documents** folder for both User1 and User2, DPM will back up both folders.
    >- In the **Folder** column, enter the folder names using variables such as *program files* or you can use the exact folder name. Select **Include** or **Exclude** for each entry in the **Rule** column.
    >- You can select **Allow users to specify protection members** to give your end users the choice to add more folders on the computer that they want to back up. However, the files and folders you have explicitly excluded as an administrator cannot be selected by the end user.
    >- Under **File type exclusions**, you can specify the file types to exclude using their file extensions.

4. In **Select data protection method**, specify how you want to handle short- and long-term backup. Short-term backup is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short- or long-term). As an alternative to long-term backup to the cloud, you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5. In **Select short-term goals**, specify how you want to back up to short-term storage on disk. In Retention range, specify how long you want to keep the data on disk. In **Synchronization frequency**, specify how often you want to run an incremental backup to disk. If you don't want to set a backup interval, you can check just before a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

6. If you want to store data on tape for long-term storage in **Specify long-term goals**, indicate how long you want to keep tape data (1-99 years). In Frequency of backup, specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    - When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    - When the retention range is 1-11 months, you can select backups to occur daily, weekly, biweekly, or monthly.

    - When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a standalone tape drive, for a single protection group, DPM uses the same tape for daily backups until there's insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page, specify the tape/library to use and whether data should be compressed and encrypted on tape.

7. In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume to continue with backups smoothly in the future.

8. In **Choose replica creation method**, select how you want to handle the initial full data replication. If you select to replicate over the network, we recommend you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page, ensure to select the workloads that you want to back up to Azure.

11. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

::: moniker range=">=sc-dpm-2019"

>[!Note]
>Online backups have a dependency on new local disk based backup prior to running. Ensure the Online protection schedule is compatible with the Express backup time and frequency.

::: moniker-end

12. In **Specify online retention policy**, specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

13. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).

14. On the **Summary** page, review your settings. After you select **Create Group**, initial replication of the data occurs. When it finishes, the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Recover client data

You can recover the client data using any one of the following methods:

- Allow clients to recover their own data by setting up user recovery
- Recover client’s computer data using Recovery Wizard on the DPM Server

Select the required tab for steps to allow **clients to recover their own data** or **recover data for clients** using the DPM Recovery Wizard:

::: moniker range="sc-dpm-2016"

# [Allow clients to recover their data](#tab/AllowClients2016)

End user recovery enables users to independently recover file data by retrieving recovery points of their files.

>[!NOTE]
>- Users can only recover data stored on disk.
>- You'll need to modify the Active Directory schema to enable end user recovery. DPM extends the schema, creates a container (MS-ShareMapConfiguration), grants the DPM server permissions to change the container contents, and adds mappings between source and replica shares. [View](/previous-versions/system-center/system-center-2012-R2/hh758112(v=sc.12)) a detailed list of classes and attributes added to AD by DPM.
>- If you enable end user recovery, you can't specify on which file servers end user recovery is enabled.
>- You can't control which Active Directory users or groups can perform end user recovery.

**Configure end user recovery, here's what you'll need to do:**

1. Configure Active Directory to support end user recovery:

    1. In the DPM console, select **Options** > **End-user Recovery** > **Configure Active Directory**.

    2. In **Configure Active Directory**, select **Use current credentials** or type in a username and password with schema and domain admin permissions. Confirm your settings.

    3. If you don't have an account that has schedule and domain admin permissions, you can ask another user with those permissions to run &lt;drive:&gt;\Program Files\Microsoft Data Protection Manager\DPM\End User Recovery\DPMADSchemaExtension.exe on a computer in the same domain as the DPM server. When the app runs, the user should specify the name of the computer on which you want to enable end user recovery and the DNS domain name of the DPM server.

        > [!NOTE]
        > If the protected computer and DPM reside in different domains, the schema needs to be extended by running the DPMADSchemaExtension.exe tool on the other domain.

2. After AD settings are complete in the **End-user Recovery** tab, select **Enable end-user recovery**.

# [Recover data for clients](#tab/RecoverData2016)

**Recover data from the DPM console as follows:**

1. In the DPM console, select **Recovery** on the navigation bar and browse for the data you want to recover. In the results pane, select the data.

2. The available recovery points are indicated in bold on the calendar in the recovery points section. Select the bold date for the recovery point you want to recover.

3. In the **Recoverable item** pane, select the recoverable item you want to recover.

4. In the **Actions** pane, select **Recover**. DPM starts the Recovery Wizard.

5. You can recover data as follows:

    1. **Recover to the original location**. This doesn't work if the client computer is connected over VPN. In this case, use an alternate location and then copy data from that location.

    2. **Recover to an alternate location**.

    3. **Copy to tape**. This option copies the volume that contains the selected data to a tape in a DPM library. You can also choose to compress or encrypt the data on tape.

6. Specify your recovery options:

    1. **Existing version recovery behavior**. Select **Create copy**, **Skip**, or **Overwrite**. This option is enabled only when you're recovering to the original location.

    2. **Restore security**. Select **Apply settings of the destination computer** or **Apply the security settings of the recovery point version**.

    3. **Network bandwidth usage throttling**. Select **Modify** to enable network bandwidth usage throttling.

    4. **Enable SAN based recovery using hardware snapshots**. Select this option to use SAN-based hardware snapshots for quicker recovery.

        This option is valid only when you have a SAN where hardware snapshot functionality is enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    5. **Notification**. Select **Send an e-mail when the recovery completes**, and specify the recipients who will receive the notification. Separate the email addresses with commas.

7. Select **Next** after you've made your selections for the preceding options.

8. Review your recovery settings, and select **Recover**. Any synchronization job for the selected recovery item will be canceled while the recovery is in progress.

**End users should recover data as follows:**

1. Navigate to the protected data file. Right-click the file name > **Properties**.

2. In **Properties** > **Previous Versions**, select the version that you want to recover from.

---

::: moniker-end

::: moniker range=">=sc-dpm-2019"

# [Allow clients to recover their data](#tab/AllowClients)

>[!Note]
>By default, DPM allows only the local administrator to perform user recoveries on the computer. The user account must be explicitly named as a local administrator on the client. It can't be a local administrator through group membership.

For more information, see [**Enable non-administrators to recover files**](#enable-non-administrators-to-recover-files).

>[!Note]
>DPM Client UI tool supports Windows Communication Foundation (WCF) that uses TCP port 6075 on the DPM server for communication while performing recoveries. On the DPM server, DPM automatically configures firewall rules starting with DPMAM_WFC_ to allow this traffic.

DPM enables you to recover files and folders from backups stored on the DPM server that are managed by the backup administrator. To recover your data, you must know the name of the DPM server on which the data was backed up. To know the name of the DPM server, contact your backup administrator.

To recover data from backups stored on the DPM server, follow these steps:

1. Select **Start** > **All Apps** and then select **Microsoft System Center DPM Client**.
     Alternately, you can select the DPM Client icon ![An icon that signifies DPM client.](media/back-up-workstations/icon-data-protection-manager-client.png) in the system tray.

2. In the **Data Protection Manager Client** page, select **Recovery** tab.

3. The FQDN of the DPM Server is auto-populated in the **Search for recovery points on:** field. If not, enter the name of DPM server on which the data was backed up.

     >[!Note]
     >To know the name of the DPM server, contact your backup administrator.

4. Select the **Search** icon to start the search for the existing recovery points on the DPM server. This lists the computers to which the user has permission.
     - Select **+** next to the computer you want to recover data to displays all the recovery points in the display pane.
     - In the display pane, the **Time** column lists the time stamps for each recovery point and the **Link** column has an **Open…** link that points to the backup folder location on the DPM server for each available recovery point listed.

5. Select **Open…** for the date and time of the recovery point to mount and access the recovery point data. Navigate to the file or folder you want to restore. Then, right-click and **copy** the data to be recovered and **paste** the data in the desired location.

## Enable non-administrators to recover files

The administrator of a client computer must authorize the username of non-admin users who need permissions to perform end-user recovery of protected data on a protected client computer.

To do this, the administrator must add the following registry key and value for each of these non-admin users. This is single value that contains a comma-separated list of client users.

**Key**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Agent\ClientProtection` <br>
**Value**: ClientOwners<br>
**Type**: String<br>
**Data**: Names of non-admin users. This must be a comma-separated list of user names without any leading or trailing spaces.<br>
          For example: *Domain\User1,Domain\User2,Domain\User3 (and so on)*

To configure DPM recovery permissions for users who are not members of the local administrators group, follow these steps:

1. Sign in to the DPM protected client computer with a user account that is a member of the local administrators group.

2. Open the registry editor and navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Agent\ClientProtection`.

3. Right-click **ClientProtection** key and select new **String Value** and name the new value as **ClientOwners**.

     - Double-click the **ClientOwner** to add a single user using the Domain\User format or add multiple users separated by a comma. Ensure not to use any leading or trailing spaces in the list.

     >[!Note]
     > Non-Admin users added to the registry have access only to the recovery points created after the user was added. Recovery points that were created earlier are accessible by Administrators only.

# [Recover data for clients](#tab/RecoverData)

**Recover data from the DPM console as follows:**

1. In the DPM console, select **Recovery** on the navigation bar and browse for the data you want to recover. In the results pane, select the data.

2. The available recovery points are indicated in bold on the calendar in the recovery points section. Select the bold date for the recovery point you want to recover.

3. In the **Recoverable item** pane, select the recoverable item you want to recover.

4. In the **Actions** pane, select **Recover**. DPM starts the Recovery Wizard.

5. You can recover data as follows:

    1. **Recover to the original location**. This doesn't work if the client computer is connected over VPN. In this case, use an alternate location and then copy data from that location.

    2. **Recover to an alternate location**.

    3. **Copy to tape**. This option copies the volume that contains the selected data to a tape in a DPM library. You can also choose to compress or encrypt the data on tape.

6. Specify your recovery options:

    1. **Existing version recovery behavior**. Select **Create copy**, **Skip**, or **Overwrite**. This option is enabled only when you're recovering to the original location.

    2. **Restore security**. Select **Apply settings of the destination computer** or **Apply the security settings of the recovery point version**.

    3. **Network bandwidth usage throttling**. Select **Modify** to enable network bandwidth usage throttling.

    4. **Enable SAN based recovery using hardware snapshots**. Select this option to use SAN-based hardware snapshots for quicker recovery.

        This option is valid only when you have a SAN where hardware snapshot functionality is enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    5. **Notification**. Select **Send an e-mail when the recovery completes**, and specify the recipients who will receive the notification. Separate the email addresses with commas.

7. Select **Next** after you've made your selections for the preceding options.

8. Review your recovery settings, and select **Recover**. Any synchronization job for the selected recovery item will be canceled while the recovery is in progress.

**End users should recover data as follows:**

1. Navigate to the protected data file. Right-click the file name > **Properties**.

2. In **Properties** > **Previous Versions**, select the version that you want to recover from.

---

::: moniker-end
