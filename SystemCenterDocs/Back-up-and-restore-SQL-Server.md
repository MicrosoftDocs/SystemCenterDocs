---
title: Back up and restore SQL Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 668e63b2-ec8a-483c-904b-3caf2b18232e
---
# Back up and restore SQL Server
DPM provides backup and recovery for SQL Server databases. Additionally, you can configure protection for volumes, system state, or full bare\-metal recovery backup of a SQL Server database to fully protect the SQL Server deployment.

Why back up SQL Server with DPM:

-   DPM was designed to protect the advanced configurations of SQL Server.

-   DPM can be set to protect SQL Server as frequently as every 15 minutes.

-   DPM reduces potential conflicts between backup tools and SQL Server protection schedules.

-   DPM can protect SQL Server at the instance level or the database level. When protection at the instance level is turned on, DPM detects new databases on that instance and automatically adds them to its protection group.

-   DPM is an affordable option. It's a good fit for a small SQL Server footprint and can scale for organizations that have a larger SQL Server footprint.

-   DPM has the Self\-Service Recovery Tool \(SSRT\) that extends database administrators’ options for self\-service recovery of SQL databases.

See the following resources to set up SQL Server protection:

[SQL Server prerequisites](../Topic/SQL-Server-prerequisites.md)—Read this article before you begin deployment. It also discusses the prerequisites for protecting a SQL Server database that has **AlwaysOn** enabled.

[Configure SQL Server protection](../Topic/Configure-SQL-Server-protection.md)—This article describes how to set up protection groups and configure monitoring for SQL Server.

[Recover SQL Server data in DPM](../Topic/Recover-SQL-Server-data-in-DPM.md)—This article explains how to recover DPM data.

