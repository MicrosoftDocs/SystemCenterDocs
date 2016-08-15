---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Assign or Remove a Default Price Sheet for a Selected Cloud
ms.technology:  service-manager
ms.assetid:  8cc9a2b5-c265-4909-9d82-4e99346dd30f
---

# How to Assign or Remove a Default Price Sheet for a Selected Cloud

>Applies To: System Center 2016 Technical Preview - Service Manager

After Service Manager has discovered cloud objects from the Operations Manager CI connector, you can assign an existing price sheet that applies default price values to all the resources of the cloud. This process is useful when you have many virtual machines so that you do not have to define prices for all the individual virtual machine parts. Once the default price sheet is assigned to a cloud, you can override the default values, on a per-user basis. For more information about overriding default prices, see  [How to Override a Default Price Sheet for a Specific VMM User Role](How-to-Override-a-Default-Price-Sheet-for-a-Specific-VMM-User-Role.md).

### To assign a default price sheet to a selected cloud

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Chargeback**, expand **Clouds**, and then select **All Clouds**.

3.  In the list of clouds, select one that you want to assign a price sheet to and then under Tasks, click **Assign Price Sheet**.

4.  In *CloudName* form under **Default Cloud Price Sheet**, in the Action column, click **Assign Price Sheet**.

    > [!NOTE]
    > If a cloud previously had a price sheet assigned, then assigning a new one automatically unassigns the price sheet that was used previously.

5.  In the **Select objects** dialog box, select a price sheet that you want to assign and then click **OK**.

6.  Click **OK** to close the *CloudName* form.

    > [!NOTE]
    > If a cloud does not have a price sheet assigned, all virtual machines in the cloud will have a price of zero in chargeback reports.

### To remove a default price sheet from a selected cloud

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Chargeback**, expand **Clouds**, and then select **All Clouds**.

3.  In the list of clouds, select one that you want to remove the default price sheet from to and then under Tasks, click **Edit**.

4.  In *CloudName* form under **Default Cloud Price Sheet**, click **Remove**.

5.  Click **OK** to close the *CloudName* form.
