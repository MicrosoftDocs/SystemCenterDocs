---
title: How to Edit a Service Offering or a Request Offering
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd49432f-f22c-4366-8cfd-16d301a6a46c
---
# How to Edit a Service Offering or a Request Offering

>Applies To: System Center 2016 Technical Preview - Service Manager

Request offerings are catalog items that describe the item, assistance, or action that is available to end users in the service catalog. Request offerings are normally placed in logical groups of service offerings. Both service offerings and their request offerings are available to Self-Service Portal users, when the status of the offerings is set to Published and if end users have been assigned a corresponding Service Manager user role. Only users that have been assigned a user role that is associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog.

You can use the following procedures to edit a service offering or a request offering.

### To edit a request offering

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, expand **Request Offerings**, and then select **All Request Offerings**.

3.  In the **All Request Offerings** list, double-click the request offering that you want to edit.

4.  In the **Edit Request Offering** form, you can edit information on the following pages:

5.  On the **General** page, complete these steps:

    1.  In the **Title** box, type a title for the request offering. For example, type **Access to Active Directory group**.

    2.  Optionally, next to **Image**, you can either click **Browse** to find an image file or leave the default selection.

    3.  In the **Description** text box, type a short description that will describe the request offering that will appear on the Self-Service Portal page. For example, type **Use this request offering to request membership to an Active Directory Group**.

6.  On the **User Prompts** page, enter questions for users or define other instructions that will appear on the Self-Service Portal when a user submits a request by completing the following steps:

    1.  In the **Form instructions** box, type a summary of the information that the user must provide for the request. For example, type **Provide the information below to request membership to the Active Directory Group**

    2.  Under **Enter prompts or information text**, click **Add**; in the **User Prompts or Information** box, type **Enter your cost center**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Integer**.

    3.  In the second **Enter Prompts or Information** box, type **Select the list of Active Directory groups that you need access to**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Query Results**.

    4.  In the third **Enter Prompts or Information** box, type **Enter your justification for this request**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Text**.

7.  On the **Configure Prompts** page, configure prompts to constrain user input to ensure that users provide the information necessary to fulfill their request by completing the following steps:

    1.  Select the **Enter your cost center** prompt, and then click **Configure**.

    2.  In the **Configure Integer Control** dialog box, select **Limit integer range**, set the **Minimum Value** to **1000**, set the **Maximum Value** to **6999**, and then click **OK** to close the dialog box.

    3.  Select the **Select the Active Directory groups that you want access to** prompt, and click **Configure** to open the **Configure Instance Picker** dialog box.

    4.  In the **Configure Instance Picker** dialog box in the **Frequently user basic classes** list, select **All basic classes**; in the filter box, type **Active**; and then select **Active Directory Group**.

    5.  Click the **Configure Criteria (optional)** tab; in the list of properties under **User**, select **Department**; and then click **Add Constraint**.

    6.  In the **Criteria** box, click **Department equals**; in the **Set Token** list, click **Select token**; and then click **1. Enter your cost center: Integer**.

    7.  If the condition is not set to **equals**, select **equals**.

    8.  Click the **Display Columns** tab, and then select **Display Name**, **Department**, and **Last Name**.

    9. Click the **Options** tab, select **Allow the user to select multiple objects**, select **Add user-selected objects as affected configuration items**, and then select **Add the requesting user to the list of Active Directory group in the impacted configuration items (Manual Activity)**.

    10. Click **Ok** to close the **Configure Instance Picker** dialog box.

8.  On the **Map Prompts** page, associate prompts with various fields of a service request or its activities, depending on the complexity of the form and the extension of the class that you have made. Complete the following steps to associate a justification with the review activity:

    1.  Select **Approval for the user requesting membership to the Active Directory group - (Review Activity)**.

    2.  Next to **Description**, select the box under **Prompt Output**, and then in the list, select **3**. Enter your justification: .

9. Optionally, on the **Knowledge Articles** page, you can select a knowledge article to associate with this request offering.

10. Optionally, on the **Publish** page, you can set publishing information.

11. Click **OK** to close the **Edit Request Offering** form.

### To edit a service offering

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, expand **Service Offerings**, and then select **All Service Offerings**.

3.  In the **All Service Offerings** list, double-click the service offering that you want to edit.

4.  In the **Edit Service Offering** form, edit information on the following pages.

5.  On the **General** page, complete these steps:

    1.  In the **Title** box, type a title for the service offering. For example, type **Access Services**.

    2.  Optionally, next to **Image**, you can either click **Browse** to find an image file, or leave the default selection.

    3.  In the **Category** list, select a category that will be the group for this service offering. For example, select **Access and Security**.

    4.  In the **Language** list, either leave the default selection or select a language.

    5.  In the **Overview** text box, type a short overview that will describe the service offering that will appear on the Self-Service Portal home page. For example, type **Access to AD Group, Access to Labs**.

    6.  In the description box, type a description that will appear on the service offering page on the Self-Service Portal.

6.  On the **Detailed Information** page, complete these steps:

    1.  In the **Service level agreement information** box, type a summary of the service level agreement (SLA) information. For example, type **The SLAs for these requests range from 1-2 business days.  For more information, click the link below.**

    2.  In the first **Link for additional information** box, type a hyperlink that users can click to view additional information about the SLA for this service offering.

    3.  In the **Cost information** box, type a summary of any costs associated with requests that will be grouped in this service offering.

    4.  In the second **Link for additional information** box, type a hyperlink that users can click to view additional information about any costs associated with requests that will be grouped in this service offering.

7.  Optionally, on the **Related Services** page, add related business services associated with the service offering.

8.  Optionally, on the **Knowledge Articles** page, add related knowledge articles associated with the service offering.

9. Optionally, on the **Request Offering** page, add related request offerings associated with the service offering.

10. On the  **Publish** page in the **Offering status** list, select **Published**, and then set the **Offering owner** to yourself.

11. Click **OK** to close the **Edit Service Offering** form.



