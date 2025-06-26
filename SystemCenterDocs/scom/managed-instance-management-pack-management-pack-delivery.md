---
ms.assetid: 117e9e45-633c-49b4-8e22-f26d397c061e
title: Management Pack for Azure SQL Managed Instance delivery
description: This article explains how to install Management Pack for Azure SQL Managed Instance
author: epomortseva
ms.author: v-fkornilov
manager: vvithal
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Management Pack for Azure SQL Managed Instance Delivery

You can download Management Pack for Azure SQL Managed Instance from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=101203) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.Azure.ManagedInstance.ManagementPack.msi** package - a set of MP and MPB files for monitoring of Azure SQL Managed Instance, the following files become available:

- Microsoft.Azure.ManagedInstance.Discovery.mpb
- Microsoft.Azure.ManagedInstance.Monitoring.mpb
- Microsoft.Azure.ManagedInstance.Views.mp
- Microsoft.SQLServer.Core.Library.mpb
- Microsoft.SQLServer.Visualization.Library.mpb

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for Azure SQL Managed Instance:

- Install **.NET Framework 4.7.2** or higher on all management servers participating in managed instance monitoring.

- Enable **TLS 1.2** protocol.

    To correctly enable Transport Layer Security (TLS) 1.2 encryption protocol, see [How to enable TLS 1.2](/mem/configmgr/core/plan-design/security/enable-tls-1-2).

- Provide access to managed instances from management servers.

    Managed instances are usually deployed to an isolated private network. This means that there should be a permanent VPN connection configured on servers from which the managed instances should be accessed.

> [!NOTE]
> Management Pack for Azure SQL Managed Instance doesn't support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Importing Management Pack

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).
