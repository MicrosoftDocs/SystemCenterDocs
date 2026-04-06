---
title: Use the service catalog
description: You can use the Service Manager service catalog to offer your organization's services to end users.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: 37c13875-a46b-4387-b35a-5d2c8f511f56
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Use the Service Manager service catalog to offer services

This article provides an overview of how to use the service catalog in Service Manager. This article also contains procedures that cover management configuration scenarios for the service catalog.

The service catalog is a collection of items, assistance, actions, or groupings of them that your IT staff and infrastructure provides and makes available to end-users in the Self-Service Portal in Service Manager. In the Service Manager console, you create catalog items to describe these items in the Library workspace using the following nodes:

- Request Offerings

- Service Offerings

The Request Offerings node is used to create a catalog item that describes an item, assistance, or action that is available to end-users. It also defines information that you want to prompt the users for and any knowledge articles that are associated with the offering.

After it's created, you can set the status of a request offering as either Draft or Published. Draft status indicates that a request offering isn't published and available to the service catalog. This prevents end-users from requesting the offering. When you set the request offering status to Published, it appears in the catalog where users can request it if they've been granted access to a catalog item group that contains the request offering.

The Service Offerings node is used to create a catalog item that categorizes request offerings.

## Create your own service offering categories

By default, Service Manager includes only the General service offering category. However, your organization will likely need additional categories to help organize service offerings that are provided to end-users through the service catalog. You can use the following procedure to add additional categories to the service catalog.

### Extend the service offering categories

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, select **Lists**, and then in the **Filter** box, enter **offering**.
3. In the **Lists** view, select **Service Offering Category**, and then in the **Tasks** list under **Service Offering Category**, select **Properties**.
4. In the **List Properties** dialog, add any service offering categories that you want, and select **OK** to close the dialog. For example, add the following categories:
    - **Data Center**
    - **Access and Security**
    - **Communication Services**
5. Select **OK** to close the **List Properties** dialog.

## Create a service offering

Service offerings are logical groups of request offerings. Both service offerings and their request offerings are available to Self-Service Portal users when their status is set to Published and if end-users have been assigned a corresponding Service Manager user role. Only users who have been assigned a user role that is associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog.

### Create a service offering

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Service Offerings**.
3. In the **Tasks** pane under **Service Offerings**, select **Create Service Offering** to open the Create Service Offering Wizard.
4. On the **Before You Begin** page, read the instructions, and select **Next**.
5. On the **General** page, complete these steps:
    1. In the **Title** box, enter a title for the service offering. For example, enter **Access Services**.
    2. Optionally, next to **Image**, you can either **Browse** to an image file or leave the default selection.
    3. In the **Category** list, select a category that this service offering will be a part of. For example, select **Access and Security**.
    4. In the **Language** list, either leave the default selection or select a language.
    5. In the **Overview** text box, enter a short overview to describe the service offering that will be shown on the Self-Service Portal home page. For example, enter **Access to AD Group, Access to Labs**.
    6. In the description box, enter a description that will appear on the service offering page in the Self-Service Portal.
    7. Next to the **Management pack**, select an unsealed management pack of your choice, and select **Next**. For example, if you previously created the Sample Management Pack, select it.
6. On the **Detailed Information** page, complete these steps:
    1. In the **Service level agreement information** box, enter a summary of the service level agreement (SLA) information. For example, enter **The SLAs for these requests, depending on the criticality of the requests, range from 1-2 business days. For more information, click the link below.**
    2. In the first **Link for additional information** box, enter a hyperlink that users can select to view additional information about the SLA for this service offering.
    3. In the **Cost information** box, enter a summary of any costs associated with requests that will be grouped in this service offering.
    4. In the second **Link for additional information** box, enter a hyperlink that users can select to view additional information about any costs associated with requests that will be grouped in this service offering.
    5. Select **Next**.
7. Optionally, on the **Related Services** page, add related business services associated with the service offering, and select **Next**.
8. Optionally, on the **Knowledge Articles** page, add related knowledge articles associated with the service offering, and select **Next**.
9. Optionally, on the **Request Offering** page, add related request offerings associated with the service offering, and select **Next**.
10. On **the Publish** page, in the **Offering status** list, select **Published** and set the **Offering owner** to yourself, and select **Next**.
11. On the **Summary** page, review the information, and select **Create**.
12. On the **Completion** page, select **Close**.

