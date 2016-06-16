---
title: How to Create a Request Offering
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1137cb8c-abcb-4929-bf4b-f3a41db1bf2e
---
# How to Create a Request Offering
Request offerings are catalog items that describe the item, assistance, or action that is available to end users in the service catalog. Request offerings are normally placed in logical groups of service offerings. Both service offerings and their request offerings are available to [!INCLUDE[smssp](../../includes/smssp_md.md)] users when the status of the offerings is set to Published and if end users have been assigned a corresponding [!INCLUDE[smshort](../../includes/smshort_md.md)] user role. Only users who have been assigned a user role associated with a catalog group that contains catalog items can use the [!INCLUDE[smssp](../../includes/smssp_md.md)] to access the service catalog.

You can use the following procedure to create a request offering.

### To create a request offering

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Request Offerings**.

3.  In the **Tasks** pane under **Request Offerings**, click **Create Request Offering** to open the Create Request Offering Wizard.

4.  On the **Before You Begin** page, read the instructions, and then click **Next**.

5.  On the **General** page, complete these steps:

    1.  In the **Title** box, type a title for the request offering. For example, type **Access to Active Directory group**.

    2.  Optionally, next to **Image**, you can either **Browse** to an image file, or leave the default selection.

    3.  In the **Description** text box, type a short description that describes the request offering that will appear on the [!INCLUDE[smssp](../../includes/smssp_md.md)] page. For example, type **Use this request offering to request membership to an Active Directory Group**.

    4.  Under **Select template**, select **Service Request**, and then in the **Select Template** dialog box, select a template that you created previously for a service request. For example, select the **Request Membership to Group** template, and then click **OK**.

    5.  Next to **Management pack**, select an unsealed management pack of your choice, and then click **Next**. For example, if you previously created the Sample Management Pack, select it.

6.  On the **User Prompts** page, enter questions for users or define other instructions which will appear in the [!INCLUDE[smssp](../../includes/smssp_md.md)] when a user submits a request by completing the following steps:

    1.  In the **Form instructions** box, type a summary of the information that the user must provide for the request. For example, type **Provide the information below to request membership to the Active Directory Group**

    2.  Under **Enter prompts or information text**, click **Add**; in the **User Prompts or Information** box, type **Enter your cost center**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Integer**.

    3.  In the second **Enter Prompts or Information** box, type **Select the list of Active Directory groups that you need access to**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Query Results**.

    4.  In the third **Enter Prompts or Information** box, type **Enter your justification for this request**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Text**.

    5.  Click **Next**.

7.  On the **Configure Prompts** page, configure prompts to constrain user input to ensure that users provide the information required to fulfill their requests by completing the following steps:

    1.  Select the **Enter your cost center** prompt, and then click **Configure**.

    2.  In the **Configure Integer Control** dialog box, select **Limit integer range**, set the **Minimum Value** to **1000** set the **Maximum Value** to **6999**, and then click **OK** to close the dialog box.

    3.  Select the **Select the Active Directory groups that you want access to** prompt, and click **Configure** to open the **Configure Instance Picker** dialog box.

    4.  In the **Configure Instance Picker** dialog box in the **Frequently used basic classes** list, select **All basic classes**; in the filter box, type **Active**; and then select **Active Directory Group**.

    5.  Click the **Configure Criteria \(optional\)** tab; in the list of properties under **User**, select **Department**; and then click **Add Constraint**.

    6.  In the **Criteria** box, select **Department equals**; in the **Set Token** list, click **Select token**; and then click **1. Enter your cost center: Integer**.

    7.  If the condition is not set to **equals**, select **equals**.

    8.  Click the **Display Columns** tab, and then select **Display Name**, **Department**, and **Last Name**.

    9. Click the **Options** tab, select **Allow the user to select multiple objects**, and then select **Add user\-selected objects as affected configuration items**.

    10. Click **Ok** to close the **Configure Instance Picker** dialog box, and then click **Next**.

8.  On the **Map Prompts** page, associate prompts with various fields of a service request or its activities, depending on the complexity of the form and the extension of the class that you have made. Complete the following steps to associate the justification to the review activity:

    1.  Select **Approval for the user requesting membership to the Active Directory group – \(Review Activity\)**.

    2.  Next to **Description**, select the box under **Prompt Output**, and then in the list, select **3. Enter your justification: String**.

    3.  Click **Next**.

9. Optionally, on the **Knowledge Articles** page you can select a knowledge article to associate with this request offering, and then click **Next**.

10. Optionally, on the **Publish** page, you can set publishing information, and then click **Next**.

11. On the **Summary** page, review the information, and then click **Create**.

12. On the **Completion** page, click **Close**.


