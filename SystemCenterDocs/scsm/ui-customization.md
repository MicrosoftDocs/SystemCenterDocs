---
title: User Interface Customization in Service Manager
description: Explains to customize how items are displayed in Service Manager.
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 04/15/2025
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.assetid: bd4ce7ab-9e8f-4f83-a04a-f4385c2ac6b0
ms.custom: UpdateFrequency3, engagement-fy24
---

# User interface customization in Service Manager



The sealed management packs in Service Manager contain, among other things, views, list items, and templates. Because these items are in a sealed management pack, they can't be edited or changed. In Service Manager, you've the option of hiding views. You can duplicate list items and templates, saving the duplicates into an unsealed management pack, and because the duplicates are in an unsealed management pack, you can edit the properties of the list item or template using the Service Manager console.

## Customize a view

The **Failed Service Requests** view in Service Manager is in a sealed management pack. In this example, you will create a duplicate of this view, save it into an unsealed management pack, and then edit the new view by changing its name to **New Failed Service Requests**. You will finish this exercise by hiding the original Failed Service Requests view. As an administrator, you will still see the hidden view.

To customize a view, follow these steps:

1. In the Service Manager console, select **Work Items**.

2. In the **Work Items** pane, expand **Service Request Fulfillment**.

3. Right-click **Failed Service Requests**, and select **Duplicate View**.

4. In the **Select management pack** dialog, accept the default management pack, **Service Manager Service Request Configuration Library**, and select **OK**.

5. Right-click **Failed Service Requests - Copy**, and select **Edit View**.

6. In the Edit Failed Service Requests - Copy Wizard, in **Name**, enter a new name for this view. For example, enter **New Failed Service Requests**, and select **OK**.

7. Right-click **Failed Service Requests**, and select **Hide View**.

## Customize a list item

The items in a list in a sealed management pack in Service Manager can't be changed. In this example, you'll add a list item (phone) to the **Service Request Source** list and save it into an unsealed management pack, and then edit the new view by changing its name to **New Failed Service Requests**. You will finish this exercise by hiding the original Failed Service Requests view. As an administrator, you will still see the hidden view.

To customize a list item, follow these steps:

1. In the Service Manager console, select **Library**.

2. In the **Library** pane, expand **Library**, and select **Lists**.

3. In the **Lists** pane, select **Service Request Source**.

4. In the **Tasks** pane, in the **Service Request Source** area, select **Properties**.

5. In the **List Properties** dialog, select **Add Item**.

6. In the **Select management pack** dialog, accept the default management pack, **Service Manager Service Request Configuration Library**, and select **OK**.

7. In the **List Properties** dialog, select **List Value**.

8. In the **Name** field, enter **Phone**, and select **OK**.

## Customize a template

Templates in a sealed management pack in Service Manager can't be changed. In this example, you will create a copy of the Default Service Request Template and save the copy in an unsealed management pack. You will then start a Create Template Wizard for the copy you made.

To customize a template, follow these steps:

1. In the Service Manager console, select **Library**.

2. In the **Library** pane, expand **Library**, and select **Templates**.

3. In the **Templates** pane, select **Default Service Request**.

4. In the **Tasks** pane, under **Default Service Request**, select **Create a Copy**.

5. In the **Select management pack** dialog, accept the default management pack, **Service Manager Service Request Configuration Library**, and select **OK**.

6. In the **Templates** pane, select **Copy of Default**.

7. In the **Tasks** pane, under **Copy of Default Service Request**, select **Properties**.

8. In the **Create Template** dialog, in the **Name** field, enter a new name for this template, and select **OK**.

9. Finish the steps in the Service Request Template Wizard to customize this template for your needs, and when you're finished, select **OK**.

## Next steps

[Manage user roles](user-roles.md).
