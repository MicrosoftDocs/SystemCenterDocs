---
title: How to Troubleshoot Reports that Return No Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f1900ac-3d19-448e-bbdd-edf794d0ed8e
---
# How to Troubleshoot Reports that Return No Data
When running a Performance Report or Configuration Data Report, data might not be displayed. Use the following procedures to evaluate if any data has been collected for the report and how to find the proper parameters to use for the report. For this example, it is assumed that the Windows Server 2003 Operating System Management Pack has been imported.

Ensure that all appropriate overrides in a particular management pack have been enabled. For example, the Windows Server Operating System Management Pack does not discover physical disk partitions, only logical disk partitions.

If you want to monitor physical disk drives, you can do so by enabling the Object Discovery feature for the Windows Server 2003 physical disk or Windows 2000 Server physical disk objects. Additionally, the Microsoft Windows Server 2003 Operating System Management Pack can monitor individual instances of processors or all instances of processors together. By default, the health of the processors will be monitored as a total of all instances. If you want to monitor individual processor instances, you can do so by enabling the Object Discoveries for Windows Server 2003 Processor objects. See the appropriate management pack guide for more information about any override that you might need to enable. The two examples listed are from the Windows Server Operating System Management Pack.

After any applicable overrides have been enabled, you would use the following two procedures. In the first procedure, you will troubleshoot an instance when no data is displayed in a performance data report by using My Workspace to see if the required data has been collected in the Operations Manager database.

In the second procedure, you will troubleshoot an instance when no data is displayed in a configuration data report. In this example, it is assumed that the Operating System Configuration report returns no data.

### To troubleshoot no data in a performance report

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2.  In the Operations console, click **Reporting**.

3.  In the Reporting workspace, expand **Reporting**, and then click **Windows Server 2003 Operating System**.

4.  In the Windows Server 2003 Operating System Reports pane, click **Disk Performance Analysis**.

5.  In the Report Details pane, a list of the performance counters available in this report is displayed. Keep in mind one of the counters, for example, **LogicalDisk\\Disk Bytes\/sec\\\_Total**.

6.  In the Operations console, click **My Workspace**.

7.  In My Workspace, right\-click **My Workspace**, point to **New**, and then click **Performance View**.

8.  In the **Properties** dialog box, in the **Name** field, type a name for this view \(for this example use **Test**\).

9. In the **Criteria** tab, click **with a specific counter name**.

10. In **Criteria description** field, click **specific**.

11. In the **Counter Name** dialog box, type the name of the counter you noted in step 5, for example **Disk Bytes\/sec**, and then click **OK**.

12. In the **Properties** dialog box, click **OK**.

13. In the Test results pane, in **Legend** area, click one or more of the **Show** check boxes.

    -   If data appears in the **Test** pane, that data is available in the Operations Manager database and should be available for the report.

    -   If no data appears, click the **Authoring** button. In Authoring, expand **Authoring**, expand **Management Pack Objects**, and then click **Rules**. Look in the **Enabled by default** column for any rules that are not enabled. If they are not enabled, use overrides to enable the rule that you need for your report.

    > [!NOTE]
    > Some performance data collection rules in the Exchange Management Packs store data in only the Reporting data warehouse and cannot be verified with this procedure.

14. In the **Legend** area, examine the **Target** column and verify that the text in the **Target** column matches what is listed in the **Object** column in the Parameter Area of the report. If the value listed in the **Target** column is different, use the value listed in **Target** column in the report and run the report again.

    > [!NOTE]
    > When searching for the name of an object in a report, you might find that the name of the hosting computer is listed only in the **Object path** column in the Parameter Area. If you want to locate multiple specific objects, you can create a dynamic group containing the correct types of objects and run the report with this new group. For more information about creating groups, see [How to Create Groups in Operations Manager](How-to-Create-Groups-in-Operations-Manager.md).

### To troubleshoot no data in a configuration data report

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2.  In the Operations console, click **My Workspace**.

3.  In My Workspace, right\-click **My Workspace**, point to **New**, and then click **State View**.

4.  In the **Properties** dialog box, in the **Name** field, type a name for this view \(for this example use **Test1**\).

5.  On the **Criteria** tab, click the ellipses \(**…**\) next to the **Show data related to** box.

6.  In the **Select a Target Type** dialog box, click **View all Targets**.

7.  In the **Find** box, type **Windows Operating System**.

8.  In the **Target** column, click **Windows Operating System**, and then click **OK**.

9. In the **Properties** dialog box, examine the contents in the list with the check boxes contain the data that you wanted to run a report against \(for example, Build Number\), and then click **OK**.

10. In the Test1 results pane, examine the content in the **Name** column. The values listed in the **Name** column are the correct object names you need to search for when searching for objects for the report.

    > [!NOTE]
    > When searching for the name of an object in a report, you might find that the name of the hosting computer is listed only in the **Object path** in the Parameter Area. In this instance, you need to create a dynamic group containing the correct types of objects and run the report with this new group. For more information about creating groups, see [How to Create Groups in Operations Manager](How-to-Create-Groups-in-Operations-Manager.md).

## See Also
[Using Reports in Operations Manager](Using-Reports-in-Operations-Manager.md)
[How to Create Reports in Operations Manager](How-to-Create-Reports-in-Operations-Manager.md)
[How to Save a Report](How-to-Save-a-Report.md)
[How to Run a Report](How-to-Run-a-Report.md)
[Scheduling Reports](Scheduling-Reports.md)
[How to Export a Report](How-to-Export-a-Report.md)
[Operations Manager Reports Library](Operations-Manager-Reports-Library.md)


