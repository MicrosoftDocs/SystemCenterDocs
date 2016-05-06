---
title: Disaster Recovery Guide for System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21c80dca-3dee-40bd-b39c-85f28ef1d40c
---
# Disaster Recovery Guide for System Center 2012 - Service Manager
A recovery plan for potential software and equipment failures in your [!INCLUDE[smlong12](./Token/smlong12_md.md)] environment requires a deployment strategy that separates the [!INCLUDE[smshort](./Token/smshort_md.md)] and data warehouse management servers from the computers that host their respective databases. During installation, you must back up the encryption keys on all the management servers, both the Service Manager management server and data warehouse management servers.

|||
|-|-|
|![](/Image/All_Symbols_Cloud.png)|Did you know that Microsoft Azure provides similar functionality in the cloud? Learn more about [Microsoft Azure storage solutions](http://aka.ms/y03tdi).<br /><br />Create a hybrid storage solution in Microsoft Azure:<br />\- [Configure Azure backup for DPM data](http://aka.ms/ao028b)<br />\- [Configure Azure Backup to prepare for back up of Windows Server](http://aka.ms/smvyw8)<br />\- [Learn about Azure backup and how it integrates with your on\-premises DPM environment](http://aka.ms/cw2v0g)|

> [!NOTE]
> The encryption keys on the Service Manager management server and data warehouse management server are different and each must be backed up.

You must also back up the [!INCLUDE[smshort](./Token/smshort_md.md)] databases and your unsealed management packs.

## Disaster recovery topics

-   [Disaster Recovery Scenarios Overview](./Disaster-Recovery-Scenarios-Overview.md)

    Provides an overview of the potential disaster recovery scenarios that are presented in this guide.

-   [Prepare for Service Manager Disaster Recovery](./Prepare-for-Service-Manager-Disaster-Recovery.md)

    Describes the steps you can take to prepare for potential disaster recovery.

-   [Implement Service Manager Disaster Recovery](./Implement-Service-Manager-Disaster-Recovery.md)

    Describes the steps you can take to implement disaster recovery procedures if problems arise.

## Downloadable Documentation
You can download a [copy of this technical documentation from the Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=246620). Always use the TechNet library for the most up\-to\-date information.


