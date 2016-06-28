---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Override a Default Price Sheet for a Specific VMM User Role
ms.technology:  service-manager
ms.assetid:  383a9a81-7543-4350-9618-02435baaac82
---

# How to Override a Default Price Sheet for a Specific VMM User Role

>Applies To: System Center 2016 Technical Preview - Service Manager

After Service Manager has discovered cloud objects from the Operations Manager CI connector, you can assign an existing price sheet that applies default price values to all the resources of the cloud. This process is useful when you have many virtual machines so that you do not have to define prices for all the individual virtual machine parts. Once the default price sheet is assigned to a cloud, you can override the default values, on a per-user basis. For more information about assigning a default price sheet to a cloud, see [How to Assign or Remove a Default Price Sheet for a Selected Cloud](How-to-Assign-or-Remove-a-Default-Price-Sheet-for-a-Selected-Cloud.md).

### To override a default price sheet for a specific VMM user role

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Chargeback**, expand **Clouds**, and then select **All Clouds**.

3.  In the list of clouds, select one that you want to assign a price sheet to and then under Tasks, click **Assign Price Sheet**.

4.  In <CloudName\> form under **User Role Price Sheet Overrides**, click **Add**.

5.  In the **Select objects** dialog box, select a VMM user role that you want to override the default price sheet with and click **Add** and then click **OK**.

6.  Under **User Role Price Sheet Overrides** scroll to the right and click **Assign Price Sheet** and then select a price sheet that is applied for the selected user only, and then click **OK**.

    > [!NOTE]
    > If a cloud previously had a price sheet assigned, then assigning a new one automatically unassigns the price sheet that was used previously.

7.  Click **OK** to close the <CloudName\> form.



