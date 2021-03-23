---
ms.assetid: 238bf100-2a47-4334-a4e6-a8c67d8aefdd
title: Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services
description: This article explains Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services

This article lists the known issues for Management Pack for SQL Server.

|Issue title|Behavior / Symptom|Known workaround|
|-|-|-|
|The **DeploymentSeedDiscovery** module fails if the instance is stopped or paused|When an instance is stopped or paused, the **DeploymentSeedDiscovery** module fails with the following error: "An error occurred during discovery."|Start or resume the instance to eliminate the issue.|
|Non-printable characters (or formatting marks) are not supported|Management Pack for SQL Server Reporting Services does not support object names consisting of non-printable characters.|No resolution.|