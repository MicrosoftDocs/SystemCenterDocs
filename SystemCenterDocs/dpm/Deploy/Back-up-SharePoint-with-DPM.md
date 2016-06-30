al backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

7.  If you want to store data on tape for long-term storage in **Specify long-term goals** indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page specify the tape/library to use, and whether data should be compressed and encrypted on tape.

8.  In **Review disk allocation** page review the storage pool disk space allocated for the protection group. **Data size** shows the size of the data you want to back up, and **Disk space** shows the space that DPM recommends for the protection group. We recommend that you select **Colocate data** to back up multiple client data sources to one replica volume if you have a large number of client computers. You won't be able to protect 1000 or more client computers with one DPM server without co-locating your data. We recommend that you do not co-locate if you have less than ten client computers in a protection group. Select **Automatically grow the volumes** to automatically increase size when more disk space is required for protecting data on the client computers.

9. In **Choose replica creation method** select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

10. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

11. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

12. In **Specify online backup schedule** specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

13. In **Specify online retention policy** you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

14. In **Choose online replication** specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](https://azure.microsoft.com/en-in/documentation/articles/backup-azure-backup-import-export/).

15. On the  **Summary** page review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring
After the protection group's been created the initial replication occurs and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups.  You can monitor the SharePoint data in a couple of ways:

-   Using default DPM monitoring can set up notifications for proactive monitoring. by publishing alerts and configuring notifications. You can send notifications by e-mail for critical, warning, or informational alerts, and for the status of instantiated recoveries.

-   If you use Operations Manager you can centrally publish alerts.

### Set up monitoring notifications

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  Click **SMTP Server**, type the server name, port, and email address from which notifications will be sent. The address must be valid.

3.  In **Authenticated SMTP server** , type a user name and password. The user name and password must be the domain account name of the person whose "From" address is described in the previous step; otherwise, notification delivery fails.

4.  To test the SMTP server settings, click **Send Test E-mail**, type the e-mail address where you want DPM to send the test message, and then click **OK**. Click **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients** type the e-mail address for each recipient to whom you want DPM to send copies of the notifications.

### Publish Operations Manager alerts

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options** > **Alert Publishing** > **Publish Active Alerts**

2.  After you enable **Alert Publishing** all existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Restore SharePoint data
You can recover SharePoint data as follows:

-   Recover to the original location

-   Recover to an alternate location. Note that you can't perform a full farm recovery to a new location.

-   Copy the data to a network folder

-   Copy the data to tape

Note that to recover a farm:

-   If you protected a SharePoint server as a SQL Server database, you can recover SharePoint data by selecting the SQL Server database in the Recovery Wizard.

-   Note the following to recover a farm:

    -   The front-end Web servers should be configured the same as they were when the recovery point was created.

    -   The farm structure must be created on the front-end Web server; the farm data will be recovered to the existing structure.

    -   The instances of SQL Server are configured with the same names as when the recovery point was created.

    -   The instances of SQL Server are configured with the same drive configuration as when the recovery point was created.

    -   The recovery farm must have all service packs, language packs, and patches installed on the primary farm.

    -   Don't directly try to recover the Central Administration content database or the configuration database because this could cause data corruption in the SharePoint farm.

    -   The recovery point time for SharePoint data displayed on the **Browse** tab may differ from the time displayed on the **Search** tab. The **Browse** tab displays the backup time for the farm, while the **Search** tab lists the correct recovery point time for sites, documents, and folders.

There a couple of possible scenarios for farm recovery:

-   A farm configuration exists as it did at the time of taking the backup. In this case, you will be restoring to a functioning farm.

-   The configuration database is corrupt and the servers in the farm are down.

#### Restore data to a functioning farm

1.  In DPM Administrator Console, click **Recovery** on the navigation bar.

2.  In the **Protected data** pane, expand the server that contains the farm you want to recover, and then click **All Protected SharePoint Data**.The farm displays in the **Recoverable** item pane as server name\farm name.

3.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

4.  On the **Recovery time** menu, select the recovery point you want to use.

5.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

6.  On the **Review recovery selection** page, click **Next**.

7.  Select where you want to recover the database. Note that:

    -   You can't recover an entire farm to an alternate location.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices. For the tape option you'll select the tape library you want to use for recovery.

8.  Specify recovery options for network bandwidth usage throttling, SAN-based recovery, and e-mail notifications, and then click **Next**.

9. On the **Summary** page, review the recovery settings, and then click **Recover**.

#### Restore data to a non-functioning farm

1.  Create a new farm that uses the same instance of SQL Server and the same front-end Web server as the original protected farm.

2.  On the front-end Web server that DPM uses to recover farm data, run the following command at the command prompt:`ConfigureSharePoint-EnableSharePointProtection`

3.  In the DPM Administrator Console, click **Recovery** on the navigation bar.

4.  In the **Protected data** pane, expand the server that contains the farm you want to recover, and then click **All Protected SharePoint Data**.The farm displays in the **Recoverable** item pane as server name\farm name.

5.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

6.  On the **Recovery time** menu, select the recovery point you want to use.

7.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

8.  On the **Review recovery selection** page, click **Next**.

9. Select where you want to recover the database. Note that:

    -   You can't recover an entire farm to an alternate location.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices. For the tape option you'll select the tape library you want to use for recovery.

10. Specify recovery options for network bandwidth usage throttling, SAN-based recovery, and e-mail notifications, and then click **Next**.

11. On the **Summary** page, review the recovery settings, and then click **Recover**.

12. On the main front-end Web server for the server farm, run the SharePoint Products and Technologies Configuration Wizard and disconnect the front-end Web server from the farm.



