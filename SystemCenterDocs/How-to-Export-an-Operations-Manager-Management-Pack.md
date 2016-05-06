---
title: How to Export an Operations Manager Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a46a374-f6b2-4e69-8459-b4171cd8bb30
---
# How to Export an Operations Manager Management Pack
Exporting a management pack allows customizations to a sealed management pack to be saved to a file. Because sealed management packs cannot be changed, the customizations made to a management pack are saved to a separate, unsealed management pack file. The unsealed management pack can then be imported to a different management group. This unsealed management pack is dependent on the original sealed management pack and can be imported only to management groups that have the original sealed management pack.

> [!NOTE]
> Using the Operations Console, you can only export unsealed management packs. To export a sealed management pack, you must use the Export\-SCOMManagementPack cmdlet. See [Operations Manager Cmdlet Reference \[OM2012\]](assetId:///b38f41d8-8e7c-4b56-82b1-95af6527b8a4) for more information.

### To export management pack customizations

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In **Administration**, click **Management Packs** to display the list of imported management packs.

4.  In the **Management Packs** pane, right\-click the management pack you want to export, and then click **Export Management Pack**.

5.  In the **Browse For Folder** dialog box, expand the path for the location to save the file, and then click **OK**.

    The management pack is saved as an Operations Manager XML management pack file and is ready for importing into another management group.

## See Also
[Creating a Management Pack for Overrides](./Creating-a-Management-Pack-for-Overrides.md)
[Management Packs Installed with Operations Manager](./Management-Packs-Installed-with-Operations-Manager.md)
[What Is in an Operations Manager Management Pack?](./What-Is-in-an-Operations-Manager-Management-Pack-.md)
[Management Pack Life Cycle](./Management-Pack-Life-Cycle.md)
[How to Import an Operations Manager Management Pack](./How-to-Import-an-Operations-Manager-Management-Pack.md)
[How to Remove an Operations Manager Management Pack](./How-to-Remove-an-Operations-Manager-Management-Pack.md)
[How to Add Knowledge to a Management Pack](./How-to-Add-Knowledge-to-a-Management-Pack.md)


