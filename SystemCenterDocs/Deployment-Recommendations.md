---
title: Deployment Recommendations
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69723c85-7d0d-4fab-b866-95e87319be57
---
# Deployment Recommendations
The following guidelines provide options in an [!INCLUDE[orchshort](Token/orchshort_md.md)] deployment to improve high availability and performance.

## Management server
An [!INCLUDE[orchshort](Token/orchshort_md.md)] deployment is limited to one management server. A management server does not have to be available for runbook servers or runbooks to function. If the management server is not available, you cannot connect the Runbook Designer to publish runbooks or start, monitor, or stop runbooks. You can still start, monitor, and stop runbooks with the Orchestration console.

## [!INCLUDE[orchshort](Token/orchshort_md.md)] database
For high availability, you can deploy the [!INCLUDE[orchshort](Token/orchshort_md.md)] database on a Microsoft SQL Server cluster with a minimum of two nodes.

## [!INCLUDE[orchshort](Token/orchshort_md.md)] web service
The [!INCLUDE[orchshort](Token/orchshort_md.md)] web service must be installed on a server that is running Internet Information Services \(IIS\). The [!INCLUDE[orchshort](Token/orchshort_md.md)] web service does not have to be available for runbook servers or runbooks to function. If the [!INCLUDE[orchshort](Token/orchshort_md.md)] web service is not available, you cannot run the Orchestration console to start, monitor, or stop runbooks. You can install the web service on multiple IIS servers configured for load balancing to provide high availability and additional capacity.

## Runbook servers
For high availability, you should have at least two runbook servers. If the primary runbook server for a runbook is unavailable, the runbook can run on another server. runbook servers are not designed to run on a computer configured as a cluster node.

For more information about specifying the runbook servers for a runbook, see the [Using Runbooks in System Center 2012 - Orchestrator](Using-Runbooks-in-System-Center-2012---Orchestrator.md).

## Runbooks
By default, runbook servers can run 50 runbooks simultaneously. The physical computer resources and the complexity of the runbook limit the actual number of runbooks that a runbook server can manage.

For the process to modify the number of runbooks that can run simultaneously, see [How to Configure Runbook Throttling](How-to-Configure-Runbook-Throttling.md).

## See Also
[Using Runbooks in System Center 2012 - Orchestrator](Using-Runbooks-in-System-Center-2012---Orchestrator.md)


