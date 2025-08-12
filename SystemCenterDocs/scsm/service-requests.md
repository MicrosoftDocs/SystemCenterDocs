---
title: Manage service requests
description: Explains how to manage service requests in Service Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 9a0583e5-0eaa-42d0-a704-2301ca3af342
---

# Manage service requests in Service Manager



Service requests are requests for existing, preauthorized services and features that Service Manager can manage as a type of work item. Service requests help you deliver a service request fulfillment solution to align your business and information technology (IT) strategy and ensure that IT services provide business value. Service requests are tightly coupled with the service catalog, and together they help add value to your IT organization by clearly managing service requests. This can help lead to a better understanding of the supply and demand for services and a more efficient and transparent customer service provided by your IT organization.  

 Service request functionality in Service Manager is based on Microsoft Operations Framework (MOF)&nbsp;4.0 and Information Technology Infrastructure Library (ITIL)&nbsp;V3 processes in order to align with industry standards. While not all functionality was completed with strict adherence to those standards, the following items are included in service request fulfillment in Service Manager:  

- Processes to record, track, and process service requests  

- Service fulfillment workflow automation  

- A consistent interface that helps Service Manager administrators identify and map their existing IT services  

- Support for situations where cost tracking and service level agreements (SLAs) are required  

- Time-to-resolution tracking through SLA integration  

## Create a service request using the Service Manager console

End-users often create service requests in Service Manager by accessing the service catalog from the Self-Service Portal or by submitting email requests. However, you can use the following procedure to manually create a new service request in the Service Manager console. For example, you might want to manually create a new service request if a user contacts the help desk by telephone. In the following example, you can update any information that you want to as you complete the form.  

To create a new service request using the Service Manager console, follow these steps:

1. In the Service Manager console, expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Assigned To Me**.  

2. In the **Tasks** pane under **Service Request Fulfillment**, select **Create Service Request from Template**.  

3. Under **Templates** in the **Select Template** dialog, select a template, and select **OK** to open a new service request and apply the template. For example, select **Request Membership to Group**.  

4. In the **&lt;SR&lt;ID&gt;: ServiceRequestName&gt;** form in the **Affected user** box, select the user who submitted the service request. For example, select **Joe Andreshak**.  

5. Optionally, in the **Alternate Contact Method** box, enter additional contact information for the affected user.  

6. In the **Title** box, enter a title for the service request or update one if it has been populated by a template. For example, enter **Request Membership to Active Directory Group - Joe Andreshak**.  

7. In the **Description** box, enter a description for this service request.  

8. In the **Urgency** and **Priority** lists, select one for each if they haven't been populated by a template.  

9. In the **Source** list, select **Portal** if it hasn't been populated by a template.  

10. In the **Assigned to** box, choose an analyst to assign the service request to. For example, assign the service request to yourself.  

11. Select **OK** to save and close the service request form.  

## Approve and complete a service request using activities

You can use the following procedures to approve a review activity and complete a manual activity for a service request in the Service Manager console. In many cases, multiple people or groups must vote to approve a single review activity before its approval is final. After approval, a service request might need a manual activity completed to verify that the service was provided to the requesting user and to close the service request.  

>[!NOTE]  
> Users can only approve or reject and close the activities that are assigned to them.  

### Approve a review activity for a service request  

1. In the Service Manager console, select **Work Items**.  

2. In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Review Activities**, and select **Activities Assigned to Me**.  

3. Select a review activity. For example, select the **Approval for the user requesting membership to an Active Directory group**.  

4. In the **Tasks** pane, select **Approve**.  

5. In the **Comments** dialog, enter any comments that you have for the approval or rejection, and select **OK**.  

### Complete a manual activity for a service request  

1. In the Service Manager console, select **Work Items**.  

2. In the **Work Items** pane, expand **Work Items**, expand **Activity Management**, expand **Manual Activities**, and select **Activities Assigned to Me**.  

3. Select a manual activity. For example, select the **Approval for the user requesting membership to an Active Directory group**.  

4. In the **Tasks** pane, select **Mark as Completed**.  

