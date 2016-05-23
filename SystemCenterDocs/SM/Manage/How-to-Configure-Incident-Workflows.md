---
title: How to Configure Incident Workflows
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf7c1bd2-c986-4979-b7c6-b6ccf300a632
---
# How to Configure Incident Workflows
You can use the following procedure to create and configure a workflow rule that will change the support tier to **Tier 2** whenever the **Urgency** property of an incident that is related to printing problems is changed to **High**. This procedure assumes that you already created an incident template to change the support tier to **Tier 2**, and it assumes that you already created the priority calculation table. For more information, see [How to Set Incident Priority](How-to-Set-Incident-Priority.md) and “To create a new printer\-related incident template” in [How to Create Incident Templates](How-to-Create-Incident-Templates.md).

### To configure an incident workflow

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Configuration**.

3.  In the **Configuration** pane, double\-click **Incident Event Workflow Configuration**.

4.  In the **Configure Incident Event Workflows** dialog box, click **Add**.

5.  In the **Add Incident Event Workflow** dialog box, complete these steps:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **Workflow Information** page, in the **Name** box, type a name for the workflow. For example, type **Escalates Printer Problems to Support Tier 2 when the Urgency property is changed to High**.

    3.  In the **Check for events** list, select **when an object is created or when an object is updated**, make sure that the **Enabled** check box is selected, and then click **Next**.

    4.  On the **Specify Event Criteria** page, click the **Changed to** tab. In the **Available Properties** list, select **Urgency**, and then click **Add**. In the **Criteria** box, select **equals**. In the list, select **High**. Then, click **Next**.

    5.  On the **Select Incident Template** page, click **Apply the following template**, and then select the template you created earlier that will set the support group to **Tier 2**. For example, select **Escalate Printer Problems to Tier 2**, and then click **Next**.

    6.  Optionally, in the **Select People to Notify** page, select the **Enable notification** check box, select the user to notify, and then click **Next**.

    7.  On the **Summary** page, review your settings, and then click **Create**.

    8.  On the **Completion** page, click **Close**.

6.  In the **Configure Incident Event Workflows** dialog box, click **OK**.

### To validate an incident workflow

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Work Items**.

2.  In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and then click **All Incidents**.

3.  In the **All Incidents** pane, double\-click an incident that is not currently assigned to the tier 2 support group.

4.  In the **Incident Form** page, set the **Urgency** property to **High**, and then click **OK**.

5.  In a few minutes, press F5. Verify that the value in the **Support Group** box changed to **Tier 2**.

![](Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a new workflow in Service Manager, see [New\-SCSMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225361).

-   For information about how to use Windows PowerShell to retrieve configuration and status information for  [!INCLUDE[smshort](../../Token/smshort_md.md)] workflows, see [Get\-SCSMWorkflowStatus](http://go.microsoft.com/fwlink/p/?LinkID=225347).

-   For information about how to use Windows PowerShell to update workflow properties, see [Update\-SCSMWorkflow cmdlet](http://go.microsoft.com/fwlink/p/?LinkID=225392).

-   For information about how to use Windows PowerShell to remove a workflow from [!INCLUDE[smshort](../../Token/smshort_md.md)], see [Remove\-SCSMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225372).


