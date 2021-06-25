---
ms.assetid: 238bf100-2a47-4334-a4e6-a8c67d8aefdd
title: Known issues and troubleshooting in Management Pack for SQL Server Reporting Services
description: This article explains Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services

This article lists the known issues for Management Pack for SQL Server.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|The **DeploymentSeedDiscovery** module fails if the instance is stopped or paused|When an instance is stopped or paused, the **DeploymentSeedDiscovery** module fails with the following error: "An error occurred during discovery."|Start or resume the instance to eliminate the issue.|
|The console task output is not produced after the execution of tasks related to SQL Server cluster instance objects.|When running tasks from the System Center Operations Manager console for any of the SQL Server cluster instance objects, the console task output is never produced and the progress wheel keeps running continuously. Even though no output is displayed and the task wizard appears to be hanging, the task being executed still can send commands to the target SQL Server cluster instance object, forcing this object to execute the command.|No resolution.|