---
title: Importing Data and Alerts from System Center Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e233cb46-69de-439d-a4f8-08d8ac993e64
---
# Importing Data and Alerts from System Center Operations Manager
If your organization uses System Center Operations Manager to monitor systems in your enterprise, the agents that are deployed gather information about configuration items that are discovered, and, as problems are detected, System Center Operations Manager generates alerts. Two connectors for Operations Manager are available in Service Manager: the configuration item \(CI\) connector that imports objects that are discovered by Operations Manager into the [!INCLUDE[smshort](../../Token/smshort_md.md)] database, and an alert connector that can create incidents based on alerts.

System Center Operations Manager collects information about many different types of objects, such as hard disk drives and Web sites. To import objects that are discovered by Operations Manager, [!INCLUDE[smshort](../../Token/smshort_md.md)] requires a list of class definitions for these objects; the list of definitions is in the System Center Operations Manager management packs. Therefore, you must import some System Center Operations Manager management packs into [!INCLUDE[smshort](../../Token/smshort_md.md)]. When you install [!INCLUDE[smshort](../../Token/smshort_md.md)], a set of System Center Operations Manager management packs for common objects and the required Windows PowerShell scripts are copied to your [!INCLUDE[smshort](../../Token/smshort_md.md)] installation folder. For more information, see [How to Import Management Packs for System Center Operations Manager Configuration Item Connectors](How-to-Import-Management-Packs-for-System-Center-Operations-Manager-Configuration-Item-Connectors.md). If you have installed additional management packs in Operations Manager, and you want to add the data from those additional management packs to [!INCLUDE[smshort](../../Token/smshort_md.md)], you can modify the configuration item \(CI\) connector to add the additional management packs. For more information, see [How to Edit a System Center Operations Manager Connector](How-to-Edit-a-System-Center-Operations-Manager-Connector.md).

The Microsoft Azure management pack for Operations Manager is supported in this release of [!INCLUDE[smshort](../../Token/smshort_md.md)]. This means that if an alert from Microsoft Azure is generated in Operations Manager, [!INCLUDE[smshort](../../Token/smshort_md.md)] will recognize the alert and an incident can be created.

## Importing Data and Alerts from Operations Manager Topics

-   [How to Import Management Packs for System Center Operations Manager Configuration Item Connectors](How-to-Import-Management-Packs-for-System-Center-Operations-Manager-Configuration-Item-Connectors.md)

    Describes how to import the management packs necessary for the System Center Operations Manager CI connectors.

-   [How to Create a System Center Operations Manager Connector](How-to-Create-a-System-Center-Operations-Manager-Connector.md)

    Describes how to create a System Center Operations Manager connector and import CIs and alerts from Operations Manager.

-   [How to Synchronize a System Center Operations Manager Connector](How-to-Synchronize-a-System-Center-Operations-Manager-Connector.md)

    Describes how to synchronize a System Center Operations Manager connector to reflect changes that you made in Operations Manager.

-   [How to Disable and Enable a System Center Operations Manager Connector](How-to-Disable-and-Enable-a-System-Center-Operations-Manager-Connector.md)

    Describes how to disable and enable a System Center Operations Manager connector to pause or resume data synchronization.

-   [How to Edit a System Center Operations Manager Connector](How-to-Edit-a-System-Center-Operations-Manager-Connector.md)

    Describes how to edit properties for a System Center Operations Manager connector.