## Create service request templates for new request offerings

By default, Service Manager includes a number of service request templates that are based on a generic incident template. By viewing the template, you can gain an understanding of the categories of information to collect and convey to end-users as they submit requests through the Self-Service Portal. You can use the following procedure to create a new service request template without using the default generic incident request template.

### Create a service request template

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, select **Templates**, and then in the **Tasks** lists under **Templates**, select **Create Template**.
3. In the **Create Template** dialog, in the **Name** box, enter a name for the template. For example, enter **Request Membership to Group**.
4. In the **Description** box, enter a description for the template. For example, enter **This template is used to request membership to a group**.
5. Next to **Class**, select **Browse**, select **Service Request**, and select **OK**.
6. Select **OK** to close the **Create Template** dialog and open the **Service Request Template** form in template mode.
7. In the **Service Request Template** form, in the **Title** box, enter **Request membership to Active Directory group**.
8. In the **Description** box, enter a description of the purpose of the form. For example, enter **This template is used to request membership to an Active Directory group**.
9. In the **Urgency** list, select **Medium**, and in the **Priority** list, select **Medium**.
10. In the **Source** list, select **Portal**, and select the **Activities** tab.
11. On the **Activities** tab, select the **Add** button to open the **Select Template** dialog, where you will add an activity.
12. Select **Default Review Activity**, and select **OK** to close the **Select Template** dialog and open the **Review Activity Template** dialog.
13. In the **Title** box, enter a name for the review activity. For example, enter **Approval for the user Requesting Membership to AD Group**.
14. Select **Add** to open the **Reviewer** dialog and select a user who will approve requests for this service request, and select **OK** to close the dialog.
15. Select **OK** to close the **Review Activity Template** form.
16. Add another activity, and then select the **Default Manual Activity** template.
17. In the **Manual Activity Template** form, in the **Title** box, enter a title for the manual activity. For example, enter **Add the requesting user to list of Active Directory groups in the impacted configuration items**.
18. Next to **Activity Implementer**, select a user who is responsible for the activity, and select **OK** to close the **Manual Activity Template** form.
19. Select **OK** to close the **Service Request Template** form.

## Create a request offering

Request offerings are catalog items that describe the item, assistance, or action that is available to end-users in the service catalog. Request offerings are normally placed in logical groups of service offerings. Both service offerings and their request offerings are available to Self-Service Portal users when the status of the offerings is set to Published and if end-users have been assigned a corresponding Service Manager user role. Only users who have been assigned a user role associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog.

To create a request offering, follow these steps:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Request Offerings**.
3. In the **Tasks** pane under **Request Offerings**, select **Create Request Offering** to open the Create Request Offering Wizard.
4. On the **Before You Begin** page, read the instructions, and select **Next**.
5. On the **General** page, complete these steps:
    1. In the **Title** box, enter a title for the request offering. For example, enter **Access to Active Directory group**.
    2. Optionally, next to **Image**, you can either **Browse** to an image file, or leave the default selection.
    3. In the **Description** text box, enter a short description that describes the request offering that will appear on the Self-Service Portal page. For example, enter **Use this request offering to request membership to an Active Directory Group**.
    4. Under **Select template**, select **Service Request**, and then in the **Select Template** dialog, select a template that you created previously for a service request. For example, select the **Request Membership to Group** template, and select **OK**.
    5. Next to **Management pack**, select an unsealed management pack of your choice, and select **Next**. For example, if you previously created the Sample Management Pack, select it.
6. On the **User Prompts** page, enter questions for users or define other instructions, which will appear in the Self-Service Portal when a user submits a request by completing the following steps:
    1. In the **Form instructions** box, enter a summary of the information that the user must provide for the request. For example, enter **Provide the information below to request membership to the Active Directory Group**
    2. Under **Enter prompts or information text**, select **Add**; in the **User Prompts or Information** box, enter **Enter your cost center**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Integer**.
    3. In the second **Enter Prompts or Information** box, enter **Select the list of Active Directory groups that you need access to**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Query Results**.
    4. In the third **Enter Prompts or Information** box, enter **Enter your justification for this request**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Text**.
    5. Select **Next**.
