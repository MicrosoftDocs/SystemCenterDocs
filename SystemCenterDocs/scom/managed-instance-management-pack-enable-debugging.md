---
title: Enabling debugging in Management Pack for Azure SQL Managed Instance
description: This article explains how to enable debugging in Management Pack for Azure SQL Managed Instance
manager: evansma
author: epomortseva
ms.author: v-ekaterinap
ms.date: 02/27/2024
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Debugging in Azure SQL Managed Instance Management Pack 

In Management Pack for Azure SQL Managed Instance, you can enable debugging in the Windows Event log in cases where you want to investigate potential issues that may occur during monitoring or see the detailed data sets used in the management pack workflows.

## Enabling Debugging

To enable debugging, follow these steps on the computer running System Center Operations Manager or another server that collects Azure SQL Managed Instance events:

1. Open the Windows registry.

2. Create the following key:
`HKLM\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\Azure SQL MI MP`

3. Create a Multi-String with the name `<Management Group Name>` that corresponds to the management group name for which you want to collect logs. Fill the **Value** field with the value "1" to enable module debugging.

> [!NOTE]
> Currently, you can enable extended logging for all Azure SQL Managed Instance MP modules only. Extended logging of separate modules isn't supported yet.