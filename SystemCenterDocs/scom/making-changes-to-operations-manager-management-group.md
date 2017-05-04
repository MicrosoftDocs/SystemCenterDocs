---
ms.assetid: 3de02832-cbf1-4e68-ae75-91b50f702c24
title: Making Changes to an Operations Manager Management Group
description: This article describes the tasks you may perform after after you have deployed or upgraded Operations Manager in your environment.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/02/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Making changes to an Operations Manager Management Group

>Applies To: System Center 2016 - Operations Manager

After the initial deployment of System Center 2016 – Operations Manager, you might need to make changes or upgrades to the original deployment for reasons such as the following: 

- You need to replace hardware that is experiencing problems and that is no longer considered reliable.  

- You need to replace hardware as part of the upgrade process from System Center Operations Manager 2012 R2.  

- You need to add additional hardware to improve scalability and performance.  

- You need to move a database and log file to a different volume because of space or performance reasons.  

- You need to change hardware that is leased and is due to expire soon.  

- You need to change or upgrade hardware to comply with new hardware standards.  

- You initially installed multiple Operations Manager features on a single server and you need to distribute some components to other servers.  

- You need to restore functionality in a failure scenario.  

Operations Manager supports changes to your Operations Manager infrastructure as listed below. Be cautious when performing these operations because they can result in data loss if not performed correctly.

- [Moving the Operational database](manage-move-opsdb.md)

- [Moving the Reporting data warehouse database](manage-move-omdwdb.md)

- [How to Configure Operations Manager to Communicate with SQL Server](manage-sqlserver-communication.md)
