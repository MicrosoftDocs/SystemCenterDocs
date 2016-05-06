---
title: How to Create Service Request Templates for New Request Offerings_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d76cea9b-5d61-471a-a05f-af1ef41874f8
---
# How to Create Service Request Templates for New Request Offerings_1
By default, [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] includes a number of service request templates that are based on a generic incident template. By viewing the template, you can gain an understanding of the categories of information to collect and convey to end users as they submit requests through the [!INCLUDE[smssp](../Token/smssp_md.md)]. You can use the following procedure to create a new service request template without using the default generic incident request template.

### To create a service request template

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], select **Library**.

2.  In the **Library** pane, click **Templates**, and then in the **Tasks** lists under **Templates**, click **Create Template**.

3.  In the **Create Template** dialog box, in the **Name** box, type a name for the template. For example, type **Request Membership to Group**.

4.  In the **Description** box, type a description for the template. For example, type **This template is used to request membership to a group**.

5.  Next to **Class**, click **Browse**, select **Service Request**, and then click **OK**.

6.  Click **OK** to close the **Create Template** dialog box and open the **Service Request Template** form in template mode.

7.  In the **Service Request Template** form, in the **Title** box, type **Request membership to Active Directory group**.

8.  In the **Description** box, type a description of the purpose of the form. For example, type **This template is used to request membership to an Active Directory group**.

9. In the **Urgency** list, select **Medium**, and in the **Priority** list, select **Medium**.

10. In the **Source** list, select **Portal**, and then click the **Activities** tab.

11. On the **Activities** tab, click the **Add** button to open the **Select Template** dialog box, where you will add an activity.

12. Select **Default Review Activity**, and then click **OK** to close the **Select Template** dialog box and open the **Review Activity Template** dialog box.

13. In the **Title** box, type a name for the review activity. For example, type **Approval for the user Requesting Membership to AD Group**.

14. Click **Add** to open the **Reviewer** dialog box and select a user who will approve requests for this service request, and then click **OK** to close the dialog box.

15. Click **OK** to close the **Review Activity Template** form.

16. Add another activity, and then select the **Default Manual Activity** template.

17. In the **Manual Activity Template** form, in the **Title** box, type a title for the manual activity. For example, type **Add the requesting user to list of Active Directory groups in the impacted configuration items**.

18. Next to **Activity Implementer**, select a user who is responsible for the activity, and then click **OK** to close the **Manual Activity Template** form.

19. Click **OK** to close the **Service Request Template** form.

## See Also
[Using the Service Catalog in System Center Technical Preview - Service Manager](../Topic/Using-the-Service-Catalog-in-System-Center-Technical-Preview---Service-Manager.md)

