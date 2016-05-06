---
title: Disaster Recovery Guide for System Center Technical Preview - Service Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2afd9e-3e8e-4a4d-a89c-fcddf6733256
---
# Disaster Recovery Guide for System Center Technical Preview - Service Manager
A recovery plan for potential software and equipment failures in your [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)] environment requires a deployment strategy that separates the [!INCLUDE[smshort12](./Token/smshort12_md.md)] and data warehouse management servers from the computers that host their respective databases. During installation, you must back up the encryption keys on all the management servers, both the Service Manager management server and data warehouse management servers.

> [!NOTE]
> The encryption keys on the Service Manager management server and data warehouse management server are different and each must be backed up.

You must also back up the [!INCLUDE[smshort12](./Token/smshort12_md.md)] databases and your unsealed management packs.

## Disaster recovery topics

-   [Disaster Recovery Scenarios Overview](./Disaster-Recovery-Scenarios-Overview.md)

    Provides an overview of the potential disaster recovery scenarios that are presented in this guide.

-   [Prepare for Service Manager Disaster Recovery](./Prepare-for-Service-Manager-Disaster-Recovery.md)

    Describes the steps you can take to prepare for potential disaster recovery.

-   [Implement Service Manager Disaster Recovery](./Implement-Service-Manager-Disaster-Recovery.md)

    Describes the steps you can take to implement disaster recovery procedures if problems arise.

## Downloadable Documentation
You can download a [copy of this technical documentation from the Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=246620). Always use the TechNet library for the most up\-to\-date information.


