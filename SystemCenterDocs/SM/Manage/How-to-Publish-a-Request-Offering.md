---
title: How to Publish a Request Offering
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0c1088f-92a8-40ba-93ec-edf6bd8b5fb3
---
# How to Publish a Request Offering
You can publish draft request offerings by using the Publish task or by using a change request. When you publish a request offering by using the Publish task, no additional interaction is required, and the request offering appears in the [!INCLUDE[smssp](../../includes/smssp_md.md)] as an uncategorized item. If you want to publish the request offering as part of a category, you must add the request offering to a service offering.

If you want to have an approval process added before publishing, you can associate the request offering to a change request. If you use a change request, you can also send email notifications as the approval process occurs.

> [!NOTE]
> Various errors might occur if you create a request offering without mapped prompts or if you have erroneously mapped any prompts. The errors can occur after you associate a change request to the request offering and then you complete the change request. To avoid such errors, ensure that you have least one prompt in the request offering and that all prompts are mapped correctly.

You can use the following procedures to publish request offerings.

### To publish draft request offerings

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Draft Request Offerings**.

3.  In the **Draft Request Offerings** list, select one or more request offerings, and in the **Tasks** pane under **\<RequestOfferingName\>**, click **Publish**.

### To use a change request to publish draft request offerings

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Draft Request Offerings**.

3.  In the **Draft Request Offerings** list, select one or more request offerings, and in the **Tasks** pane under **\<RequestOfferingName\>**, click **Create Change Request to Publish**.

4.  In the **Select Template** dialog box, select the **Publish Offering** change request template, and then click **OK** to open a new change request form.

5.  In the **\<ChangeRequestID: Publish Offerings\>** form, notice that the catalog items to publish appear under **Catalog items**.

6.  Click the **Activities** tab, and notice that there is a review activity and an automated activity associated with the change request. Later, when the review activity is approved, the automated activity will set the publish status to Published.

7.  Click **OK** to save the change request.


