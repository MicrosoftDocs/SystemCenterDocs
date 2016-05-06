---
title: How to Run a Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 006ab31c-26c3-4150-9544-5e99c32981d6
---
# How to Run a Report
Use the following procedure to run a report from the Reporting workspace. In this example, you will run an availability report.

### To run a report from the Reporting pane

1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.

2.  In the Operations console, click **Reporting**.

3.  In the **Reporting** workspace, expand **Reporting** and then click **Microsoft Generic Report Library**.

4.  In the **Reports** pane, right\-click one of the reports \(for example, **Availability**\) and then click **Open**.

5.  In the **Report** view, in the **Parameter** area, click the down arrow in the **From** box, point to **This week**, and then click **Sunday**.

6.  Click the down arrow in the **To** box, point to **Thisweek** and then click **Saturday**.

7.  Click **Use business hours**.

    > [!NOTE]
    > You can further specify the timeframe for the report in the additional options in the **Parameter** area.

8.  Click **Add Object**.

9. In the **AddObject** dialog box, in the **ObjectName** text box, type the computer name for a computer that you want to report availability, and then click **Search**.

10. In the **Availableitems** list, click the computer you want to run a report for, click **Add**, and then click **OK**.

11. Click **Run** to display the Availability Report.

12. For a more detailed report, such as a report showing a graph for every day, click the horizontal bar graph under **Availability Tracker**.

13. In the toolbar, click **View**, point to **GoTo**, and then click **Back to Parent Report** to return to the original report.

14. Click **Close** to close the report.

## See Also
[Using Reports in Operations Manager](./Using-Reports-in-Operations-Manager.md)
[How to Create Reports in Operations Manager](./How-to-Create-Reports-in-Operations-Manager.md)
[How to Save a Report](./How-to-Save-a-Report.md)
[Operations Manager Reports Library](./Operations-Manager-Reports-Library.md)
[Scheduling Reports](./Scheduling-Reports.md)
[Operations Manager Reports Library](./Operations-Manager-Reports-Library.md)
[How to Troubleshoot Reports that Return No Data](./How-to-Troubleshoot-Reports-that-Return-No-Data.md)


