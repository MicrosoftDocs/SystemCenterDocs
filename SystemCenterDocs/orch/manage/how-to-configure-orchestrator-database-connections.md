---
title: How to Configure Orchestrator Database Connections
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cfcc2e1e-9dd0-46fd-8fdc-3dfcf3c11573
author: cfreemanwa
ms.author: cfreeman
ms.date: 2016-10-12
manager: cfreeman
---
# How to Configure Orchestrator Database Connections

> Apples To: System Center 2016 - Orchestrator

DBSetup allows you to secure an unsecured database. The common scenario is connecting to a restored backup.  

This utility provides two functions:  

1.  DBSetup allows you to change the database name or credentials that are used by the management server or runbook servers to connect to the database.  

2.  DBSetup allows you to connect to a rebuilt database.  

When connecting to a rebuilt database:  

-   This procedure can only be performed against the same database server used during the installation of the management server.  

-   You must have database permissions to create the database.  

In contrast, DBconfig only creates a new database; it does not configure the security for the database. DBConfig configures the database schema in the database and creates the contents of **settings.dat**, which contains the connection details for the management server and runbook servers. For more information on running DBConfig, see [How to Change the Orchestrator Database](../manage/how-to-change-the-orchestrator-database.md).  

### To configure Orchestrator database connections  

-   Run the DBsetup binary from the **Start** menu or from the **Program Files** folder.  

### To create a new database on a new database server  

1.  Run the System Center 2016 - Orchestrator Setup Wizard and install a new management server.  

2.  On the **Configure the database server** page in the setup wizard, point to the new database server.  

3.  After you add a new DB server to your deployment, you must also run permissionsconfig, and then export and import the service master key to the new database server.  

## See Also  
[How to Change the Orchestrator Database](../manage/how-to-change-the-orchestrator-database.md)  