7. On the **Configure Prompts** page, configure prompts to constrain user input to ensure that users provide the information required to fulfill their requests by completing the following steps:
    1. Select the **Enter your cost center** prompt, and select **Configure**.
    2. In the **Configure Integer Control** dialog, select **Limit integer range**, set the **Minimum Value** to **1000** set the **Maximum Value** to **6999**, and select **OK** to close the dialog.
    3. Select the **Select the Active Directory groups that you want access to** prompt, and select **Configure** to open the **Configure Instance Picker** dialog.
    4. In the **Configure Instance Picker** dialog in the **Frequently used basic classes** list, select **All basic classes**; in the filter box, enter **Active**; and then select **Active Directory Group**.
    5. Select the **Configure Criteria (optional)** tab; in the list of properties under **User**, select **Department**; and select **Add Constraint**.
    6. In the **Criteria** box, select **Department equals**; in the **Set Token** list, select **Select token**; and select **1. Enter your cost center: Integer**.
    7. If the condition is not set to **equals**, select **equals**.
    8. Select the **Display Columns** tab, and then select **Display Name**, **Department**, and **Last Name**.
    9. Select the **Options** tab, select **Allow the user to select multiple objects**, and then select **Add user-selected objects as affected configuration items**.
    10. Select **Ok** to close the **Configure Instance Picker** dialog, and select **Next**.
8. On the **Map Prompts** page, associate prompts with various fields of a service request or its activities, depending on the complexity of the form and the extension of the class that you've made. Complete the following steps to associate the justification to the review activity:
    1. Select **Approval for the user requesting membership to the Active Directory group - (Review Activity)**.
    2. Next to **Description**, select the box under **Prompt Output**, and then in the list, select **3. Enter your justification: String**.
    3. Select **Next**.
9. Optionally, on the **Knowledge Articles** page, you can select a knowledge article to associate with this request offering, and select **Next**.
10. Optionally, on the **Publish** page, you can set publishing information, and select **Next**.
11. On the **Summary** page, review the information, and select **Create**.
12. On the **Completion** page, select **Close**.

## Publish a request offering

You can publish draft request offerings by using the Publish task or by using a change request. When you publish a request offering by using the Publish task, no additional interaction is required, and the request offering appears in the Self-Service Portal as an uncategorized item. If you want to publish the request offering as part of a category, you must add the request offering to a service offering.

If you want to have an approval process added before publishing, you can associate the request offering to a change request. If you use a change request, you can also send email notifications as the approval process occurs.

> [!NOTE]
> Various errors might occur if you create a request offering without mapped prompts or if you've erroneously mapped any prompts. The errors can occur after you associate a change request to the request offering and then you complete the change request. To avoid such errors, ensure that you've at least one prompt in the request offering and that all the prompts are mapped correctly.

You can use the following procedures to publish request offerings.

### Publish draft request offerings

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Draft Request Offerings**.
3. In the **Draft Request Offerings** list, select one or more request offerings, and in the **Tasks** pane under *RequestOfferingName*, select **Publish**.

### Use a change request to publish draft request offerings

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Draft Request Offerings**.
3. In the **Draft Request Offerings** list, select one or more request offerings, and in the **Tasks** pane under *RequestOfferingName*, select **Create Change Request to Publish**.
4. In the **Select Template** dialog, select the **Publish Offering** change request template, and select **OK** to open a new change request form.
5. In the *ChangeRequestID: Publish Offerings* form, notice that the catalog items to publish appear under **Catalog items**.
6. Select the **Activities** tab, and notice that there is a review activity and an automated activity associated with the change request. Later, when the review activity is approved, the automated activity will set the publish status to Published.
7. Select **OK** to save the change request.

## Add request offerings to service offerings

Service offerings are logical groups of request offerings. For a service offering to appear in the Self-Service Portal, each service offering must have at least one request offering added to it. After a service offering and a request offering are published, it's a straightforward process to associate them as a collection.

To add request offerings to service offerings, follow these steps:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Published Request Offerings**.
3. In the **Published Request Offerings** list, select one or more request offerings, and in the **Tasks** pane under **RequestOfferingName**, select **Add to Service Offering**.
4. In the **Select objects** dialog, select the service offering that you want to associate the request offering with, select **Add**, and select **OK** to close the dialog.

