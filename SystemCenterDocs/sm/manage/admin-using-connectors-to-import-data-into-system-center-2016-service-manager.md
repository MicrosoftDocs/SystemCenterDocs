---
description:  
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 01/04/2017
title:  Using Connectors to Import Data into Service Manager
ms.technology:  service-manager
ms.assetid:  e79f0bdb-9330-4589-8d29-5d1a353c849a
---

# Using Connectors to Import Data into Service Manager

>Applies To: System Center 2016 - Service Manager

You can use Service Manager connectors to import data as configuration items from Active Directory Domain Services (AD DS), System Center Configuration Manager, System Center Orchestrator, System Center Virtual Machine Manager, and System Center Operations Manager. In addition, you can import alerts from Operations Manager, and you can configure these alerts to automatically generate incidents in Service Manager. You can also import data from comma-separated value (CSV) files into the Service Manager database.

## Service Manager 2016 connectors supported with System Center 2012 R2 components

To help simplify upgrades, you can use the following Service Manager 2016 connectors with System Center 2012 R2 components.

- System Center 2012 R2 Virtual Machine manager
- System Center 2012 R2 Orchestrator
- System Center 2012 R2 Operations Manager
- System Center 2012 R2 Configuration Manager (including SCCM 1511, 1602 and 1606)


## Using Connectors to Import Data Topics

-   [Effects of Deleting a Connector on Configuration Items](admin-effects-of-deleting-a-connector-on-configuration-items.md)

    Describes the effects of deleting a connector.

-   [Importing Data from Active Directory Domain Services](admin-importing-data-from-active-directory-domain-services.md)

    Describes how to create, synchronize, and disable or enable an Active Directory connector.

-   [Importing Data and Alerts from System Center Operations Manager](admin-importing-data-and-alerts-from-system-center-operations-manager.md)

    Describes how to create, synchronize, edit, disable or enable an Operations Manager alert or configuration item (CI) connector.

-   [Importing Data from System Center Configuration Manager](admin-importing-data-from-system-center-configuration-manager.md)

    Describes how to create a connector to System Center Configuration Manager and how to customize configuration management to extend the hardware information that is collected.

-   [Importing Runbooks from System Center Orchestrator](admin-importing-runbooks-from-system-center-orchestrator.md)

    Describes how to import runbooks from System Center Orchestrator.

-   [Importing Data from System Center Virtual Machine Manager](admin-importing-data-from-system-center-virtual-machine-manager.md)

    Describes how to import VMM objects into the Service Manager database.

-   [Using a CSV File to Import Data into Service Manager](admin-using-a-csv-file-to-import-data-into-service-manager.md)

    Describes how to import data into Service Manager by using a CSV file.
