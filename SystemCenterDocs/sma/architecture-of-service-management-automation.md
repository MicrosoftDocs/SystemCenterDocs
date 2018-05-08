---
title: Service Management Automation architecture in System Center
description: Provides an overview of the architecutre in System Center Service Management Automation (SMA)
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center-threshold
ms.date: 05/08/2018
ms.technology: service-management-automation

---

# Service Management Automation architecture

This article shows a diagram that illustrates each SMA feature.


![SMA architecture diagram](/system-center/sma/media/architecture-of-service-management-automation/architecture.png)
![SMA architecture diagram](/system-center/sma/media/architecture-of-service-management-automation/smaarchitecture.png)
 
 ## Features

  - The SMA web service communicates with Windows Azure Pack and authenticates users.
  - The SQL Server databases store and retrieve a number of components. These include runbooks, runbook assets, activities, integration modules, and runbook job information.
  - Runbook workers run the runbooks, and they can be used for load balancing.
  The management portal in Windows Azure Pack is where you author, debug, start, and stop runbooks.

## Next steps
Learn [what's new](whats-new-1801.md) in the latest version of SMA.
