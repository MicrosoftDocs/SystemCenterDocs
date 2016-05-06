---
title: How to Add a List Item
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90b35dee-ae3b-42f0-986b-17bd1bc84037
robots: noindex,nofollow
---
# How to Add a List Item
In [!INCLUDE[smlong12](../Token/smlong12_md.md)], you can use these procedures to add a list item to an existing list and then validate it. For example, you can use this procedure to add a Laser Printer and Check\-Writing Printer list item to the **Incident Classification** list.

### To add list items to Service Manager lists

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, click **Lists**. The **Lists** pane displays all the existing lists.

3.  Select the list to which you want to add a list item. For example, select the **Incident Classification** list. In the **Tasks** pane, under **Incident Classification**, click **Properties**.

4.  In the **List Properties** dialog box, click **Printing Problems**, and then click **Add Child**. Notice that a new **List Value** list item is added.

    > [!NOTE]
    > When you click **Add Item** or **Add Child**, a **Select management pack** dialog box might appear. If this dialog box appears, select the default management pack, select another unsealed management pack, or create a new management pack.

5.  Click the new **List Value** list item. In the **Name** box, type a name for the new list item. For example, type **Laser Printer**. If you want, you can optionally type a description in the **Description** box.

6.  Repeat steps 4 and 5 and create a new list item with the name **Check\-Writing Printer**, and then click **OK**.

### To validate the addition of a new list item

1.  Select the same list again, click **Properties** in the **Tasks** pane, and then verify that the new list item appears.

2.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], create a new incident, and then locate the new list item in the **Classification Category** list. For example, expand **Printer Problems**, and then locate the **Laser Printer** and **Check\-Writing Printer** list items.

    For more information about creating a new incident, see the topic [How to Manually Create a New Incident](assetId:///e6541088-f94a-4fb5-80ce-be8afad11b81) in the Operations Guide for [!INCLUDE[smlong12](../Token/smlong12_md.md)].