## Create a catalog item group

Catalog item groups are lists of catalog items that are used to secure the service catalog and provide access to users based on membership in a corresponding Service Manager user role. In the following procedure, you create a simple catalog item group. After you create the group, use an existing user role, or create a new user role, to provide access to catalog items that have been associated with the group.

To create a catalog item group, follow these steps:

1. In the Service Manager console, select **Library**, and select **Groups**.
2. In the **Tasks** pane under **Groups**, select **Create Catalog Group** to open the Create Group Wizard.
3. On the **Before You Begin** page, read the instructions, and select **Next**.
4. On the **General** page, complete these steps:
    1. In the **Group name** box, enter a name for the catalog group. For example, enter **Access Request Offering Group**.
    2. In the **Group description** box, enter a description for the catalog group. For example, enter **This group is used to consolidate and provide security to Access Request Offering catalog items**.
    3. Next to **Management pack**, select an unsealed management pack of your choice, and select **Next**. For example, if you previously created the Sample Management Pack, select it.
5. On the **Included Members** page, complete these steps to select catalog items and associate them with the catalog group:
    1. Select **Add** to open the **Select objects** dialog, select one or more catalog items that you created previously, select **Add**, and select **OK** to close the dialog.
    2. Select **Next**.
6. Optionally, on the **Dynamic Members** page, you can select a class and specific objects, based on the criteria that you choose, to add as members of the group, and select **Next**.
7. Optionally, on the **Subgroups** page, you can add other groups as members of the new group that you're creating, and select **Next**.
8. Optionally, on the **Excluded Members** page, you can select a class and specific objects, based on criteria that you choose, to exclude as members of the group, and select **Next**.
9. On the **Summary** page, review the information, and select **Create**.
10. On the **Completion** page, select **Close**.

## Specify a user role for catalog items

User roles provide access to catalog groups that contain catalog items. Both service offerings and their request offerings are available to Self-Service Portal users, when the status of the offerings is set to Published and if end-users have been assigned a corresponding Service Manager user role. Only users who have been assigned a user role associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog. You can use the following procedure to create a user role and associate catalog items and users with the role.

### Create a user role and associate it with catalog items and users

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Security**, and then select **User Roles**.
3. In the **Tasks** pane under **User Roles**, select **Create User Role**, and select **End User** to open the Create User Role Wizard.
4. On the **Before You Begin** page, read the instructions, and select **Next**.
5. On the **General** page, complete these steps:
    1. In the **Name** box, enter a name for the user role. For example, enter **Security Offerings End User Role**.
    2. Optionally, in the **Description** box, enter a description of the purpose of the user role. For example, enter **This user role provides access to security offerings to end users**.
    3. Select **Next**.
6. On the **Management Packs** page, complete these steps:
    1. In **Management Packs** list, select a management pack that is used by catalog items. For example, select **Service Manager Service Request Configuration Library**.
    2. Select **Next**.
7. On the **Queues** page, there are no options that apply to security to catalog items; therefore, select **Next**.
8. On the **Configuration Item Groups** page, there are no options that apply to security to catalog items; therefore, select **Next**.
9. On the **Catalog Item Groups** page, select **Provide access to only the selected groups**, select the groups that you want to provide access to, and select **Next**.
10. On the **Form Templates** page, ensure that **All forms can be accessed** is selected, and select **Next**.
11. On the **Users** page, add the users and groups that you want to provide access to, and select **Next**.
12. On the **Summary** page, review the information, and select **Create**.
13. On the **Completion** page, select **Close**.

## Copy request offerings and service offerings

After you create a request offering or a service offering, you can copy the offering so that you can easily modify the copied offering.

You can use the following procedures to copy a request offering and a service offering. Keep in mind that if you copy a published catalog item, the published status of the copy is set to Draft.

Select the required tab for steps to copy a request or service offering:

# [Copy a request offering](#tab/CopyRequestOffering)

