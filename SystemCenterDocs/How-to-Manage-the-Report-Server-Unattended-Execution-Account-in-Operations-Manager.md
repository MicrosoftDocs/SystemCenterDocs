---
title: How to Manage the Report Server Unattended Execution Account in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15305141-083c-4b98-b745-28c7b68fcb46
---
# How to Manage the Report Server Unattended Execution Account in Operations Manager
The Operations Manager Report Server unattended execution account is used to query data from the Reporting Data Warehouse. Users that manage this account require only the Read user right. This account is not managed from within the Operations Manager user interface. Use this procedure to change the user name or password for this account.

### To manage the Report Server unattended execution account

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, point to **Configuration Tools**, and then click **Reporting Services Configuration Manager**.

2.  In **Reporting Services Configuration Manager**, in the **Report Server Installation Instance Selection** dialog box, click **Connect**.

3.  In the navigation pane, click **Execution Account**.

4.  In the **Execution Account** pane, type a new user name or password as required.

5.  Click **Apply**, and then click **Exit**.

## See Also
[Managing Access in Operations Manager](../Topic/Managing-Access-in-Operations-Manager.md)
[Operations Manager Accounts](../Topic/Operations-Manager-Accounts.md)
[Implementing User Roles](../Topic/Implementing-User-Roles.md)
[How to Create a New Action Account in Operations Manager](../Topic/How-to-Create-a-New-Action-Account-in-Operations-Manager.md)
[Control Access by Using the Health Service Lockdown Tool in Operations Manager](../Topic/Control-Access-by-Using-the-Health-Service-Lockdown-Tool-in-Operations-Manager.md)
[Accessing UNIX and Linux Computers in Operations Manager](../Topic/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Managing Run As Accounts and Profiles](../Topic/Managing-Run-As-Accounts-and-Profiles.md)

