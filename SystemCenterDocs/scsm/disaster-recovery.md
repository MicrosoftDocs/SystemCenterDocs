---
title: Disaster recovery for Service Manager
description: Describes the process used for disaster recovery for System Center - Service Manager.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Disaster recovery for System Center - Service Manager



A recovery plan for potential software and equipment failures in your System Center - Service Manager environment requires a deployment strategy that separates the Service Manager and data warehouse management servers from the computers that host their respective databases. During installation, you must back up the encryption keys on all the management servers, both the Service Manager management server and data warehouse management servers.  

![Screenshot of the cloud symbol.](./media/disaster-recovery/disaster-all_symbols_cloud.png)

- Did you know that Microsoft Azure provides similar functionality in the cloud? Learn more about [Microsoft Azure storage solutions](https://aka.ms/y03tdi).
- Create a hybrid storage solution in Microsoft Azure:
    - [Configure Azure backup for DPM data](/previous-versions/system-center/system-center-2012-R2/jj728752(v=sc.12)).
    - [Configure Azure Backup to prepare for back up of Windows Server](/azure/backup/backup-windows-with-mars-agent).
    - [Learn about Azure backup and how it integrates with your on\-premises DPM environment](/azure/backup/backup-overview).

> [!NOTE]  
> The encryption keys on the Service Manager management server and data warehouse management server are different and each must be backed up.  

 You must also back up the Service Manager databases and your unsealed management packs.  

## Service Manager management server

You can take two approaches to restoring a failed Service Manager management server. You can replace the management server, or you can promote an additional management server to the primary role if an additional management server exists. The option of replacing the management server or promoting it depends largely on your time frame. If you can bring up another computer quickly, you might choose that option. Otherwise, you can promote an additional management server to the primary role and then add another management server later.  

Promoting an additional management server involves the following procedures:  

1. Promote an additional Service Manager management server. For more information, see [How to Promote a Service Manager Management Server](./implement-disaster-recovery.md) in this guide.  

2. When a replacement server is available, install an additional Service Manager management server. For more information, see [How to Install an Additional Management Server](deploy-additional-ms.md).  

   If promoting an additional Service Manager management server isn't an option, you've to install a replacement management server. Installing a replacement Service Manager management server involves the following procedures:  

3. Start with a new computer that has the same computer name as the computer that failed.  

4. Restore the encryption key that you saved from the original Service Manager management server. For more information, see [How to Restore the Service Manager Encryption Key](./implement-disaster-recovery.md) in this guide.  

5. Install a Service Manager management server. For more information, see [Service Manager Deployment Scenarios](deploy-scenarios.md).  

## Data Warehouse management server

Only one recovery scenario is possible for the data warehouse management server: you must install a new data warehouse management server on a computer with the same computer name as the computer that failed. Installing a replacement data warehouse management server involves the following procedures:  

1. Start with a new computer that has the same computer name as the computer that failed.  

2. Restore the encryption key that you saved from the original data warehouse management server. For more information, see [How to Restore the Service Manager Encryption Key](./implement-disaster-recovery.md) in this guide.  

3. Install a data warehouse management server. For more information, see [Service Manager Deployment Scenarios](deploy-scenarios.md).  

## Service Manager databases

Recovery procedures are the same for both the Service Manager database and the data warehouse database. You use a computer with the same name, and then you restore the Microsoft SQL&nbsp;Server databases using the same instance as the original. Recovery of a Service Manager database and a data warehouse database involves the following procedures:  

1. Start with a new computer with the same computer name and with the same SQL&nbsp;Server instance as the computer that failed.  

2. Restore the SQL&nbsp;Server database or databases using the same instance name as the original. For more information, see [Database Recovery in Service Manager](./implement-disaster-recovery.md) in this guide.

## Next steps

- [Prepare for Service Manager disaster recovery](prepare-disaster-recovery.md).
