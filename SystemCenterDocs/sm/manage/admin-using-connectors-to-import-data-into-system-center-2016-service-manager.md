---
title:  Use connectors to import data
description: Explains how to use connectors to import data into Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 01/04/2017
ms.technology: service-manager
ms.assetid: e79f0bdb-9330-4589-8d29-5d1a353c849a
---

# Use connectors to import data into Service Manager

>Applies To: System Center 2016 - Service Manager

You can use Service Manager connectors to import data as configuration items from Active Directory Domain Services (AD DS), System Center Configuration Manager, System Center Orchestrator, System Center Virtual Machine Manager, and System Center Operations Manager. In addition, you can import alerts from Operations Manager, and you can configure these alerts to automatically generate incidents in Service Manager. You can also import data from comma-separated value (CSV) files into the Service Manager database.

## Service Manager 2016 connectors supported with System Center 2012 R2 components

To help simplify upgrades, you can use the following Service Manager 2016 connectors with System Center 2012 R2 components.

- System Center 2012 R2 Virtual Machine manager
- System Center 2012 R2 Orchestrator
- System Center 2012 R2 Operations Manager
- System Center 2012 R2 Configuration Manager (including SCCM 1511, 1602 and 1606)

## Effects of deleting a connector on configuration items

Many of the configuration items that are found in the Service Manager database are the result of the data that is imported by using connectors. Therefore, if a connector is deleted, the configuration items that are associated with that connector will also be deleted, except where the configuration item is related to an active incident or change request. If more than one connector defines a configuration item, the configuration item will be deleted when all of the contributing connectors are deleted.

If you are creating a new connector to replace an existing connector, create the new connector first, and then synchronize the new connector before deleting the old connector.

> [!TIP]
> ![PowerShell symbol](../media/pssymbol.png)You can use a Windows PowerShell command to remove a connector from Service Manager. For more information, see [Remove-SCSMConnector](http://go.microsoft.com/fwlink/p/?LinkID=225363).
