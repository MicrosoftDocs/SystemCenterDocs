---
title: How to Create a Configuration Changes Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8133f0ab-07ee-4c23-8c8c-7c13eac1492a
---
# How to Create a Configuration Changes Report
[!INCLUDE[om12long](../Token/om12long_md.md)] monitors parameters of objects that are defined in management packs. You can create a Configuration Changes report listing changes that have occurred to monitored parameters. You should expect a delay of at least 2 minutes from the time when a change is made until it is reflected in a Configuration Changes report. In the following example procedure, you will make a change to the Heartbeat Interval setting and then create a Configuration Changes report to view the result.

### To report configuration changes

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  Click **Settings**.

4.  Under **Agent**, double\-click **Heartbeat** .

5.  Change the agent Heartbeat Interval from its default value of 60 seconds to 120 seconds, and click **OK**.

6.  In the Operations console, click **Monitoring**.

7.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

8.  In the **Windows Computers** pane, click a row containing a Health Service instance.

9. In the **Tasks** pane, under **Report Tasks**, click **Configuration Changes**.

10. In the **Reporting Parameter** area, click the down arrow in the **From** box, and then click **Yesterday**.

    > [!NOTE]
    > You can further specify the timeframe for the report in the additional options in the Reporting Parameter area.

11. In the **Reporting Parameter** area, under **Monitoring Object**, click **Add**.

12. In the **Add Object** dialog box, in the **Object Name** list, click the down arrow and then click **Begins with**.

13. In the **Object name** text box, type the computer name for the computer you selected in step 5, and then click **Search**.

14. In the **Available items** list, click the computer with the **Type** of **Health Service**, click **Add**, and then click **OK**.

15. In the **Reporting Parameter** area, in the **Monitoring Object** list, click the entry that is not of the type **Health Service**, and then click **Remove**.

16. Click **Run** to display the **Configuration Changes Report**.

17. Click **Close** to close the report.

