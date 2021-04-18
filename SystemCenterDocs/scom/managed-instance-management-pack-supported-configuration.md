---
ms.assetid: c31d2851-7333-4aa0-8f4f-890eb1fbaa64
title: Scope and supported configuration in Management Pack for Azure SQL Managed Instance
description: This article explains the scope and supported configuration in Management Pack for Azure SQL Managed Instance
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for Azure SQL Managed Instance

Management Pack for Azure SQL Managed Instance supports monitoring of [Azure SQL Managed Instance](https://docs.microsoft.com/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview) and the corresponding entities using T-SQL queries.

## Supported Tiers and Features

Management Pack for Azure SQL Managed Instance supports the following tiers and managed instance features:

- Tiers
    - General Purpose
    - Business Critical (monitoring of Read-Scale Replicas is not supported yet)
- Features
    - Database Engine
    - Database
    - Agent and Jobs
    - Memory-Optimized Data (In-Memory OLTP)
    - Failover Groups, including secondary read-only replicas
    - Authentication Mode — both SQL Server Authentication and Azure AD Authentication are supported.

## System Center Operations Manager

Management Pack for Azure SQL Managed Instance supports agentless monitoring of Azure SQL Managed Instance only.

All workflows in the management pack are executed by the management servers that are members of the Management Server Pool. 

The management pack does not require to have a dedicated management group and can work in virtual environments.

The following is a list of supported versions of System Center Operations Manager:

- System Center Operations Manager 2012 R2
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019
