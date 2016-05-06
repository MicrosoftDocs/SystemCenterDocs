---
title: How to Collect IntelliTrace Historical Profiling Traces from System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e32a8560-aada-42d3-8f6a-ff1cc207f7e6
---
# How to Collect IntelliTrace Historical Profiling Traces from System Center 2012 R2
In [!INCLUDE[omblue_1](../Token/omblue_1_md.md)], you can use [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] to capture historical snapshots \(traces\) directly from the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console and to receive IntelliTrace snapshots from .NET Application Performance Monitoring \(APM\) events. These snapshots can help developers investigate problems. They provide visibility to application execution history without needing to access the servers where the problems occurred. Developers can use Microsoft Visual Studio 2012 Ultimate or Microsoft Visual Studio 2013 Preview to open collected snapshots. For information about IntelliTrace for developers, see [Debug Your App by Recording Code Execution with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=275118)

Snapshots can be accessed from a network file share or from Team Foundation Server \(TFS\) work item attachments if TFS synchronization is enabled. For more information, see [How to Configure Integration with IntelliTrace Historical Profiling in System Center 2012 R2](../Topic/How-to-Configure-Integration-with-IntelliTrace-Historical-Profiling-in-System-Center-2012-R2.md).

> [!IMPORTANT]
> After you import and configure the IntelliTrace Profiling management pack, the IntelliTrace tasks are not available until you restart the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console.

## Collecting IntelliTrace Historical Profiling Snapshots

#### To collect IntelliTrace snapshots for an existing APM alert

1.  You can perform this procedure when you want to keep collected snapshots and attach an IntelliTrace snapshot to an alert. When TFS synchronization is enabled, the collected snapshots are attached or linked to associated work items in TFS.

2.  In the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console, click **Monitoring**, open an alert view, and then click the alert that you want to investigate.

3.  In the **Tasks** pane, expand **IntelliTrace Tasks**, and then click **Start IntelliTrace Collection**.

4.  On the **Run Task – Start IntelliTrace** page, in the **Run the task on these targets** section, select the servers from which you want to collect snapshots. The list shows all servers on which the application is configured for monitoring by the APM template in the environment where the alert occurred.

5.  In the **Task credentials section**, select **Use the predefined Run As Account** if the Default Action Account has administrative privileges on the application Internet Information Services \(IIS\) pool. Otherwise, select **Other** to specify credentials that have administrative privileges for this IIS pool.

6.  If you want to customize collection parameters, click **Override**.

7.  Click **Run**, wait for the task to be completed successfully, and then click **Close**.

    > [!IMPORTANT]
    > When you click **Run**, the application IIS pool automatically recycles on all of the servers that you selected in the **Run the task on these targets** section. APM turns off for all applications that are running in the same application pool.

8.  Reproduce the application problem that resulted in the APM exception alert.

9. Select the same alert on which you started IntelliTrace. In the **Tasks** pane, click **Collect IntelliTrace Snapshot**.

10. On the **Run Task – Collect IntelliTrace Snapshot** page, select the same servers and same **Task credentials** that you previously selected when you started IntelliTrace collection.

11. Click **Run**, wait for the task to be completed successfully, and then click **Close**. The task output indicates whether any problems occurred while running the IntelliTrace collector tasks.

12. To collect multiple snapshots, repeat the previous four steps. All snapshots that you collect are attached to the same APM alert.

13. To stop IntelliTrace collection, select the same alert on which you started IntelliTrace. In the **Tasks** pane, click **Stop IntelliTrace Collection**.

    > [!IMPORTANT]
    > Be sure to stop IntelliTrace collection. If you do not stop IntelliTrace collection, IntelliTrace will continue to run. This will impact application performance, and APM will remain off so that you will not receive new alerts from this application. To stop IntelliTrace when the alert is already closed and no longer shows in the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console, complete the step from the subsequent procedure that stops IntelliTrace: [To collect IntelliTrace snapshots when there are no APM exception alerts](../Topic/How-to-Collect-IntelliTrace-Historical-Profiling-Traces-from-System-Center-2012-SP1.md#BKMK_NAPMAL)

14. To see the IntelliTrace snapshots that are attached to an alert, select the alert. In the **Tasks** pane, click **Open Snapshot Location**.

15. If TFS synchronization is turned on, you can assign an alert to engineering. To do so, set the alert resolution state to **Assigned to Engineering**. This creates a new work item in TFS, with the snapshot attached or linked. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](../Topic/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).

