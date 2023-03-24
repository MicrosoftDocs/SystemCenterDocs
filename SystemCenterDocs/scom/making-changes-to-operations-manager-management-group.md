---
ms.assetid: 3de02832-cbf1-4e68-ae75-91b50f702c24
title: Making Changes to an Operations Manager Management Group
description: This article describes the tasks you may perform after you have deployed or upgraded Operations Manager in your environment.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 04/29/2019
ms.custom: UpdateFrequency3
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Making changes to an Operations Manager Management Group

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

After the initial deployment of System Center – Operations Manager, you might need to make changes or upgrades to the original deployment for reasons such as the following:

- Replace hardware that is experiencing problems and that is no longer considered reliable.  

- Replace hardware as part of the upgrade process from System Center - Operations Manager previous version.  

- Add additional hardware to improve scalability and performance.  

- Move a database and log file to a different volume because of space or performance reasons.  

- Change hardware that is leased and is due to expire soon.  

- Change or upgrade hardware to comply with new hardware standards.  

- You initially installed multiple Operations Manager features on a single server and you need to distribute some components to other servers.  

- You need to restore functionality in a failure scenario.  

Operations Manager supports changes to your Operations Manager infrastructure as listed below. Be cautious when performing these operations because they can result in data loss if not performed correctly.

- [Moving the Operational database](manage-move-opsdb.md)

- [Moving the Reporting data warehouse database](manage-move-omdwdb.md)

- [How to Configure Operations Manager to Communicate with SQL Server](manage-sqlserver-communication.md)
