---
title: How to Configure General Activity Settings
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87d70344-d44d-4c54-b215-3217a217699b
---
# How to Configure General Activity Settings
Use the following procedure to configure settings to specify activity prefixes when you view activity records. You can then validate the settings. You can define these activity settings in the administrative area of the [!INCLUDE[smcons](../Token/smcons_md.md)].

> [!NOTE]
> Revising the activity request prefix does not affect existing activity records.

### To configure general activity settings

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Activity Settings**.

4.  In the **Tasks** pane, in the **Activity Settings** area, click **Properties**.

5.  In the **Activity Settings** dialog box, you can make the following changes:

    -   If you want to change the activity prefix code, change the default value in the **Activity prefix** box. For example, change the value to **AA**.

    -   If you want to change the manual activity prefix code, change the default value in the **Manual activity prefix** box. For example, change the value to **AM**.

    -   If you want to change the review activity prefix code, change the default value in the **Review activity prefix** box. For example, change the value to **AR**.

6.  Click **OK** to close the **Activity Settings** dialog box.

### To validate activity setting changes

-   To validate changes to any prefix code, create a new change request, and then verify on the **Activities** tab that the activities have the new prefix that you specified.

