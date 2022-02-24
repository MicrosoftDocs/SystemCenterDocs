---
ms.assetid: a2732a5c-9722-412f-9efa-da652146d3e7
title: Data flow in Management Pack for SQL Server Replication
description: This section explains data flows in Management Pack for SQL Server Replication
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Data Flow

This section explains data flows in Management Pack for SQL Server Replication.

## Logical Structure

![Logical structure diagram](./media/sql-replication-management-pack/logical-structure-data-flow.png)

## Publication Flow

![Publication flow diagram](./media/sql-replication-management-pack/publication-flow-diagram.png)

## Replication Database Health

![Top-level structure diagram](./media/sql-replication-management-pack/top-level-structure-diagram.png)

### Virtual Distributor Level Structure

![Virtual distributor level structure diagram](./media/sql-replication-management-pack/virtual-distributor-diagram.png)

### Replication Agents

The following table lists replication agent files located in the **\Program Files\Microsoft SQL Server\100\COM** directory.

|Agent Executable|File Name|
|-|-|
|[Replication Snapshot Agent](/sql/relational-databases/replication/agents/replication-snapshot-agent)|snapshot.exe|
|[Replication Distribution Agent](/sql/relational-databases/replication/agents/replication-distribution-agent)|distrib.exe|
|[Replication Log Reader Agent](/sql/relational-databases/replication/agents/replication-log-reader-agent)|logread.exe|
|[Replication Queue Reader Agent](/sql/relational-databases/replication/agents/replication-queue-reader-agent)|qrdrsvc.exe|
|[Replication Merge Agent](/sql/relational-databases/replication/agents/replication-merge-agent)|replmerg.exe|

### Replication Maintenance Jobs

In addition to replication agents, replication has a number of jobs that perform scheduled and on-demand maintenance operations.

|Clean up job|Description|Default schedule|
|-|-|-|
|Agent History Clean Up: Distribution|Removes replication agent history from the distribution database.|Runs every ten minutes|
|Distribution Clean Up: Distribution|Removes replicated transactions from the distribution database. Deactivates subscriptions that have not been synchronized within the maximum distribution retention period.|Runs every ten minutes|
|Expired Subscription Clean Up|Detects and removes expired subscriptions from publication databases.|Runs every day at 1:00 A.M.|
|Reinitialize Subscriptions Having Data Validation Failures|Detects all subscriptions that have data validation failures and marks them for re-initialization. The next time the Merge Agent or Distribution Agent runs, a new snapshot will be applied at the Subscribers.|No default schedule (not enabled by default).|
|Replication Agents Checkup|Detects replication agents that are not actively logging history. It writes to the Microsoft Windows event log if a job step fails.|Runs every ten minutes.|
|Replication monitoring refresher for distribution|Refreshes cached queries used by Replication Monitor.|Runs continuously.|

### Virtual Publisher Level Structure

![Virtual Publisher level structure diagram](./media/sql-replication-management-pack/publisher-structure-diagram.png)

### Virtual Subscriber Level Structure

![Virtual Subscriber level structure diagram](./media/sql-replication-management-pack/describer-structure-diagram.png)
