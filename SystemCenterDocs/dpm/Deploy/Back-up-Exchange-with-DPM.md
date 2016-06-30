 recovery mailbox database. If you don't, create one using the New-MailboxDatabase cmdlet. Configure the recovery database so it can be overwritten by using the Set-MailboxDatabase cmdlet. For example:

    ```
    New-MailboxDatabase -Recovery -Name RDB-CONTROL -Server E2K13-MBX1
    ```

    ```
    Set-MailboxDatabase -Identity 'RDB-CONTROL' -AllowFileRestore $true
    ```

2.  In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protectd Exchange Data** node).

3.  Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, select a recovery point in **Recovery time** > **Recover**.

    Note that you won't be able to select **Latest**. This isn't available for individual mailboxes.

4.  In the Recovery Wizard review your recovery selection, and click **Next**.

5.  Specify the type of recovery you would like to perform and click **Next**.

6.  In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Clear the check box if you don't want to mount the databases.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

7.  On the **Summary** page review your recovery settings, and click **Recover**. When the recovery finishes click **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

8.  After the recovery process has finished, the required mailbox is not quite fully restored. The mailbox database to which the mailbox belongs is only restored to the Recovery mailbox database. Restore the mailbox by running this cmdlet:

    ```
    New-MailboxRestoreRequest -SourceDatabase 'RDB-CONTROL' -SourceStoreMailbox 'mailbox name' -TargetMailbox <name>@contoso.com -TargetRootFolder Recovery -SkipMerging StorageProviderForSource
    ```

    You must add `\-SkipMerging StorageProviderForSource` to the command; otherwise an error occurs. For a workaround, see Release Notes for Exchange 2013.

    When you now open the `<mailbox name>` mailbox, all its contents until 3:15 PM are located beneath the Recovery folder.

9. After you finished the restore, you can dismount and delete the Recovery Mailbox database by running the following Windows PowerShell cmdlet.

    ```
    Remove-MailboxDatabase -Identity 'RDB-CONTROL'
    ```

### <a name="BKMK_DB"></a>Recover an Exchange database

-   In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

-   Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, and select **Latest** to get the newest backup and click **Recover**.

-   In the Recovery Wizard review your recovery selection, and click **Next**.

-   Specify the type of recovery you would like to perform and click **Next**.

-   In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Select this.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

-   You must now return to the Exchange server in order to enable the databases to be overwritten by the restore. If you miss this step, the restore fails. To do this, open the Exchange admin center, navigate to  **Servers**> **Databases**, select the Exchange mailbox database that you want to be overwritten, and then click **Edit**.

    Click **Maintenance** > **This database can be overwritten by a restore** > **Save**.

-   Back in the Recovery Wizard on the **Summary** page review your recovery settings, and click **Recover**. When the recovery finishes click **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

-   Check your mailbox contents to verify the success of your restore operation. If the recovered mailbox database was part of a Database Availability Group (DAG), the passive copy shows the failed and suspended status.

-   To resume normal DAG operations, select the failed database copy, and then click **Resume**. A dialog box appears prompting you to reseed (or reset) the database. Click **Yes**.

### <a name="BKMK_Server"></a>Recover an entire Exchange server

-   In the DPM Administrator Console, go to the **Recovery** view and navigate to the server you want to recover.

-   Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, and select a recovery point from the list. In the list, right-click **Bare Metal Recovery** (BMR) and click **Recover**.

-   In the Recovery Wizard review your recovery selection, and click **Next**.

-   In the **Select Recovery Type** page, select **Copy to a network folder** to restore the server to a separate network location. Or you can select **Copy to tape** if you have one available.

-   In the **Specify Destination** page, select where you want to copy the database files. These files can be used to perform the BMR.

-   In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Select this.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

-   You can monitor the process on the **Monitoring** tab. A 'recovery success' alert shows when recovery finishes.

    Open the folder where are located recovery files and rename it with a shorter name. This will make the recovery process easier. Create a share in the recovery folder.

-   To run the bare metal recovery, insert the ISO of your operating system for boot purposes. Select the **Repair** option and in **Advanced Options**, select **System Image Recovery**.

    In the **Re-image your computer** wizard, you can ignore any warning about a system image not found.

-   In the **Select a system image backup** page, click **Select a system image**. Click **Advanced** to select recovery files from a network share. Select **Search for a system image on the network**and click **Yes**if asked if you're sure you want to connect to the network.

-   Specify the network folder, select the backup, and select the date and time of the image you want to restore. Specify any additional driver and disk settings, and then click **Finish**to start the restore.



