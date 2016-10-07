---
description: Describes how you can create a new service request template without using the default generic incident request template.
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Create Service Request Templates for New Request Offerings
ms.technology:  service-manager
ms.assetid:  78965a33-426c-4d7c-82f2-14f23e32fdc9
---

# How to Create Service Request Templates for New Request Offerings

>Applies To: System Center 2016 - Service Manager

By default, Service Manager includes a number of service request templates that are based on a generic incident template. By viewing the template, you can gain an understanding of the categories of information to collect and convey to end users as they submit requests through the Self-Service Portal. You can use the following procedure to create a new service request template without using the default generic incident request template.

### To create a service request template

1.  In the Service Manager console, select **Library**.

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