5. In the **Comments** dialog, enter any comments that you've for the manual activity, and select **OK**. For example, enter **The Active Directory administrator has added this user to the groups requested**.  

## Cancel a service request

Occasionally, you might need to cancel a service request in Service Manager. You can accomplish this by using the Service Manager console. You can use the following procedure to cancel a service request.  

To cancel a service request, follow these steps:

1. In the Service Manager console, select **Work Items**.  

2. In the **Work Items** pane, expand **Work Items**, expand **Service Request Fulfillment**, and select **All Open Service Requests** or some other service request view.  

3. Select the service request that you want to cancel. For example, select **Request Membership to Active Directory Group - Joe Andreshak**.  

4. In the **Tasks** pane, select **Cancel**.  

5. In the **Comments** dialog, enter any comments that you have for canceling the service request, and select **OK**. For example, enter **This request was a duplicate and is not needed**.  

## Close a service request

After all the review activities are approved or rejected and any manual activities are completed, you can close a service request in the Service Manager console. You can use the following procedure to close a service request.  

To close a service request, follow these steps:

1. In the Service Manager console, select **Work Items**.  

2. In the **Work Items** pane, expand **Work Items**, expand **Service Request Fulfillment**, and select **Completed Service Requests**.  

3. Select a completed service request. For example, select **Request Membership to Active Directory Group - Joe Andreshak**.  

4. In the **Tasks** pane, select **Close**.  

5. In the **Comments** dialog, enter any comments that you've for the closure, and select **OK**.  

## Edit a service request

Service requests are often created by end users by accessing the service catalog from the Self-Service Portal or by submitting email requests, and you might need to update a service request with additional information. You can use the following procedure to update a service request in the Service Manager console.  

To edit a service request using the Service Manager console, follow these steps:

1. In the Service Manager console, expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Assigned To Me**.  

2. In the list, select a service request to edit, and then in the **Tasks** pane under **&lt;Service Request ID - Service Request Name&gt;**, select **Edit**. For example, select **Request Membership to Active Directory Group**.  

3. In the **&lt;SR&lt;ID&gt;: ServiceRequestName&gt;** form in the **Affected user** box, select the user who submitted the service request. For example, select **Joe Andreshak**.  

4. Update any information in the form as necessary, and select **OK** to close the form.  

## View service request details

You can use the following procedure to view the details of a service request in the Service Manager console in System Center - Service Manager.  

1. In the Service Manager console, expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Assigned To Me**.  
2. In the list, select a service request to view, and then in the **Tasks** pane under **\<Service Request ID - Service Request Name\>**, select **Edit**. For example, select **Request Membership to Active Directory Group**.  
3. Review information in service request form, and select **OK** to close the form.  

## Duplicate or hide views for service requests

You can use the following procedures to duplicate or hide a service request view in the Service Manager console in Service Manager. You can use the **Unhide** task if you want to show the hidden view. You can modify the title or other view criteria using the **Edit View** task.  

### Duplicate a service request view  

1. In the Service Manager console, expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode. For example, select **Assigned To Me**.  

2. In the **Tasks** pane, select **Duplicate View**.  

3. In the **Select management pack** dialog, select a management pack to add the new view information to or create a new one, and select **OK**.  

4. Optionally, you can use the **Edit View** task to edit the new view, titled **&lt;View Name - Copy&gt;**, to change the view name or other criteria of the view.  

5. In the **Work Items** pane, locate the new duplicate view that was created. For example, select **Assigned To Me - Copy**.  

6. In the **Tasks** pane, select **Edit View**.  

7. In the **Edit Assigned To Me -Copy** dialog, select **Criteria**.  

8. In the **Criteria** area, next to **Assigned To User ID**, in the text box after **equals**, enter **[me]**, and select **OK**.  

### Hide a service request view  

1. In the Service Manager console, expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Closed Service Requests**.  

2. In the **Tasks** pane, select **Hide View**.  

## Next steps

- To help automate the process of updating the status of change requests and the status propagation between parallel activities, sequential activities, and the activities within them, see [Manage release records](release-records.md).
