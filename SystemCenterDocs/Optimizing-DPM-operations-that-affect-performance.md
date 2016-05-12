---
title: Optimizing DPM operations that affect performance
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8f9df03-9b9d-4841-bd8c-3002288823b2
---
# Optimizing DPM operations that affect performance
There are a number of steps you can take to optimize the performance of [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] data replication and synchronization, including:

-   [Configure network throttling](#BKMK_Throttle)

-   [Enable data compression](#BKMK_Compress)

-   [Stagger synchronization start times](#BKMK_Stagger)

-   [Perform initial replication offline](#BKMK_Replica)

-   [Modify the schedule for express full backups](#BKMK_Express)

## <a name="BKMK_Throttle"></a>Configure network throttling
Network bandwidth throttling limits the amount of network bandwidth that [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] can use to create and synchronize replicas. Note that throttling can lengthen the amount of time each synchronization job takes to complete. Throttling isn’t turned on by default.

#### To enable network bandwidth usage throttling

1.  In DPM Administrator Console, go to the **Management** view.

2.  Open the **Agent** workspace, and select the computer you want to throttle.

3.  Click **Throttle computer**.

4.  In the **Throttle** dialog box, check **Enable network bandwidth usage**.

5.  Select **Throttle Settings** and **Work Schedule** for the computer.

    > [!NOTE]
    > You can configure network bandwidth usage throttling separately for work hours and nonwork hours, and you can define the work hours for the protected computer.

6.  To apply your settings, click **OK**.

    Network bandwidth usage can be also limited by Group Policy. The Group Policy reservable bandwidth limit on the local computer determines the combined reservable bandwidth for all programs that use the Packet Scheduler, including DPM. The DPM network bandwidth usage limit determines the amount of network bandwidth that DPM can consume during replica creation, synchronization, and consistency checks. If the DPM bandwidth usage limit, either by itself or in combination with the limits of other programs, exceeds the Group Policy reservable bandwidth limit, the DPM bandwidth usage limit might not be applied.

    For example, if a DPM computer with a 1\-gigabit\-per\-second \(Gbps\) network connection has a Group Policy reservable bandwidth limit of 20 percent, 200 Mbps of bandwidth is reserved for all programs that use the Packet Scheduler. If DPM bandwidth usage is then set to a maximum of 150 Mbps while Internet Information Services \(IIS\) bandwidth usage is set to a maximum of 100 Mbps, the combined bandwidth usage limits of DPM and IIS exceed the Group Policy reservable bandwidth limit, and the DPM limit might not be applied.To resolve this issue, reduce the DPM setting for network bandwidth usage throttling.

## <a name="BKMK_Compress"></a>Enable data compression
Compression decreases the size of data being transferred during replica creation and synchronization and allows more data throughput with less impact to network performance. However, this option adds to the CPU load on both the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server and protected computers. The amount of compression and improvement on network performance depends on workload.

Compression is enabled at the protection group level and applies to replica creation, synchronization, and consistency check operations. Recovery jobs also use compression.

#### To enable on\-the\-wire compression

1.  In [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Administrator console, go to the **Protection** view.

2.  Click **Optimize performance**.

3.  On the **Network** tab, check **Enable on\-the\-wire compression**.

4.  To apply your changes, click **OK**.

## <a name="BKMK_Stagger"></a>Stagger synchronization start times
To optimize performance, you can offset the start time of synchronization jobs across different protection groups so that all of them do not start at the same time. Offsetting synchronization start times can also be used to optimize secondary protection of another DPM server.

#### To stagger synchronization start times

1.  In [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Administrator Console, go to the **Protection** view.

2.  In the display area, select a protection group.

3.  Click **Optimize performance** on the tool ribbon.

4.  On the **Network** tab, select the hours and minutes to offset the start of the synchronization job in the **Offset <time> start time by** field.

    > [!NOTE]
    > The maximum allowed value for offset is the same as the synchronization frequency.

5.  To apply your changes, click **OK**.

    > [!NOTE]
    > Changing the start time offsets recovery points for files by the equivalent amount of time. This setting does not apply to protection groups for client computers.

## <a name="BKMK_Replica"></a>Perform initial replication offline
When you create a protection group you select a method to create an initial replica of the data you want to protect. If you select the automatic option PDM copies the data across the network. However you can set an option for create a replica manually. With this option selection you manually copy the data using removable media. You’ll need ot know the details of the source path on the protected computer and the replica path on the DPM server. It’s critical to retain the same directory structure and properties \(time stamps and security permissions\) as those for the data that you are protecting. For large amount of data it might be quicker to do a manual replica than to replicate over the network. We recommend that you use the manual method if you’re deploying DPM to protect data over a WAN and your protection group includes more than 5 GB of data.

#### To display the details of the source and replica paths

1.  In DPM Administrator Console, go to the **Protection** view.

2.  Select the data source you want to replicate on the DPM server.

3.  Click  **View Details** on the tool ribbon. The **Details of Replica Path** dialog box is displayed.

4.  Copy the list view content for reference. To copy the replica path, select a row in the **Details of Replica Path** dialog box, and then press CTRL\+C.

#### To copy data files from a protected computer to the DPM server

1.  In the **Protection** view, select the protected data and then locate the **Replica path** in the **Details** pane.

2.  In the **Details** pane, select the replica path and copy it into a text editor such as Notepad. The path will look like the following:

    **<Drive:>\\DPM\\DPM\\Volumes\\Replica\\Fileserver.mydomain.corp.myorg.com\\File System\\D\-87a82ad4\-f9d2\-11d9\-b758\-000d561ae74f\\e55173e1\-0b7a\-4fa4\-b4d1\-387ac2b016b8\\3ed60b1c\-dcf8\-442e\-b441\-d771a3d7f014\\Users**

    > [!NOTE]
    > You cannot change the directory to this path in Windows Explorer because it is too large.

3.  To access the Users folder, perform the following steps:

    1.  At the command prompt, type **mountvol** and then press Enter.

    2.  From the list of mounted volumes, pick the volume that corresponds to the appropriate path. The path will look like the following:

        **\\\\?\\Volume{a2072784\-7573\-4dce\-a7e9\-26713fd12697}\\**

        **<Drive:>\\DPM\\DPM\\Volumes\\Replica\\Fileserver.mydomain.corp.myorg.com\\File System\\D\-87a82ad4\-f9d2\-11d9\-b758\-000d561ae74f\\**

    3.  Type the following to mount the volume to a drive letter:

        **mountvol k:\\ \\\\?\\Volume{a2072784\-7573\-4dce\-a7e9\-26713fd12697}\\**

    4.  Click **Start**, double\-click **My Computer**, and on the **Tools** menu, click **Folder Options**.

    5.  In the **Folder Options** dialog box, on the **View** tab, in the **Advanced settings** box, under **Hidden files and folders**, clear the **Hide protected operating system files \(Recommended\)** option, click **Yes** to confirm that you want to display the files, and then click **OK**.

        Now you can browse to view the entire path from step 3 in Windows Explorer.

4.  Manually copy the data to the Users folder under the drive letter you used to map the volume \(K:\\ in this example\). Overwrite any data in the Users folder.

5.  After you copy the data to the replica location, perform a synchronization with consistency check. Protection will start after the synchronization with consistency check has successfully completed.

6.  At the command prompt, type the following to remove the drive letter that you used to mount the volume:

    **mountvol k:\\ \/d**

    > [!NOTE]
    > In Windows Server 2008, run the command from an elevated command prompt.

For replication of workload data such as SQL Server, Exchange Server, or SharePoint you can use the following procedure.

#### To create a manual replica for application servers

1.  Use the specific application administrator console to determine the location of the data files for the data source you are protecting. For example, use SQL Management Studio for Microsoft SQL Server 2005 databases.

2.  Use the native backup tool to back up the data files of the data source. In Windows Server 2003, click **Start**, click **Run**, and then enter **ntbackup**.

    You should perform a file\-level backup and not an application backup. For example, back up the Exchange log and databases as files and not as an application.

    > [!IMPORTANT]
    > Use the Volume Shadow Copy Service \(VSS\) parameter of the Ntbackup tool to ensure that the file backup includes recovery points. The parameter is *\/SNAP:on*.

3.  In DPM Administrator Console, go to the **Protection** view.

4.  In the display pane, select a data source.

5.  In the **Details** pane, click **Click to view details**. The **Details of Replica Path** dialog box displays the original path of the data files on the protected server and the target path where this data should be copied.

6.  Use Ntbackup to restore the data files to the corresponding paths on the DPM server to create the manual replica.

7.  When you have copied the data to the DPM Server from DPM Administrator Console, go to the **Monitoring** view and then open the **Alerts** workspace.

8.  In the **Manual Replica Creation Pending** alert, you can choose to run a consistency check job.

    > [!NOTE]
    > You can also run a consistency check job in the **Protection** area of the navigation pane for this data source.

Note that as an alternative you could stop the application service, copy the files between the protected server and the destination \(DPM\) server, and then restart the application service. If you do this, for SharePoint the following data sources should be copied:

-   All of the SQL databases—configuration database, content databases, security support provider databases, and the search database.

-   Search indexes, if you have enabled a search service or server.

When you create a manual replica for application servers, DPM displays a **Details of Replica Path** dialog box. The path defined under the Destination \(DPM Server\) column in the Details of Replica Path dialog box corresponds to the volume root of each corresponding data file on the source protected server. You must recreate the folder hierarchy under this volume root so that the folder hierarchy under the specified DPM replica path is the same as the relative path\/folder hierarchy under the volume root of the protected server. This must be done for each data file that is part of the data source. For example, if the SQL Server database files are located under G:\\Dir, the files are named G:\\Dir\\Dir.mdf and G:\\Dir\\Dir\_log.ldf. Using this example, the Details of Replica Path dialog box displays the following paths.

|Source \(protected server\)|Destination \(DPM server\)|
|-------------------------------|------------------------------|
|G:\\on widgets.corp.microsoft.com|C:\\Program Files\\Microsoft DPM\\DPM\\Volumes\\Replica\\widgets.corp.microsoft.com\\SqlServerWriter\\Dir\\5f933057\-a1fa\-432c\-9c2f\-86d64e91e21f\\Full\\G\-Vol\\|

To perform a manual load, copy dir\\dir.mdf and dir\\dir\_log.ldf under the path so that the final paths are as follows:

-   **Database**: \\Program Files\\Microsoft DPM\\DPM\\Volumes\\Replica\\widgets.corp.microsoft.com\\SqlServerWriter\\Dir\\5f933057\-a1fa\-432c\-9c2f\-86d64e91e21f\\Full\\G\-Vol\\dir\\dir.mdf

-   **Log**: \\Program Files\\Microsoft DPM\\DPM\\Volumes\\Replica\\widgets.corp.microsoft.com\\SqlServerWriter\\Dir\\5f933057\-a1fa\-432c\-9c2f\-86d64e91e21f\\Full\\G\-Vol\\dir\\dir\_log.ldf

## <a name="BKMK_Express"></a>Modify the schedule for express full backups
To provide quick recovery of application data, DPM must create an express full backup periodically. The express full backup operation typically increases the demand on the server's resources by 5 percent for several minutes. To reduce the demand on the server's resources, you can schedule fewer express full backups, but this can increase data recovery time.

> [!NOTE]
> You can modify the schedule for express full backups only for applications that are part of a protection group. For files that are part of a protection group, use the Create New Protection Group Wizard to specify your short\-term backup objective.

#### To modify the schedule for express full backups

1.  In DPM Administrator Console, go to the **Protection** view.

2.  In the display pane, select a protection group for which you want to modify the express full backup schedule.

3.  Click **Optimize performance** on the tool ribbon.

4.  On the **Express Full Backup** tab, select the available times for the express full backups and click **Add**.

5.  Select the days of the week for the express full backups.

6.  To apply your changes, click **OK**.

    > [!NOTE]
    > To modify the express full backup, you need to use the **Modify protection group** wizard.