Follow these steps to copy a request offering:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, expand **Request Offerings**, and then select **All Request Offerings**.
3. In the **All Request Offerings** list, select the request offering that you want to copy, and then in the **Tasks** pane under *RequestOfferingName*, select **Create a Copy** to open the **Copy Request Offering** dialog.
4. In the dialog, you can optionally select **Also create a copy of the template referred to in this Request Offering** to create a copy of the template.
5. Optionally, you can change the management pack where information about the copied request offering is stored or you can create a new management pack.
6. Select **OK** to close the dialog and create the copy.
7. The copied item appears in the list, with a prefix of **Copy of**. For example, your copy might have the name **Copy of Access to Active Directory Group**.

# [Copy a service offering](#tab/CopyServiceOffering)

Follow these steps to copy a service offering:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, expand **Service Offerings**, and then select **All Service Offerings**.
3. In the **All Service Offerings** list, select the service offering that you want to copy, and then in the **Tasks** pane under *ServiceOfferingName*, select **Create a Copy** to open the **Copy Service Offering** dialog.
4. Optionally, you can change the management pack where information about the copied service offering is stored or you can create a new management pack.
5. Select **OK** to close the dialog and create the copy.
6. The copied item appears in the list, with a prefix of **Copy of**. For example, your copy might have the name **Copy of Access Services**.

---

## Publish a service offering

You can publish draft service offerings by using the Publish task or by using a change request. When you publish a service offering by using the Publish task, the service offing must contain at least one published request offering before it appears in the Self-Service Portal. If you want to have an approval process added before publishing, you can associate the service offering with a change request. If you use a change request, you can also send email notifications as the approval process occurs.

To publish a draft service offering, follow these steps:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Draft Service Offerings**.
3. In the **Draft Service Offerings** list, select one or more service offerings, and in the **Tasks** pane under *ServiceOfferingName*, select **Publish**.

### Use a change request to publish a draft service offering

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, and then select **Draft Service Offerings**.
3. In the **Draft Service Offerings** list, select one or more service offerings, and in the **Tasks** pane under *ServiceOfferingName*, select **Create Change Request to Publish**.
4. In the **Select Template** dialog, select the **Publish Offering** change request template, and select **OK** to open a new change request form.
5. In the *ChangeRequestID: Publish Offerings* form, notice that the catalog items to be published appear under **Catalog items**.
6. Select the **Activities** tab, and notice that there's a review activity and an automated activity associated with the change request. Later, when the review activity is approved, the automated activity will set the publish status to Published.
7. Select **OK** to save the change request.

## Edit a service offering or a request offering

Request offerings are catalog items that describe the item, assistance, or action that is available to end-users in the service catalog. Request offerings are normally placed in logical groups of service offerings. Both service offerings and their request offerings are available to Self-Service Portal users, when the status of the offerings is set to Published and if end-users have been assigned a corresponding Service Manager user role. Only users that have been assigned a user role that is associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog.

You can use the following procedures to edit a service offering or a request offering.

# [Edit a request offering](#tab/EditRequestOffering)

Follow these steps to edit a request offering:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, expand **Request Offerings**, and then select **All Request Offerings**.
3. In the **All Request Offerings** list, double-click the request offering that you want to edit.
4. In the **Edit Request Offering** form, you can edit information on the following pages:
5. On the **General** page, complete these steps:
    1. In the **Title** box, enter a title for the request offering. For example, enter **Access to Active Directory group**.
    2. Optionally, next to **Image**, you can either select **Browse** to find an image file or leave the default selection.
    3. In the **Description** text box, enter a short description that will describe the request offering that will appear on the Self-Service Portal page. For example, enter **Use this request offering to request membership to an Active Directory Group**.
6. On the **User Prompts** page, enter questions for users or define other instructions that will appear on the Self-Service Portal when a user submits a request by completing the following steps:
    1. In the **Form instructions** box, enter a summary of the information that the user must provide for the request. For example, enter **Provide the information below to request membership to the Active Directory Group**
    2. Under **Enter prompts or information text**, select **Add**; in the **User Prompts or Information** box, enter **Enter your cost center**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Integer**.
    3. In the second **Enter Prompts or Information** box, enter **Select the list of Active Directory groups that you need access to**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Query Results**.
    4. In the third **Enter Prompts or Information** box, enter **Enter your justification for this request**; in the **Response Type** list, select **Required**; and in the **Prompt Type** list, select **Text**.
