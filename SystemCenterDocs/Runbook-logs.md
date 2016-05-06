---
title: Runbook logs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a001d77-2578-4e4d-b000-1b278c43117c
---
# Runbook logs
Every runbook generates a log when it is running. The Runbook Designer enables you to view both real\-time log information and historic logs.

## <a name="RealTimeLog"></a>Real\-Time Log
You can view the real\-time log of a runbook on the **Log** tab in the **Log** pane of the Runbook Designer. The log has an entry for each running instance of the runbook and the time that it was started. If you expand this entry, you can view the activity that is currently running. Double\-click the activity to view its details. If you have configured logging for the workbook to include Published Data, this information is included in the activity’s details.

## <a name="HistoryLog"></a>Historic Log
You can view the historic log of a runbook on the **Log History** tab in the **Log** pane of the Runbook Designer. This log has an entry for each completed instance of the runbook with its start and end times and completion status. If you double\-click an entry, the **Runbook Details** dialog box opens that includes each activity in the runbook and its completion status. Double\-click each activity to view its details. If you have configured logging for the workbook to include Published Data, this information is included in the activity’s details.

## <a name="LogOptions"></a>Runbook Log Options
By default, the Runbook logs do not include Published Data for each activity. For standard activities, refer to [Standard Activities](./Standard-Activities.md) for a list of the Published Data items available for each. For integration packs, refer to the specific integration pack guide. You can change the logging properties for an individual runbook to include this information in the logs. You can include both or either of the following two kinds of Published Data:

-   *Activity\-specific Published Data* is Published Data that is specific to a particular activity. Typically, this option should be enabled only for debugging purposes.

-   *Common Published Data* is a set of data items that are common to all activities. These are as follows:

    -   Activity Name

    -   Activity Type

    -   Activity ID

    -   Activity End Time Year, Month, Day, Weekday, Hours, Minutes, Seconds

    -   Activity Duration

    -   Previous Activity

    -   Previous Activity Name

    -   Time Published Data

> [!CAUTION]
> By default, logging options are disabled. Be aware that adding these items to the log increases the size of the data store.

## <a name="AuditHistory"></a>Runbook Audit History
The **Runbook Audit History** tracks the changes to each activity in a runbook. This includes the user that made the change, the date and time that the change occurred, the activity that was changed, and the current and previous values of any changed properties. The audit history is maintained as long as the runbook exists and cannot be cleared.

You can view the **Runbook Audit History** on the **Audit History** tab of the Runbook Designer. The entries for the currently selected runbook will be displayed. Double\-click an entry to open the **Details** dialog box where you can view a list of all activities that were part of the change. Select one of the entries to view the activity that was performed in addition to the old and new values of any properties that were changed.

## <a name="Purge"></a>Purging Runbook Logs
The **Runbook Designer** provides a **Log Purge** feature. [!INCLUDE[orchshort](./Token/orchshort_md.md)] log data can be purged on demand, or on a scheduled basis. A good practice is to schedule a log purge regularly during off\-peak hours to maintain the database.

> [!NOTE]
> When logs are purged, the data is deleted from Orchestration database and cannot be recovered.

If you let the number of log entries grow indiscriminately, it can result in excessive storage requirements for the Orchestration database. To maintain the health and performance of the database, you should regularly purge old log entries. You can purge either them on an automatic schedule or manually.

### Automatically Purging Runbook Logs
You can schedule the runbook logs to be purged on a regular basis by selecting frequency options and how many entries to retain. By default, runbook logs are automatically purged with the following settings.

|Setting|Default value|
|-----------|-----------------|
|Frequency|One time per day|
|Time|1:00 AM|
|Retain|Keep last 5000 entries|

The default log purge job purges all but the last 500 log entries per runbook. This means that if an [!INCLUDE[orchshort](./Token/orchshort_md.md)] deployment had 20 runbooks, the default purge would keep the last 500 log entries for each runbook, for a maximum of 10,000 log entries for the database for all runbooks.

You can continue to use these defaults or change the settings by using the following process in the Runbook Designer.

##### To purge runbooks on demand or set the purge frequency

1.  In the **Runbook Designer**, right\-click **Management server** to select **Log Purge**.

    If you want to purge all the runbooks now, click **Purge Now**.

    If you want to purge a specific runbook now, click the **Log History** tab to select the runbook to purge.

2.  Ensure that the **Schedule Log Purge** option is selected.

3.  Select the number of days between running the purge process and a time to run the process.

4.  If you do not want to delete all entries, set the **Log Purge Options** to specify the log entries that you want to keep.

5.  Click **Finish**.

### Manually Purging the Runbook Logs
Audit History logs are a special case because these logs canno bte purged with the **Log Purge** feature. The audit history feature tracks the changes made to a runbook in the **Runbook Designer** and cannot be deleted. The only way to delete Audit History logs is to delete the runbook associated with them. However, data volumes for the Audit History logs for a given runbook are generally small, even in large deployments storage will not require more than the minimum system requirements.

There are two options to manually purge the runbook logs as shown in the following two procedures. They are performed in the Runbook Designer.

##### To manually purge the runbook logs for all runbooks

1.  Right\-click **Management server** to select **Log Purge**.

2.  Set the **Log Purge Options** to specify the log entries that you want to keep.

3.  Click **Purge Now**.

##### To manually purge all runbook log entries for a single runbook

1.  In the **Connections** pane, select the **Runbooks** folder.

2.  In the workspace pane, click the tab of the runbook.

3.  In the **Log History** pane, click the **Log History** tab.

4.  Click the **Recycle Bin** icon at the top of the pane.

5.  When prompted whether you are sure that you want to purge the logs, click **Yes**.

##### To delete a specific set of runbook log entries for a single runbook

1.  In the **Connections** pane, select the **Runbooks** folder.

2.  In the workspace pane, click the tab of the runbook.

3.  In the **Log History** pane, click the **Log History** tab.

4.  Select a single log entry or use the key combination Ctrl\+Shift to select multiple entries.

5.  Click the red **Delete** icon at the top of the pane.

6.  When prompted if you are sure that you want to delete the selected entries, click **Yes**.

### Removing Orphaned Log Entries
Orphaned log files can be left in the orchestration database if the Runbook Server Service is stopped suddenly while runbook instances are running. If that happens, the runbook instance status does not get updated correctly with its ending time. These entries are removed when the log entries are purged by using one of the purging methods described above. If you want to remove orphaned entries before the next time that the entries are purged, you can manually run the **ClearOrphanedRunbookInstances** stored procedure to perform this function.

The following process describes how to run this stored procedure by using the Microsoft SQL Server Management Studio installed on the orchestration database server. You can perform this process from any computer with this tool installed that has access to the orchestration database.

##### To remove orphaned log entries

1.  On the server with the orchestration database, click **Start**, point to **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, in the **Server name** list, select **\(local\)**, and then click **Connect**.

3.  In the **Object Explorer**, expand **Databases**, and then click **Orchestrator**.

    > [!NOTE]
    > If you used a different name for the [!INCLUDE[orchshort](./Token/orchshort_md.md)] database, select that name.

4.  Expand **Programmability**, and then click **Stored Procedures**.

5.  Right\-click **Microsoft.SystemCenter.Orchestrator.Runtime.Internal.ClearOrphanedRunbookInstances** to select **Execute Stored Procedure**.

6.  In the **Execute Procedure** dialog box, click **OK**.

7.  On the toolbar, click **Execute**.

8.  When you receive a message at the bottom of the Logging pane that the query has completed, close **SQL Server Management Studio**.

## See Also
[Orchestrator Logs](./Orchestrator-Logs.md)


