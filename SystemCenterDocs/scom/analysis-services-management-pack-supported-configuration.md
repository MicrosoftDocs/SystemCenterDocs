---
ms.assetid: a9edb3f9-ca6d-4b40-b202-4a9b5728dbc1
title: Scope and supported configuration in Management Pack for SQL Server Analysis Services
description: This article explains the scope and supported configuration for Management Pack for SQL Server Analysis Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server Analysis Services

This section lists operating systems and features supported by Management Pack for SQL Server Analysis Services.

## Operating Systems and Platforms

Management Pack for SQL Server Analysis Services supports the following operating systems and platforms:

- Windows Server 2012
- Windows Server 2016
- Windows Server 2019

## SQL Server Analysis Services Features

The following is a list of features and configurations supported in Management Pack for SQL Server Analysis Services:

- An instance of SQL Server Analysis Services running in one of these modes:
  - Multidimensional Mode
  - Tabular Mode
  - PowerPivot Mode

- SQL Server Analysis Services Databases

- SQL Server Analysis Services Database Partitions

- Clustered installation of SSAS

>[!NOTE]
>This management pack supports at least 3 SSAS instances with 100 databases on a single agent that uses default settings. If your environment contains more than 100 databases and 3 SSAS instances, some of the workflows may fail during monitoring and discovery. For more information on how to change the default agent settings, see [Management servers and their managed devices are dimmed in the Operations Manager console](/troubleshoot/system-center/scom/management-servers-devices-dimmed).

## System Center Operations Manager

Management Pack for SQL Server Analysis Services supports the following versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019

A dedicated Operations Manager management group is not required for this management pack.