7. On the **Configure Prompts** page, configure prompts to constrain user input to ensure that users provide the information necessary to fulfill their request by completing the following steps:
    1. Select the **Enter your cost center** prompt, and select **Configure**.
    2. In the **Configure Integer Control** dialog, select **Limit integer range**, set the **Minimum Value** to **1000**, set the **Maximum Value** to **6999**, and select **OK** to close the dialog.
    3. Select the **Select the Active Directory groups that you want access to** prompt, and select **Configure** to open the **Configure Instance Picker** dialog.
    4. In the **Configure Instance Picker** dialog in the **Frequently user basic classes** list, select **All basic classes**; in the filter box, enter **Active**; and then select **Active Directory Group**.
    5. Select the **Configure Criteria (optional)** tab; in the list of properties under **User**, select **Department**; and select **Add Constraint**.
    6. In the **Criteria** box, select **Department equals**; in the **Set Token** list, select **Select token**; and select **1. Enter your cost center: Integer**.
    7. If the condition is not set to **equals**, select **equals**.
    8. Select the **Display Columns** tab, and then select **Display Name**, **Department**, and **Last Name**.
    9. Select the **Options** tab, select **Allow the user to select multiple objects**, select **Add user-selected objects as affected configuration items**, and then select **Add the requesting user to the list of Active Directory group in the impacted configuration items (Manual Activity)**.
    10. Select **Ok** to close the **Configure Instance Picker** dialog.
8. On the **Map Prompts** page, associate prompts with various fields of a service request or its activities, depending on the complexity of the form and the extension of the class that you have made. Complete the following steps to associate a justification with the review activity:
    1. Select **Approval for the user requesting membership to the Active Directory group - (Review Activity)**.
    2. Next to **Description**, select the box under **Prompt Output**, and then in the list, select **3**. Enter your justification: .
9. Optionally, on the **Knowledge Articles** page, you can select a knowledge article to associate with this request offering.
10. Optionally, on the **Publish** page, you can set publishing information.
11. Select **OK** to close the **Edit Request Offering** form.

# [Edit a service offering](#tab/EditServiceOffering)

Follow these steps to edit a service offering:

1. In the Service Manager console, select **Library**.
2. In the **Library** pane, expand **Service Catalog**, expand **Service Offerings**, and then select **All Service Offerings**.
3. In the **All Service Offerings** list, double-click the service offering that you want to edit.
4. In the **Edit Service Offering** form, edit information on the following pages.
5. On the **General** page, complete these steps:
    1. In the **Title** box, enter a title for the service offering. For example, enter **Access Services**.
    2. Optionally, next to **Image**, you can either select **Browse** to find an image file, or leave the default selection.
    3. In the **Category** list, select a category that will be the group for this service offering. For example, select **Access and Security**.
    4. In the **Language** list, either leave the default selection or select a language.
    5. In the **Overview** text box, enter a short overview that will describe the service offering that will appear on the Self-Service Portal home page. For example, enter **Access to AD Group, Access to Labs**.
    6. In the description box, enter a description that will appear on the service offering page on the Self-Service Portal.
6. On the **Detailed Information** page, complete these steps:
    1. In the **Service level agreement information** box, enter a summary of the service level agreement (SLA) information. For example, enter **The SLAs for these requests range from 1-2 business days.  For more information, click the link below.**
    2. In the first **Link for additional information** box, enter a hyperlink that users can select to view additional information about the SLA for this service offering.
    3. In the **Cost information** box, enter a summary of any costs associated with requests that will be grouped in this service offering.
    4. In the second **Link for additional information** box, enter a hyperlink that users can select to view additional information about any costs associated with requests that will be grouped in this service offering.
7. Optionally, on the **Related Services** page, add related business services associated with the service offering.
8. Optionally, on the **Knowledge Articles** page, add related knowledge articles associated with the service offering.
9. Optionally, on the **Request Offering** page, add related request offerings associated with the service offering.
10. On the  **Publish** page in the **Offering status** list, select **Published**, and then set the **Offering owner** to yourself.
11. Select **OK** to close the **Edit Service Offering** form.

---

## Next steps

[Use groups, queues, and lists in Service Manager](group-queue-lists.md).