### <a name="BKMK_NAPMAL"></a>To collect IntelliTrace snapshots when there are no APM alerts

1.  You can perform this procedure when you are investigating problems with application logic, poor performance \(when performance alerting on particular SLA violations is not turned on\), or when APM is not enabled for an application. The subject application in this procedure must be discovered by the IIS management packs.

2.  In the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console, click **Monitoring**, expand **Application Monitoring**, and then expand **.NET Monitoring**.

3.  If your application is running on Windows Server 2008 R2, click **IIS 7.0 ASP .NET Web Application Inventory**. If your application is running on Windows Server 2012, click **IIS 8.0 ASP .NET Web Application Inventory**.

4.  Select the application pool on which you want to run IntelliTrace profiling.

5.  In the **Tasks** pane, expand **IntelliTrace Tasks**, and then click **Start IntelliTrace Collection**.

6.  On the **Run Task – Start IntelliTrace** page, in the **Run the task on these targets** section, select the application pool in which you want to collect snapshots.

7.  In the **Task credentials section**, select **Use the predefined Run As Account** if the Default Action Account has administrative privileges on the application IIS pool. Otherwise, select **Other** to specify alternative credentials that have administrative privileges for this IIS pool.

8.  If you want to customize collection parameters, click **Override**.

9. Click **Run**, wait for the task to be completed successfully, and then click **Close**.

    > [!IMPORTANT]
    > When you click **Run**, the application IIS pool automatically recycles on all of the servers that you selected in the **Run the task on these targets** section. APM turns off for all applications that are running in the same application pool.

10. Run your application and reproduce the behavior that you want to investigate.

11. Select the same application pool on which you started IntelliTrace. In the **Tasks** pane, click **Collect IntelliTrace Snapshot**.

12. On the **Run Task – Collect IntelliTrace Snapshot** page, select the same target and same **Task credentials** that you previously selected when you started IntelliTrace collection.

13. Click **Run**, wait for the task to be completed successfully, and then click **Close**. The task output indicates whether any problems occurred while running the IntelliTrace collector tasks.

14. To collect multiple snapshots, repeat the previous four steps. For each snapshot that you collected, you will receive a new informational alert when the snapshot is uploaded to the network file share.

15. To stop IntelliTrace collection, select the same application pool on which you started IntelliTrace. In the **Tasks** pane, click **Stop IntelliTrace Collection**.

    > [!IMPORTANT]
    > Be sure to stop IntelliTrace collection. If you do not stop IntelliTrace collection, IntelliTrace will continue to run. This will impact application performance and APM will remain off so that you will not receive new alerts from this application.

16. To see the IntelliTrace snapshots, in the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console, click **Monitoring**, expand **IntelliTrace Profiling**, and then click **New Alerts**. The **New Traces** pane shows an alert for each snapshot that you have collected.

17. In the **Tasks** pane, expand **Alert Attachment Tasks**, and then click **Open Attachment Location**.

18. If TFS synchronization is turned on, you can assign an alert to engineering. To do so, set the alert resolution state to **Assigned to Engineering**. This creates a new work item in TFS with the snapshot attached or linked. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](../Topic/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).

#### To access IntelliTrace snapshots that are generated from APM data

1.  You can perform this procedure when you want to investigate an existing APM performance or exception alert that is based solely on historical data without having to run IntelliTrace Profiling on your application.

2.  In the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console, click **Monitoring**, open an alert view, and then click the alert that you want to investigate.

3.  In the **Tasks** pane, expand **Alert Attachment Tasks**, and then click **Open Attachment Location**. Windows Explorer opens the location of the files that are attached to the alert you have selected.

4.  To see the IntelliTrace snapshot for this alert, in Windows Explorer, open the **APMException** folder.

5.  If TFS synchronization is turned on, you can assign this alert to engineering. To do so, set the alert resolution state to **Assigned to Engineering**. This creates a new work item in TFS, with the snapshot attached or linked. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](../Topic/How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).

