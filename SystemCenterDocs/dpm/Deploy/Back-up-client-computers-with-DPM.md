ere is insufficient space on the tape. You can also colocate data from different protection groups on tape.

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



