---
title: Initiating and Classifying a Change Request
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16d49b02-a266-40d3-a81e-fdb9405d0e56
---

# Initiating and Classifying a Change Request

>Applies To: System Center 2016 - Service Manager

The procedures in this section describe how to initiate and classify a change request in Service Manager from start to finish.  

 A change request normally results in a change to a configuration item. Therefore, it is important to understand the difference between a related item and a linked or affected item. A related item indicates that an association exists between the change request and a configuration item or other change requests. In other words, the change request might affect the related item or it might not. An affected or linked item indicates that the change request is tied directly to the item and that the change will affect the item itself.  

 Complete the following steps to initiate and classify a change request.  

## How to Create a New Change Request

You can use the following procedures in Service Manager to create a change request for servers that are part of a service and then validate the creation of the change request. First, you view items from the service dependency view. Then, you navigate to the configuration items and open a change request template. Lastly, you assess the priority, impact, and risk level of the request. Although you create the change request from a service dependency view, you can also create a new change request from other places in Service Manager.  

> [!NOTE]  
>  IDs that are assigned to change requests and incidents are not created in sequence. However, newer change requests and incidents are assigned IDs with a higher number than ones created previously.  

### To create a change request  

1.  In the Service Manager console, click **Configuration Items**.  

2.  In the **Configuration Items** pane, expand **Business Services**, and then click **All Business Services**.  

3.  In the **All Business Services** pane, double\-click the service. For example, double\-click **IT Messaging Service**.  

4.  In the dialog box that opens, click the **Service Dependents** tab.  

5.  In the **Expand to** list, click **Level 1**, and then view the items in the list. Notice the server names. For example, **Exchange01.woodgrove.com** and **Exchange02.woodgrove.com** appear in the list.  

6.  In the **Service Dependents** list, select a computer, and then click **Open**. For example, select and open **Exchange01.woodgrove.com**.  

7.  In the computer form, click **Create Related Change Request** under **Tasks**.  

8.  In the **Select Template** dialog box, click a template, and then click **OK**. For example, click **Changes to messaging infrastructure template**.  

9. In the **Title** box, type a name for the change request. For example, type **Apply Exchange Server Service Pack**. Notice that various values in the form are populated with information from the change request template.  

10. In the **Description** and **Reason** fields, type a description and the reason for the change request. For example, type **Apply Exchange Server Service Pack to these servers** in the **Description** field, and type **The service pack fixes the problem that these servers have** in the **Reason** field.  

11. In the **Assigned To** field, enter the name of the person to whom you want to assign the change request. For example, type **Aaron Lee**.  

12. Specify the priority, impact, and risk. For example, In the **Priority** list, select **Medium**. In the **Impact** list, select **Standard**. In the **Risk** list, click **Medium**.  

13. In the **Config Items To Change** list, make sure that one server is listed, and then click **Add**.  

14. In the **Select Objects** dialog box, select another item to add to the change request, and then click **Add**. For example, select **Exchange02.woodgrove.com**, and then click **OK**.  

15. Click **OK** to close the change request form.  

### To validate the creation of a change request  

1.  Open the service that contains the items for which you created the change request, and then click the **Service Dependents** tab.  

2.  In the **Service Components** list, notice that the two servers you opened the change request for are marked with **YES** under the **Affected By Change** column.  

3.  Click **Cancel** to close the service.  

## How to Add Related Items to a Change Request

You can use the following procedures to add related items to a change request and then validate the addition of the items. You can add related items, such as configuration items, incidents, other change requests, files, and knowledge articles. When you add files, such as saved screen shots, saved written procedures, and knowledge articles, reviewers and implementers can more easily review, approve, and implement the change.  

 To add files to any work item, including change requests, you must first enable the appropriate option. For more information, see [How to Configure General Change Settings](admin-how-to-configure-general-change-settings.md).  

### To add related items to a change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  

3.  In the **All Change Requests** pane, double\-click the change request to which you want to add an item.  

4.  Click the **Related Items** tab.  

5.  On the **Related Items** tab under **Attached Files**, click **Add** to attach a file to the change request.  

    > [!NOTE]  
    >  You might need to maximize the form to view buttons on the tab.  

6.  Under **Knowledge Articles**, click **Add** to attach a knowledge article to the change request.  

7.  Click **OK**.  

### To validate that you added related items to a change request  

-   To verify that the file and knowledge articles were attached to the change request, reopen the change request, and then click the **Related Items** tab.

## How to Add Manual Activities to a Change Request

You can use the following procedures to add a manual activity and then assign it to yourself and then validate that the manual activity was added. For example, when you investigate a new change request, you might want to add a manual activity to the change request. This manual activity could be any task that is not defined in the change request template that was used to create the change request.  

> [!NOTE]  
>  You cannot delete an activity in a change request if the change request is in progress, however you can skip the activity or put the change request on hold and then delete the activity.  

### To add a manual activity  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  

3.  Double\-click the change request to which you want to add a manual activity. For example, double\-click **Apply Exchange Server Update**.  

4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Manual Activity**, and then click **OK**.  

5.  In the **Title** box, type a name that describes the manual activity. For example, type **Warranty Review**.  

6.  In the **Description** box, type a description of the manual activity. For example, type **Verify that the server is still under warranty before approval**.  

7.  Under **Activity Implementer**, click the ellipsis button \(...\).  

8.  In the **Select User** dialog box, select the name of the person who will perform the manual activity, and then click **OK**. For example, select **Aaron Lee**.  

9. Click **OK** to update the changes to the manual activity.  

10. Click **OK** to update the change request and to close the form.  

### To validate that the manual activity was added  

-   Reopen the change request, and then click the **Activities** tab to view the manual activity that you added.  

## How to Add Dependent Activities to a Change Request for Release Records

You can use the following procedures to add a dependent activity to an existing change request, which is used as part of the release management process. Although you can add dependent activities to work items, such as release records and service requests, the primary purpose of a dependent activity is for use as a mechanism to associate a change request with a release record. Specifically, a manual activity in a release record is linked to the dependent activity in a change request. When it is completed, the dependent activity indicates that the release management process is complete for the change request.  

 If you intend to use release management as part of the standard processes in your organization, consider adding dependent activities to change request templates. For more information about creating change request templates, see [How to Create Change Request Templates](admin-how-to-create-change-request-templates.md).  

### To add a dependent activity to a change request  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  

3.  Double\-click the change request to which you want to add a dependent activity. For example, double\-click **Apply Exchange Server Update**.  

4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Dependent Activity**, and then click **OK**.  

5.  In the **Title** box, type a name that describes the dependent activity. For example, type **Exchange Server Update - Deploy, Test, and Verify** .  

6.  In the **Description** box, type a description of the dependent activity. For example, type **Verify that the service pack is deployed, tested, and verified successful**.  

7.  Under **Owner**, click the ellipsis button \(...\).  

8.  In the **Select User** dialog box, select the name of the person who has overall responsibility for the dependent activity, and then click **OK**.  

9. Under **Assigned To**, click the ellipsis button \(...\).  

10. In the **Select User** dialog box, select the name of the person who will perform the dependent activity, and then click **OK**. For example, select **Aaron Lee**.  

11. As an option, specify scheduling information on the **Scheduling** tab.  

12. Click **OK** to update the changes to the dependent activity.  

13. Click **OK** to update the change request and to close the form.  

### To validate that the dependent activity was added  

-   Reopen the change request, and then click the **Activities** tab to view the dependent activity that you added.  
