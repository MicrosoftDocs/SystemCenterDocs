---
title: TCP Port Requirements
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9186a693-be7f-4bae-af75-3a7001926a47
---
# TCP Port Requirements
Communication between [!INCLUDE[orchshort](Token/orchshort_md.md)] features on different computers occurs over TCP\/IP. If you have firewalls in your environment between these features, you must enable the ports indicated in the following table.

|Source|Targeted computer|Default port|Configurable|Notes|
|----------|---------------------|----------------|----------------|---------|
|Runbook Designer|Management server|135, 1024\-65535|Yes|The Runbook Designer communicates with the management server over DCOM. By default, DCOM communicates over port 135 and dynamically allocates a port between 1024 and 65535. For information about configuring DCOM for a specific port range, see [Configuring Microsoft Distributed Transaction Coordinator \(DTC\) to work through a firewall](http://go.microsoft.com/fwlink/p/?LinkID=229219).|
|Management server<br /><br />runbook server<br /><br />Web service|orchestration database|1433|Yes|Specified during Microsoft SQL Server installation|
|Client browser|[!INCLUDE[orchshort](Token/orchshort_md.md)] REST\-based web service|81|Yes|Specified during [!INCLUDE[orchshort](Token/orchshort_md.md)] installation. Both ports must be accessible for the Orchestration console.|
|Client browser|Orchestration console|82|Yes|Specified during [!INCLUDE[orchshort](Token/orchshort_md.md)] installation. Both ports must be accessible for the Orchestration console.|
|Activities|Various targeted computers depending on activity|||For information about individual integration packs, see [Integration Packs for System Center 2012 \- Orchestrator &#91;Orch2012\_TechNet\_IP&#93;](assetId:///e6aff353-c364-4852-bfb7-9088407a7bd9).|

## Other resources for this product

-   TechNet Library main page for [Orchestrator_1](Orchestrator_1.md)

-   [Deploying System Center 2012 - Orchestrator](Deploying-System-Center-2012---Orchestrator.md)

-   [Plan Your Orchestrator Deployment](Plan-Your-Orchestrator-Deployment.md)

-   [System Requirements](assetId:///aabe0348-a207-46e4-87df-24aa993df984)

-   [Orchestrator Security Planning](assetId:///358c5344-8649-4d40-a53c-37f8e70e58f6)

## See Also
[Plan Your Orchestrator Deployment](Plan-Your-Orchestrator-Deployment.md)
[Integration Packs for System Center 2012 \- Orchestrator &#91;Orch2012\_TechNet\_IP&#93;](assetId:///e6aff353-c364-4852-bfb7-9088407a7bd9)


