---
ms.assetid: ec50ea24-d1e0-4230-a3fc-717bd6556cb5
title: Health rolls up in management pack for SQL Server
description: This article explains how health rolls up
author: Anastas1ya
manager: evansma
ms.date: 04/21/2025
ms.author: jsuri
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Health rolls up in SQL Server Management Pack

This article explains diagrams that show how the health state of objects rolls up in Management Pack for SQL Server.

## Legend

The following figure explains how to read the diagram:

![Illustration of the Legend.](./media/sql-server-management-pack/health-rolls-up-legend.png)

## Database Engine health rollup diagram

The following diagram shows the inheritance model of the health state of Database Engine objects. The health state of child objects affects the health state of parent objects.

![The Health diagram.](./media/sql-server-management-pack/health-rollup-diagram.png)

## Database health rollup diagram

The following diagram shows the inheritance model of the health state of database objects. The health state of child objects affects the health state of parent objects.

![The Database diagram.](./media/sql-server-management-pack/database-health-rollup-diagram.png)
