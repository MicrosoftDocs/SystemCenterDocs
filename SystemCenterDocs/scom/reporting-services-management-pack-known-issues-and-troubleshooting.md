---
ms.assetid: 238bf100-2a47-4334-a4e6-a8c67d8aefdd
title: Known issues and troubleshooting in Management Pack for SQL Server Reporting Services
description: This article explains Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: troubleshooting-known-issue
ms.service: system-center
ms.subservice: operations-manager
---

# Known Issues and Troubleshooting in Management Pack for SQL Server Reporting Services

This article lists the known issues for Management Pack for SQL Server Reporting Services.

|Issue title|Behavior/Symptom|Known workaround|
|-|-|-|
|The **SQL Server Reporting Discovery**, **SQL Server Reporting Monitoring**, and **SQL Server Reporting Deployment** modules fail if the SQL Server instance that hosts the Reporting Services database is stopped or paused.|When an SQL Server instance that hosts the Reporting Services database is stopped or paused, all the Reporting Services modules fail with the following error: **A network-related or instance-specific error occurred while establishing a connection to SQL Server.**|Start or resume the SQL Server instance to eliminate the issue.|
