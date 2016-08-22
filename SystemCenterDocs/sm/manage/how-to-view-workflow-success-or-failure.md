---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to View Workflow Success or Failure
ms.technology:  service-manager
ms.assetid:  eb1f9f39-6d4e-4f8c-b236-c1d3bf90f5f3
---

# How to View Workflow Success or Failure

>Applies To: System Center 2016 Technical Preview - Service Manager

Use the following procedure to view the success or failure instances of the workflows.

### To view workflow success or failure

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Status**.

3.  In the **Status** pane, click the workflow that you want to view. For example, click **Escalates Printer Problems to Support Tier 2 when the Urgency property is changed to High**.

4.  In the **Status** results pane, click **Need attention** to view workflows that did not run successfully. Or, click **All Instances**, and then do the following:

    1.  Click **View log** to view the list of events that occurred when the workflow ran.

    2.  Click **View related object** to view the form that was used when the workflow ran.

    The status of each workflow is displayed in the **Status** column.

![](../media/pssymbol.png)You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to retrieve the status of workflows in Service Manager, see [Get-SCSMWorkflowStatus](http://go.microsoft.com/fwlink/p/?LinkID=225347).



