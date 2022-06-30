---
ms.assetid: 238bf100-2a47-4334-a4e6-a8c67d8aefdd
title: Known issues and troubleshooting in Management Pack for SQL Server Reporting Services
description: This article explains Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services
author: Anastas1ya
manager: evansma
<<<<<<< HEAD
ms.author: jsuri
ms.date: 5/12/2022
=======
ms.date: 6/30/2022
>>>>>>> b9a01db5f336d57615746b432a02f20e4a66efbd
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services

This article lists the known issues for Management Pack for SQL Server Reporting Services.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|The **DeploymentSeedDiscovery** module fails if the instance is stopped or paused|When an instance is stopped or paused, the **DeploymentSeedDiscovery** module fails with the following error: "An error occurred during discovery."|Start or resume the instance to eliminate the issue.|
|Usage of **Local System** as the monitoring account may cause monitoring issues on servers with SCOM Reporting Server|On servers having both SQL Server Reporting Services and SCOM Reporting Server installed at the same time, the usage of **Local System** as the monitoring account for SSRS management pack may cause both monitors "Report manager accessible" and "Web service accessible" to become inoperable. These monitors continually indicate an unhealthy state of the appropriate services regardless of the actual state. In addition, the event 26319 appears regularly in the Operations Manager log.|Use a domain account for the monitoring of SSRS.|
|The "CPU Utilization" monitor may show values above 100%|Sometimes in the heavy-load environments, the "CPU Utilization" monitor may show values above 100% for the monitored SSRS/PBI instance.|A fix of this issue will be provided in the next release of the SSRS Management Pack.|
