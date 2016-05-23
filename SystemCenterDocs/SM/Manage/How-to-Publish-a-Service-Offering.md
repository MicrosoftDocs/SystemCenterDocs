---
title: How to Publish a Service Offering
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bcede83b-0c4c-4dbd-b943-d62bbcb1242e
---
# How to Publish a Service Offering
You can publish draft service offerings by using the Publish task or by using a change request. When you publish a service offering by using the Publish task, the service offing must contain at least one published request offering before it appears in the [!INCLUDE[smssp](../../Token/smssp_md.md)]. If you want to have an approval process added before publishing, you can associate the service offering with a change request. If you use a change request, you can also send email notifications as the approval process occurs.

You can use the following procedures to publish a draft service offering and then use a change request to publish it.

### To publish a draft service offering

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Draft Service Offerings**.

3.  In the **Draft Service Offerings** list, select one or more service offerings, and in the **Tasks** pane under **\<ServiceOfferingName\>**, click **Publish**.

### To use a change request to publish a draft service offering

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Draft Service Offerings**.

3.  In the **Draft Service Offerings** list, select one or more service offerings, and in the **Tasks** pane under **\<ServiceOfferingName\>**, click **Create Change Request to Publish**.

4.  In the **Select Template** dialog box, select the **Publish Offering** change request template, and then click **OK** to open a new change request form.

5.  In the **\<ChangeRequestID: Publish Offerings\>** form, notice that the catalog items to be published appear under **Catalog items**.

6.  Click the **Activities** tab, and notice that there is a review activity and an automated activity associated with the change request. Later, when the review activity is approved, the automated activity will set the publish status to Published.

7.  Click **OK** to save the change request.


