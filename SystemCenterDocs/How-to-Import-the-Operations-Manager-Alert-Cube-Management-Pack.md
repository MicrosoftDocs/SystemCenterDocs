---
title: How to Import the Operations Manager Alert Cube Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e305aef-3c43-470c-a1c5-c17394fdd7ce
robots: noindex,nofollow
---
# How to Import the Operations Manager Alert Cube Management Pack
By default, [!INCLUDE[smlong12](Token/smlong12_md.md)] does not automatically import the System Center Alert Management Cube management pack when you register Operations Manager as a data source.

Instead you must manually create a data source for Operations Manager. For more information, see [How to Register the System Center Data Warehouse to Operations Manager](How-to-Register-the-System-Center-Data-Warehouse-to-Operations-Manager.md). Afterward, use the following procedure to import the management pack.

### To import the Operations Manager alert cube management pack

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Data Warehouse**, click **Management Packs**, and confirm that **System Center Datawarehouse Operations Manager Library** is listed.

2.  On the Data Warehouse Management Server, type the following Windows PowerShell commands to manually import the management pack. \(This example assumes that Service Manager is on drive C and that you installed Service Manager using the default path\).

    ```
    cd 'C:\Program Files\Microsoft System Center\Service Manager 2012 R2\PowerShell'
    Import-Module .\System.Center.Service.Manager.psd1
    Import-SCSMManagementPack ..\AlertCube.mpb
    ```


