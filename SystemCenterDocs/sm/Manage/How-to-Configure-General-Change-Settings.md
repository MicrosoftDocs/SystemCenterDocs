---
title: How to Configure General Change Settings
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3de3a691-b2d7-4133-ad4a-e20a9f0f1475
---
# How to Configure General Change Settings

>Applies To: System Center 2016 Technical Preview - Service Manager

Use the following procedures to configure settings to specify change request prefixes and to define change request file attachment limits and then validate the settings.

> [!NOTE]
> Revising the change request prefix does not affect existing change requests.

### To configure general change settings

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Change Request Settings**.

4.  In the **Tasks** pane, in the **Change Request Settings** area, click **Properties**.

5.  In the **Change Request Settings** dialog box, you can make the following changes:

    1.  If you want to change the prefix code, change the default value in the **Change Request ID prefix** box.

    2.  If you want to change the maximum number of files that you can attach to a change request, change the default value in the **Maximum number of attached files** box. For example, type **2**.

    3.  If you want to change the maximum size of files that you attach to a change request, change the default value in the **Maximum size (KB)** box. For example, type **300**.

6.  Click **OK** to close the **Change Request Settings** dialog box.

### To validate change settings

1.  To validate changes to the prefix code, create a new a change request, and verify that the change request IDs have the prefix that you specified.

2.  To validate changes to the attachment settings, open a change request, and attempt to add a file attachment that violates the settings that you specified.



