---
title: How to Create an Event Analysis Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edb543b9-e405-4a72-8864-d35c3704d318
---
# How to Create an Event Analysis Report
Use the following procedure to create an event analysis report.

### To create an event analysis report

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Monitoring**.

3.  In the **Monitoring** workspace, expand **Monitoring**, and then click **Windows Computers**.

4.  In the **Windows Computers** pane, click a row containing a Health Service instance.

5.  In the **Tasks** pane, under **Report Tasks**, click **Event Analysis**.

6.  In the **Reporting Parameter** area, click the down arrow in the **From** box, and then click **Yesterday**.

    > [!NOTE]
    > You can further specify the timeframe for the report in the additional options in the Reporting Parameter area.

7.  In the **Reporting Parameter** area, under **Monitoring Object**, click **Add**.

8.  In the **Add Object** dialog box, in the **Object Name** list, click the down arrow, and then click **Begins with**.

9. In the **Object name** text box, type the computer name for the computer you selected in step 4, and then click **Search**.

10. In the **Available items** list, click the computer with the **Type** of **Health Service**, click **Add**, and then click **OK**.

11. In the **Reporting Parameter** area, in the **Monitoring Object** list, click the entry that is not of the type **Health Service**, and then click **Remove**.

12. Click **Run** to display the **Event Analysis Report**.

13. Click **Close** to close the report.


