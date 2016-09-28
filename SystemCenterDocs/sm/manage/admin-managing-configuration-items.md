---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Managing Configuration Items
ms.technology:  service-manager
ms.assetid:  22d6d616-e0b3-47b2-a8d8-f235091bf1d5
---

# Managing Configuration Items

>Applies To: System Center 2016 - Service Manager

You might want to associate a work item to apply a Microsoft Exchange Server service pack update to the service that represents the computers that are affected by the email incident. To accomplish this, you can update the service configuration item and then add the respective work item as a related item.

You can use the following procedures to add information, such as related work items or files, to configuration items in Service Manager. The procedures in this topic describe only how to add items, but you can follow similar steps to view or remove items.

For example, when you are troubleshooting an incident, you might discover that a relationship exists between two or more objects. A work item to apply an application service pack might be related to more than one configuration item. You might need to update the configuration items to reflect that relationship.

Similarly, work items such as incidents, problems, and change requests are often interrelated. Related work items share some commonality with each other or with a configuration item. When a work item affects a particular configuration item, they are linked.

### To add information to configuration items

1.  In the Service Manager console, click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, and then expand **Computers**.

3.  Click **All Windows Computers**. In the **All Windows Computers** pane, double-click the computer to which you want to add information.

4.  In the computer form, click the **Related Items**tab.

    ##### To add related services, people, and configuration items

    1.  In the **Configuration Items: Computers, Services, and People** area, click **Add**.

    2.  In the **Select Objects** dialog box, select a class from the **Filter by class** list to narrow the choices available in the **Available objects** list.

    3.  In the **Available objects** list, select the items that you want to add, and then click **Add**.

    4.  Click **OK** to close the dialog box and to add the selected items.

    ##### To add related work items

    1.  In the **Related work items** area, click **Add**.

    2.  In the **Select Objects** dialog box, select a class from the **Filter by class** list to narrow the choices available in the **Available objects** list.

    3.  In the **Available objects** list, select the work items that you want to add, and then click **Add**.

    4.  Click **OK** to close the dialog box and to add the selected work items.

    ##### To attach files

    1.  In the **Attached files** area, click **Add**.

    2.  In the **Open** dialog box, select the file that you want to add, and then click **Open**.

    3.  In this release, do not attempt to open an attached file before you submit the form.

5.  Click **OK** to save the form.



