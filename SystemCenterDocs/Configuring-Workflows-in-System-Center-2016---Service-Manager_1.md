---
title: Configuring Workflows in System Center 2016 - Service Manager_1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5790391a-1821-44f4-8666-3f264a306753
robots: noindex,nofollow
---
# Configuring Workflows in System Center 2016 - Service Manager_1
In [!INCLUDE[smlong12](./Token/smlong12_md.md)], a workflow is a sequence of activities that automate a business process. Workflows can, for example, update incidents when various changes occur. A workflow can automatically generate incidents when computers fall out of compliance from desired configuration management. You create a workflow that defines when and under what circumstances it will run. For example, a workflow can automatically change the support tier from a setting of 1 to 2 whenever a low\-priority incident pertaining to printing problems is changed to a higher priority. Workflow activities function by the application of templates. For this example, an incident template to change the support tier to a setting of 2 must have been created previously.

You can create multiple workflows for each workflow configuration. You can enable or disable the workflow conditions. If a particular rule is disabled, the remaining rules still cause the workflow to run. If you want to completely disable a workflow, you must disable all of the rules that call the workflow.

The success or failure of a workflow is retained by [!INCLUDE[smshort](./Token/smshort_md.md)], and it is available for you to view. Two views are available. **All Results** consists of a view of all success and failure instances, and the **Errors** view displays only those instances when a workflow failed. In the **All Results** view, you can, for each instance, view the log and view the related object. When you view the log, you can examine the events that occurred when the workflow ran. When you view the related object, you see the form that this workflow acted on. The **Errors** view is limited to the most recent 250 instances. When you are viewing a failed instance, you have the same options in the **Success** view to view the log and view the related object. In addition, in the **Errors** view, you have the option to select **Retry** or **Ignore**. Selecting **Retry** causes the workflow to run again with the same parameters and removes this instance from the view. Selecting **Ignore** removes the instance from the view.

## Configuring Workflow Topics

-   [How to Configure Incident Workflows](./How-to-Configure-Incident-Workflows.md)

    Describes how to create an incident event workflow rule that changes the support tier level from 1 to 2 because of a change in incident priority.

-   [How to View Workflow Success or Failure](./How-to-View-Workflow-Success-or-Failure.md)

    Describes how to view the success or failure of a workflow.

## Other Resources for This Component

-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)

-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)

-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)

-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)


