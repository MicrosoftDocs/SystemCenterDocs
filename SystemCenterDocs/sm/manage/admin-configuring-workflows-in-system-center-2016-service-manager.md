---
title: Configure workflows
description: Learn about configuring workflows in Service Manager.
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  b204c2fc-c65e-41f3-a650-e425060f61b3
---

# Configure workflows in Service Manager

>Applies To: System Center 2016 - Service Manager

In Service Manager, a workflow is a sequence of activities that automate a business process. Workflows can, for example, update incidents when various changes occur. A workflow can automatically generate incidents when computers fall out of compliance from desired configuration management. You create a workflow that defines when and under what circumstances it will run. For example, a workflow can automatically change the support tier from a setting of 1 to 2 whenever a low-priority incident pertaining to printing problems is changed to a higher priority. Workflow activities function by the application of templates. For this example, an incident template to change the support tier to a setting of 2 must have been created previously.

You can create multiple workflows for each workflow configuration. You can enable or disable the workflow conditions. If a particular rule is disabled, the remaining rules still cause the workflow to run. If you want to completely disable a workflow, you must disable all of the rules that call the workflow.

The success or failure of a workflow is retained by Service Manager, and it is available for you to view. Two views are available. **All Results** consists of a view of all success and failure instances, and the **Errors** view displays only those instances when a workflow failed. In the **All Results** view, you can, for each instance, view the log and view the related object. When you view the log, you can examine the events that occurred when the workflow ran. When you view the related object, you see the form that this workflow acted on. The **Errors** view is limited to the most recent 250 instances. When you are viewing a failed instance, you have the same options in the **Success** view to view the log and view the related object. In addition, in the **Errors** view, you have the option to select **Retry** or **Ignore**. Selecting **Retry** causes the workflow to run again with the same parameters and removes this instance from the view. Selecting **Ignore** removes the instance from the view.
