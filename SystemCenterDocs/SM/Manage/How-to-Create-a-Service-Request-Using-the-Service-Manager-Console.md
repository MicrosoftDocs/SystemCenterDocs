---
title: How to Create a Service Request Using the Service Manager Console
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2081264-5175-41a4-a96c-283e2e9c23be
---
# How to Create a Service Request Using the Service Manager Console
End users often create service requests in [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] by accessing the service catalog from the [!INCLUDE[smssp](../../Token/smssp_md.md)] or by submitting email requests. However, you can use the following procedure to manually create a new service request in the [!INCLUDE[smcons](../../Token/smcons_md.md)]. For example, you might want to manually create a new service request if a user contacts the help desk by telephone. In the following example, you can update any information that you want to as you complete the form.

### To create a new service request using the [!INCLUDE[smcons](../../Token/smcons_md.md)]

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Assigned To Me**.

2.  In the **Tasks** pane under **Service Request Fulfillment**, click **Create Service Request from Template**.

3.  Under **Templates** in the **Select Template** dialog box, select a template, and then click **OK** to open a new service request and apply the template. For example, select **Request Membership to Group**.

4.  In the **<SR<ID>: ServiceRequestName>** form in the **Affected user** box, select the user who submitted the service request. For example, select **Joe Andreshak**.

5.  Optionally, in the **Alternate Contact Method** box, enter additional contact information for the affected user.

6.  In the **Title** box, type a title for the service request or update one if it has been populated by a template. For example, type **Request Membership to Active Directory Group – Joe Andreshak**.

7.  In the **Description** box, enter a description for this service request.

8.  In the **Urgency** and **Priority** lists, select one for each if they have not been populated by a template.

9. In the **Source** list, select **Portal** if it has not been populated by a template.

10. In the **Assigned to** box, choose an analyst to assign the service request to. For example, assign the service request to yourself.

11. Click **OK** to save and close the service request form.

## See Also
[Managing Service Requests in Service Manager](Managing-Service-Requests-in-Service-Manager.md)


