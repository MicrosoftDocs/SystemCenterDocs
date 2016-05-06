---
title: How to Manually Create Configuration Items
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24089a9b-eaa2-42f7-b600-2d0e6a2149ec
---
# How to Manually Create Configuration Items
You might have to create a configuration item to add computers that do not exist in Active Directory Domain Services \(AD DS\) and that are not managed by Configuration Manager to the Service Manager database.

Additionally, you might have to manually create a new user configuration item to be used in the **Affected User** box in incidents created by Operations Manager.

You can use the following procedures to manually create two computer configuration items. However, you can also use the same procedures to add software, printers, or software updates in [!INCLUDE[smshort](./Token/smshort_md.md)]. After you add the two computers, you can identify them as a service.

### To manually create a computer configuration item

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, and then expand **Computers**.

3.  Click **All Windows Computers**. In the **Tasks** pane, under **Computers**, click **Create Computer**.

4.  In the form that appears, create a configuration item for a computer, such as **Exchange01.woodgrove.com**. On the **General**, **Software**, and **Related Items** tabs, enter information about the computer.

5.  Click **OK** to save the new configuration item.

6.  Repeat step 3 through step 5 to create a second computer, such as **Exchange02.woodgrove.com**.

### To manually create a user configuration item

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **Users**.

3.  In the **Tasks** pane, under **Users**, click **Create User**.

4.  On the **General** tab in the form, follow these steps:

    1.  In the **First Name** box, type a first name. For example, for the user account that will be used to populate the **Affected User** box for all incidents created by Operations Manager, type **OMAlert**.

    2.  In the **Last Name** box, type a last name. For example, for the user account that will be used to populate the **Affected User** box for all incidents created by Operations Manager, type **User**.

5.  On the **Notification** tab, click **Add**, and perform the following for each notification address that you want to add:

    1.  In the **User Notification** dialog box, in the **Notification address name** box, type a name you want to use for this notification.

    2.  In the **Notification address description** box, type a description you want to use for this notification.

    3.  In the **Delivery address for this notification channel** box, type the address you would use to deliver a notification. Typically, this would be an email address.

    4.  Click **OK**.

### To validate the manually created configuration item

-   Verify that the computer you added appears in the **Computers** pane.

-   Verify that the user you added appears in the **Users** pane.


