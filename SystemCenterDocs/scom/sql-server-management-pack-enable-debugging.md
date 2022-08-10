---
ms.assetid: b6aec30b-3bd1-4e4e-a664-23faee39953a
title: Enabling debugging in Management Pack for SQL Server
description: This article explains how to enable debugging in Management Pack for SQL Server
author: Anastas1ya
ms.author: v-asimanovic
manager: vvithal
ms.date: 7/11/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Enabling Debugging

In Management Pack for SQL Server, you can enable debugging in the Windows Event log in cases when you want to investigate potential issues that may occur during monitoring or see the detailed data sets used in the management pack workflows.

To enable debugging, do the following:

1. Open the Windows registry.

2. Create the following key `\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\SQL Server MP` and add a value that corresponds to the management group name for which you want to collect logs.

For example, if you want to enable debugging for the **TestMG01** management group, you need to add the **TestMG01** value to the registry key above. The value can be of any type and with any data. The same should be done for each agent where extended logging must be enabled. You do not need to restart any service; changes are applied automatically.

>[!NOTE] 
>Currently you can enable extended logging for all SQL MP modules only. Extended logging of separate modules is not supported yet.
