---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Effects of Deleting a Connector on Configuration Items
ms.technology:  service-manager
ms.assetid:  fca58d2f-d6f4-470b-9f5d-dffb327c8e1a
---

# Effects of Deleting a Connector on Configuration Items

>Applies To: System Center 2016 - Service Manager

Many of the configuration items that are found in the Service Manager database are the result of the data that is imported by using connectors. Therefore, if a connector is deleted, the configuration items that are associated with that connector will also be deleted, except where the configuration item is related to an active incident or change request. If more than one connector defines a configuration item, the configuration item will be deleted when all of the contributing connectors are deleted.

If you are creating a new connector to replace an existing connector, create the new connector first, and then synchronize the new connector before deleting the old connector.

> [!TIP]
> ![PowerShell symbol](../media/pssymbol.png)You can use a Windows PowerShell command to remove a connector from Service Manager. For more information, see [Remove-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225363).
