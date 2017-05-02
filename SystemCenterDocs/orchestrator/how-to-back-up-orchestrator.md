---
title: How to Back up Orchestrator
description: Describes how to backup a System Center 2016 - Orchestrator environment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44c3460d-4171-4838-84c7-a9c3bd75b28a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# How to Back up Orchestrator

> Applies To: System Center 2016 - Orchestrator

A complete backup of an Orchestrator environment consists of the following:  

-   Backup of the Orchestrator database.  
-   File backup of the Orchestrator management server.  
-   File backup of each Runbook server and Orchestrator web server.  

System Center 2016 - Orchestrator supports Volume Shadow copy Service \(VSS\) for backup and restore with System Center 2016 - Data Protection Manager (DPM). VSS is a framework that allows volume backups to be performed while an application continues to run.  

## Registering Orchestrator with VSS  
The **SCOExpressWriter** command\-line utility registers an Orchestrator database as a component associated with the Orchestrator management server. This association instructs DPM to back up the Orchestrator database when it performs a backup of the management server. Without this registration DPM must perform an individual backup of each component.  

You must run **SCOExpressWriter** on the management server being registered, and you must be logged on with a user account that is a member of the local Administrators group.  

The usage of this command\-line utility is as follows:  

`SCOExpressWriter {/register | /unregister}`  

To register the Orchestrator database used by the local management server, run the following command:  

`SCOExpressWriter /register`  

## Orchestrator Servers  
Orchestrator management server, Runbook servers, and web servers do not persist any data. Runbooks and their settings are stored entirely in the Orchestrator database and accessed by these servers as required. Management servers and Runbook servers have a settings.dat file that includes configuration details to connect to the Orchestrator database. Orchestrator web servers have a web.config file with this same information. These files are backed up with standard file backups which are supported by DPM.  

## Orchestrator Database  
The Orchestrator database is a standard SQL Server database that is supported by DPM. You should make sure to backup the service master key and store it in a secure off\-site location. For more information see [BACKUP SERVICE MASTER KEY \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=243093).  

## Next steps

[How to recover a database](how-to-recover-a-database.md)