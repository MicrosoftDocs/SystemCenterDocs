---
title: Architecture of Service Management Automation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-management-automation-(sma)
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cefc0b34-d77a-4f17-8f69-68b4282beea7
---
# Architecture of Service Management Automation
The following diagram illustrates each of the [!INCLUDE[sma_1](Token/sma_1_md.md)] features and the communication between them.

![](Image/SMAArchitecture.jpg)

-   The [!INCLUDE[sma_1](Token/sma_1_md.md)] web service communicates with [!INCLUDE[katal_2](Token/katal_2_md.md)] and authenticates users.

-   The SQL Server databases store and retrieve runbooks, runbook assets, activities, integration modules, and runbook job information.

-   Runbook workers run the runbooks, and they can be used for load balancing.

-   The management portal in [!INCLUDE[katal_2](Token/katal_2_md.md)] is where you author, debug, and start and stop runbooks.


