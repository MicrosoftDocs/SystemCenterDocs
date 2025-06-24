---
title: Use Connectors to Import Data into System Center - Service Manager
description: Explains how to use connectors to import data into System Center - Service Manager.
ms.topic: article
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.service: system-center
ms.date: 11/01/2024
ms.subservice: service-manager
ms.custom: UpdateFrequency3, engagement-fy24
---

# Use connectors to import data into Service Manager



You can use System Center - Service Manager connectors to import data as configuration items from Active Directory Domain Services (AD DS), System Center Configuration Manager, System Center Orchestrator, System Center Virtual Machine Manager, and System Center Operations Manager. In addition, you can import alerts from Operations Manager, and you can configure these alerts to automatically generate incidents in Service Manager. You can also import data from comma-separated value (CSV) files into the Service Manager database.

This article explains how to use connectors to import data into System Center - Service Manager.

## Effects of deleting a connector on configuration items

Many of the configuration items that are found in the Service Manager database are the result of the data that is imported using connectors. Therefore, if a connector is deleted, the configuration items that are associated with that connector will also be deleted, except where the configuration item is related to an active incident or change request. If more than one connector defines a configuration item, the configuration item will be deleted when all of the contributing connectors are deleted.

If you're creating a new connector to replace an existing connector, create the new connector first, and then synchronize the new connector before deleting the old connector.

> [!TIP]
> ![PowerShell symbol](./media/import-data-connectors/pssymbol.png) You can use a Windows PowerShell command to remove a connector from Service Manager. For more information, see [Remove-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316239(v=sc.20)).

## Next steps

- Learn how to [import data from Active Directory Domain Services](import-data-ads.md).
- Learn how to [import data and alerts from Operations Manager](import-data-om.md).
- Learn how to [import data from Configuration Manager](import-data-cm.md).
