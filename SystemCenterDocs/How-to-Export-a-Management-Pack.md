---
title: How to Export a Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9b7f519-1317-4917-bed9-e33b74976d5b
robots: noindex,nofollow
---
# How to Export a Management Pack
After you create a management pack in [!INCLUDE[smlong12](./Token/smlong12_md.md)], you can export the unsealed management pack as a file to back up any customizations in the management pack. The exported management pack is a valid XML\-formatted file. After you export an unsealed management pack, you can later import it to restore the objects that the management pack contains.

When you export a sealed management pack, from the [!INCLUDE[smcons](./Token/smcons_md.md)] or by using the Windows PowerShell cmdlet [Export\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225398), [!INCLUDE[smshort](./Token/smshort_md.md)] generates an equivalent, unsealed management pack and stores it as a .XML file on the hard drive. You can then edit this management pack file to increase the version of the management pack, and re\-seal it so it can be re\-imported into [!INCLUDE[smshort](./Token/smshort_md.md)].

Use the following procedures to export an unsealed management pack and then validate the export.

### To export a management pack

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Management Packs** pane, select the management pack that you want to export.

4.  In the **Tasks** pane, under the name of the management pack that you want to export, click **Export**.

5.  In the **Browse For Folder** dialog box, select a location for the file, and then click **OK**.

    > [!NOTE]
    > You cannot change the default name of the management pack file.

### To validate the export of a management pack

-   In Windows Explorer, ensure that you can locate the management pack file.

![](/Image/PSSymbol.gif)You can use Windows PowerShell commands to complete this task. For information about how to use Windows PowerShell to export a management pack as a valid XML\-formatted file that you can later import into [!INCLUDE[smshort](./Token/smshort_md.md)] or [!INCLUDE[om12short](./Token/om12short_md.md)], see [Export\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225398).

## See Also
[How to Import a Management Pack](./How-to-Import-a-Management-Pack.md)


