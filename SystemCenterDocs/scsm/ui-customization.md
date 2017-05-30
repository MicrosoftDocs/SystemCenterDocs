---
title: User interface customization in Service Manager
description: Explains to customize how items are displayed in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: bd4ce7ab-9e8f-4f83-a04a-f4385c2ac6b0
---

# User interface customization in Service Manager

>Applies To: System Center 2016 - Service Manager

The sealed management packs in Service Manager contain, among other things, views, list items, and templates. Because these items are in a sealed management pack, they cannot be edited or changed. In Service Manager, you have the option of hiding views. You can duplicate list items and templates, saving the duplicates into an unsealed management pack, and because the duplicates are in an unsealed management pack, you can edit the properties of the list item or template using the Service Manager console.


## Customize a view
The **Failed Service Requests** view in Service Manager is in a sealed management pack. In this example, you will create a duplicate of this view, save it into an unsealed management pack, and then edit the new view by changing its name to **New Failed Service Requests**. You will finish this exercise by hiding the original Failed Service Requests view. As an administrator, you will still see the hidden view.

### To customize a view

1.  In the Service Manager console, click **Work Items**.

2.  In the **Work Items** pane, expand **Service Request Fulfillment**.

3.  Right-click **Failed Service Requests**, and then click **Duplicate View**.

4.  In the **Select management pack** dialog box, accept the default management pack, **Service Manager Service Request Configuration Library**, and then click **OK**.

5.  Right-click **Failed Service Requests - Copy**, and then click **Edit View**.

6.  In the Edit Failed Service Requests - Copy Wizard, in **Name**, type a new name for this view. For example, type **New Failed Service Requests**, and then click **OK**.

7.  Right-click **Failed Service Requests**, and then click **Hide View**.


## Customize a list item

The items in a list in a sealed management pack in Service Manager cannot be changed. In this example, you will add a list item (phone) to the **Service Request Source** list and save it into an unsealed management pack, and then edit the new view by changing its name to **New Failed Service Requests**. You will finish this exercise by hiding the original Failed Service Requests view. As an administrator, you will still see the hidden view.

### To customize a list item

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Lists**.

3.  In the **Lists** pane, click **Service Request Source**.

4.  In the **Tasks** pane, in the **Service Request Source** area, click **Properties**.

5.  In the **List Properties** dialog box, click **Add Item**.

6.  In the **Select management pack** dialog box, accept the default management pack, **Service Manager Service Request Configuration Library**, and then click **OK**.

7.  In the **List Properties** dialog box, click **List Value**.

8.  In the **Name** field, type **Phone**, and then click **OK**.

## Customize a template

Templates in a sealed management pack in Service Manager cannot be changed. In this example, you will create a copy of the Default Service Request Template and save the copy in an unsealed management pack. You will then start a Create Template Wizard for the copy you made.

### To customize a template

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Templates**.

3.  In the **Templates** pane, click **Default Service Request**.

4.  In the **Tasks** pane, under **Default Service Request**, click **Create a Copy**.

5.  In the **Select management pack** dialog box, accept the default management pack, **Service Manager Service Request Configuration Library**, and then click **OK**.

6.  In the **Templates** pane, click **Copy of Default**.

7.  In the **Tasks** pane, under **Copy of Default Service Request**, click **Properties**.

8.  In the **Create Template** dialog box, in the **Name** field, type a new name for this template, and then click **OK**.

9. Finish the steps in the Service Request Template Wizard to customize this template for your needs, and when you are finished, click **OK**.

## Next steps

- [Manage user roles](user-roles.md).
