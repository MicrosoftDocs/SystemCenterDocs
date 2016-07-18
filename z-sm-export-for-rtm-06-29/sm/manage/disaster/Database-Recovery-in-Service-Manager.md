---
title: Database Recovery in Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3edfc737-9548-416c-a9ec-aa7f11af8c3c
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Database Recovery in Service Manager
To restore a database \(which includes the encryption keys\) for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you rebuild a new computer using the same computer names and instance names as the original. Your disaster recovery strategy for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] databases should be based on general procedures for SQL Server 2008 disaster recovery. For more information, see [SQL Server 2008 R2 Books Online: Planning for Disaster Recovery](http://go.microsoft.com/fwlink/p/?LinkID=131016). Remember that if you restore a database, you must give the new computer the same name as the original computer and use the same instance name as the original instance.  
  
 In addition, you must use the script that you created in the [Backing Up Unsealed Management Packs in Service Manager](../../../sm/manage/disaster/Backing-Up-Unsealed-Management-Packs-in-Service-Manager.md) section in this guide. You use this script to restore permissions for the recreated database.  
  
> [!WARNING]  
>  Long\-term historical data is stored in the Service Manager data warehouse and the current snapshot of the system is stored in the Service Manager database. Recreating the Service Manager data warehouse databases should only be used as a measure of last resort. When possible, you should try to restore the Service Manager data warehouse databases from backups and avoid recreating those databases. If reinstalled, the newly created Service Manager data warehouse databases will be able to synchronize the current snapshot of the system from the Service Manager database—however, historical data will be lost.