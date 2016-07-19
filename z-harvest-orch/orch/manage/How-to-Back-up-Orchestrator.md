---
title: How to Back up Orchestrator
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44c3460d-4171-4838-84c7-a9c3bd75b28a
author:bwren
manager:cfreemanwa
---
# How to Back up Orchestrator
A complete backup of an [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] environment consists of the following:  
  
-   Backup of the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database.  
  
-   File backup of the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] management server.  
  
-   File backup of each Runbook server and [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] web server.  
  
[!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] supports Volume Shadow copy Service \(VSS\) for backup and restore with [!INCLUDE[dpm2012long](../../orch/manage/includes/dpm2012long_md.md)]. VSS is a framework that allows volume backups to be performed while an application continues to run.  
  
## Registering Orchestrator with VSS  
The **SCOExpressWriter** command\-line utility registers an [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database as a component associated with the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] management server. This association instructs [!INCLUDE[dpm2012short](../../orch/manage/includes/dpm2012short_md.md)] to back up the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database when it performs a backup of the management server. Without this registration [!INCLUDE[dpm2012short](../../orch/manage/includes/dpm2012short_md.md)] must perform an individual backup of each component.  
  
You must run **SCOExpressWriter** on the management server being registered, and you must be logged on with a user account that is a member of the local Administrators group.  
  
The usage of this command\-line utility is as follows:  
  
`SCOExpressWriter {/register | /unregister}`  
  
To register the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database used by the local management server, run the following command:  
  
`SCOExpressWriter /register`  
  
## Orchestrator Servers  
[!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] management server, Runbook servers, and web servers do not persist any data. Runbooks and their settings are stored entirely in the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database and accessed by these servers as required. Management servers and Runbook servers have a settings.dat file that includes configuration details to connect to the [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database. [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] web servers have a web.config file with this same information. These files are backed up with standard file backups which are supported by [!INCLUDE[dpm2012short](../../orch/manage/includes/dpm2012short_md.md)].  
  
## Orchestrator Database  
The [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] database is a standard SQL Server database that is supported by [!INCLUDE[dpm2012short](../../orch/manage/includes/dpm2012short_md.md)]. You should make sure to backup the service master key and store it in a secure off\-site location. For more information see [BACKUP SERVICE MASTER KEY \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=243093).  
  
