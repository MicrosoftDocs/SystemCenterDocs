---
ms.assetid: ec50ea24-d1e0-4230-a3fc-717bd6556cb5
title: How health rolls up in Management Pack for SQL Server
description: This article explains how health rolls up
author: Anastas1ya
ms.author: v-fkornilov
manager: evansma
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# How Health Rolls Up in SQL Server Management Pack

This section explains diagrams that show how the health state of objects roll up in Management Pack for SQL Server.

## Legend

The following figure explains how to read the diagram.

![Illustration of the Legend.](./media/sql-server-management-pack/health-rolls-up-legend.png)

## Database Engine Health Rollup Diagram

The following diagram shows the inheritance model of the health state of Database Engine objects. The health state of child objects affects the health state of parent objects.

![The Health diagram.](./media/sql-server-management-pack/health-rollup-diagram.png)

## Database Health Rollup Diagram

The following diagram shows the inheritance model of the health state of database objects. The health state of child objects affects the health state of parent objects.

![The Database diagram.](./media/sql-server-management-pack/database-health-rollup-diagram.png)
