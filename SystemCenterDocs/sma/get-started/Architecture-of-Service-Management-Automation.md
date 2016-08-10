---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Architecture of Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  cefc0b34-d77a-4f17-8f69-68b4282beea7
---

# Architecture of Service Management Automation

>Applies To: System Center Technical Preview

The following diagram illustrates each of the Service Management Automation features and the communication between them.

![](../../media/SMAArchitecture.jpg)

-   The Service Management Automation web service communicates with Windows Azure Pack and authenticates users.

-   The SQL Server databases store and retrieve runbooks, runbook assets, activities, integration modules, and runbook job information.

-   Runbook workers run the runbooks, and they can be used for load balancing.

-   The management portal in Windows Azure Pack is where you author, debug, and start and stop runbooks.



