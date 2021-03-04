---
ms.assetid: 117e9e45-633c-49b4-8e22-f26d397c061e
title: Management Pack for Azure SQL Managed Instance Delivery
description: This article explains how to install Management Pack for Azure SQL Managed Instance
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for Azure SQL Managed Instance Delivery

You can download Management Pack for Azure SQL Managed Instance from the [Microsoft portal](https://www.microsoft.com/en-us/download/details.aspx?id=101203) or System Center Operations Manager Online Catalog.

The package includes the following files:

- **Microsoft.Azure.ManagedInstance.ManagementPack.msi**—a set of MP and MPB files for monitoring of Azure SQL Managed Instance.

Management Pack for Azure SQL Managed Instance consists of the following files:  

- Microsoft.Azure.ManagedInstance.Discovery.mpb

- Microsoft.Azure.ManagedInstance.Monitoring.mpb

- Microsoft.Azure.ManagedInstance.Views.</i>mp

- Microsoft.SQLServer.Core.Library.mpb

- Microsoft.SQLServer.Visualization.Library.mpb

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for Azure SQL Managed Instance:

- Install **.NET Framework 4.6.1** or higher on all management servers participating in managed instance monitoring.

- Provide access to managed instances from management servers.

    Managed instances are usually deployed to an isolated private network. This means that there should be a permanent VPN connection configured on servers from which the managed instances should be accessed. 
    
## Importing Management Pack

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).

