---
title: How to Remove an Operations Manager Management Pack_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd5ecaca-1cc5-40fc-b002-49f015c7269a
---
# How to Remove an Operations Manager Management Pack_1
When you no longer need a management pack, you can delete it using the Operations console. When you delete a management pack, all the settings and thresholds associated with it are removed from [!INCLUDE[om12long](./Token/om12long_md.md)]. Also, the .mp or .xml file for that management pack is deleted from the hard disk of the management server. You can delete a management pack only if you have first deleted dependent management packs.

### To remove a management pack

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In **Administration**, click **Management Packs.**

4.  In the **Management Packs** pane, right\-click the management pack you would like to remove and then click **Delete**.

5.  On the message stating that deleting the management pack might affect the scoping of some user roles, click **Yes**.

> [!NOTE]
> If any other imported management packs depend on the management pack you are trying to remove, the **Dependent Management Packs** error message displays. You must remove the dependent management packs before you can continue.

Operations Manager removes the selected management pack.

## See Also
[Creating a Management Pack for Overrides](./Creating-a-Management-Pack-for-Overrides.md)
[Management Packs Installed with Operations Manager](./Management-Packs-Installed-with-Operations-Manager.md)
[What Is in an Operations Manager Management Pack?](./What-Is-in-an-Operations-Manager-Management-Pack-.md)
[Management Pack Life Cycle](./Management-Pack-Life-Cycle.md)
[How to Import an Operations Manager Management Pack](./How-to-Import-an-Operations-Manager-Management-Pack.md)
[How to Export an Operations Manager Management Pack](./How-to-Export-an-Operations-Manager-Management-Pack.md)
[How to Add Knowledge to a Management Pack](./How-to-Add-Knowledge-to-a-Management-Pack.md)


