---
description:  
manager:  cfreeman
ms.topic:  article
author:  bwren
ms.author: bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  01/22/2018
title:  Architecture of Service Management Automation
ms.technology:  service-management-automation
---

# Architecture of Service Management Automation

The following diagram illustrates each of the Service Management Automation features and the communication between them.

![SMA Architecture diagram](/system-center/sma/media/architecture-of-service-management-automation/smaarchitecture.png)

-   The Service Management Automation web service communicates with Windows Azure Pack and authenticates users.

-   The SQL Server databases store and retrieve runbooks, runbook assets, activities, integration modules, and runbook job information.

-   Runbook workers run the runbooks, and they can be used for load balancing.

-   The management portal in Windows Azure Pack is where you author, debug, and start and stop runbooks.
