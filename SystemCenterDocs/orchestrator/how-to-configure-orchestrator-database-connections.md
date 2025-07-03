---
title: Configure Orchestrator database connections
description: Describes how to configure database connections in System Center - Orchestrator.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Configure Orchestrator database connections

As part of your day-to-day operations of Orchestrator, you may need to change the connection settings to the Orchestrator database. You can use the `DBSetup` utility to change this setting. The common scenario is connecting to a restored backup.  

This utility provides two functions:  

1. `DBSetup` allows you to change the database name or credentials that are used by the management server or runbook servers to connect to the database.  
2. `DBSetup` allows you to connect to a rebuilt database.  

When connecting to a rebuilt database:  

- This procedure can only be performed against the same database server used during the installation of the management server.  
- You must have database permissions to create the database.  

In contrast, `DBconfig` only creates a new database; it doesn't configure the security for the database. DBConfig configures the database schema in the database and creates the contents of **settings.dat**, which contains the connection details for the management server and runbook servers. For more information on running DBConfig, see [How to Change the Orchestrator Database](how-to-change-the-orchestrator-database.md).  

To configure Orchestrator database connections

- Run the `DBsetup` binary from the **Start** menu or from the **Program Files** folder.  

## Create a new database on a new database server  

Follow these steps to create a new database on a new database server:

1. Run the Orchestrator Setup Wizard, and install a new management server.  
2. On the **Configure the database server** page in the setup wizard, point to the new database server.  
3. After you add a new DB server to your deployment, you must also run `permissionsconfig`, and then export and import the service master key to the new database server.  

## Next steps

Learn more about how to change the Orchestrator database at [How to Change the Orchestrator Database](how-to-change-the-orchestrator-database.md).
