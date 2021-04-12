---
ms.assetid: ec50ea24-d1e0-4230-a3fc-717bd6556cb5
title: How Health Rolls Up in Management Pack for SQL Server
description: This article explains how health rolls up
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# How Health Rolls Up

The following diagrams show how the health states of objects roll up in Management Pack for SQL Server.

## Legend

![Legend](./media/sql-server-management-pack/health-rolls-up-legend.png)

## Database Engine Health Rollup Diagram 

The following diagram shows the inheritance model of the health state of Database Engine objects. The health state of child objects affects the health state of parent objects.

![Health diagram](./media/sql-server-management-pack/health-rollup-diagram.png)

## Database Health Rollup Diagram

The following diagram shows the inheritance model of the health state of database objects. The health state of child objects affects the health state of parent objects.

![Database diagram](./media/sql-server-management-pack/database-health-rollup-diagram.png)