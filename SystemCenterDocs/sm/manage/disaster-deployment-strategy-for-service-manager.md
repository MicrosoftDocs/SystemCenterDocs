---
title: Deployment Strategy for Service Manager
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: debd28f1-c449-4190-99e2-81a4e731b97d
---

# Deployment Strategy for Service Manager

>Applies To: System Center 2016 - Service Manager

As a best practice, deploy your management servers and associated databases for Service Manager on separate computers. Isolating the management servers and databases provides for a successful disaster recovery operation in the event of potential software and equipment failures.  

 You must have a functioning database to restore a failed management server. Recovery of a management server is impossible if the management server and the associated database are on the same physical computer and that computer fails. For more information, see [Installing Service Manager on Four Computers](../deploy/deploy-installing-service-manager-on-four-computers.md).
