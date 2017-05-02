---
title: Disaster recovery for Service Manager
description: Describes the process used for disaster recovery for System Center 2016 - Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21c80dca-3dee-40bd-b39c-85f28ef1d40c
---

# Disaster recovery for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

A recovery plan for potential software and equipment failures in your System Center 2016 - Service Manager environment requires a deployment strategy that separates the Service Manager and data warehouse management servers from the computers that host their respective databases. During installation, you must back up the encryption keys on all the management servers, both the Service Manager management server and data warehouse management servers.  

![cloud symbol](./media/disaster-recovery/disaster-all_symbols_cloud.png)

- Did you know that Microsoft Azure provides similar functionality in the cloud? Learn more about [Microsoft Azure storage solutions](http://aka.ms/y03tdi).
- Create a hybrid storage solution in Microsoft Azure:
    - [Configure Azure backup for DPM data](http://aka.ms/ao028b)
    - [Configure Azure Backup to prepare for back up of Windows Server](http://aka.ms/smvyw8)
    - [Learn about Azure backup and how it integrates with your on\-premises DPM environment](http://aka.ms/cw2v0g)   


> [!NOTE]  
>  The encryption keys on the Service Manager management server and data warehouse management server are different and each must be backed up.  

 You must also back up the Service Manager databases and your unsealed management packs.  

## Service Manager management server  
 You can take two approaches to restoring a failed Service Manager management server. You can replace the management server, or you can promote an additional management server to the primary role if an additional management server exists. The option of replacing the management server or promoting it depends largely on your time frame. If you can bring up another computer quickly, you might choose that option. Otherwise, you can promote an additional management server to the primary role and then add another management server later.  

 Promoting an additional management server involves the following procedures:  

1.  Promote an additional Service Manager management server. For more information, see [How to Promote a Service Manager Management Server](ms-disaster-recovery.md) in this guide.  

2.  When a replacement server is available, install an additional Service Manager management server. For more information, see [How to Install an Additional Management Server](deploy-additional-ms.md).  

 If promoting an additional Service Manager management server is not an option, you have to install a replacement management server. Installing a replacement Service Manager management server involves the following procedures:  

1.  Start with a new computer that has the same computer name as the computer that failed.  

2.  Restore the encryption key that you saved from the original Service Manager management server. For more information, see [How to Restore the Service Manager Encryption Key](ms-disaster-recovery.md) in this guide.  

3.  Install a Service Manager management server. For more information, see [Service Manager Deployment Scenarios](deploy-scenarios.md).  

## Data Warehouse management server  
 Only one recovery scenario is possible for the data warehouse management server: you must install a new data warehouse management server on a computer with the same computer name as the computer that failed. Installing a replacement data warehouse management server involves the following procedures:  

1.  Start with a new computer that has the same computer name as the computer that failed.  

2.  Restore the encryption key that you saved from the original data warehouse management server. For more information, see [How to Restore the Service Manager Encryption Key](ms-disaster-recovery.md) in this guide.  

3.  Install a data warehouse management server. For more information, see [Service Manager Deployment Scenarios](deploy-scenarios.md).  

## Service Manager databases  
 Recovery procedures are the same for both the Service Manager database and the data warehouse database. You use a computer with the same name, and then you restore the Microsoft SQL&nbsp;Server databases using the same instance as the original. Recovery of a Service Manager database and a data warehouse database involves the following procedures:  

1.  Start with a new computer with the same computer name and with the same SQL&nbsp;Server instance as the computer that failed.  

2.  Restore the SQL&nbsp;Server database or databases using the same instance name as the original. For more information, see [Database Recovery in Service Manager](database-recovery.md) in this guide.
