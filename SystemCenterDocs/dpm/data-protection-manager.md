---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-09-09
title:  Data Protection Manager
ms.technology:  data-protection-manager
ms.assetid:  ee706e89-20fd-4883-82e3-75565a705751
---

# Data Protection Manager

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

Your organization needs a BCDR strategy to make sure that resources are available during planned and unplanned outages, and that you're able to recover to normal working conditions when things go wrong. Your BCDR strategy revolves broadly around keeping your data safe and recoverable, and keeping your business workloads, applications, and services continuously available. System Center Data Protection Manager (DPM) is an robust enterprise backup and recovery system that contributes to your BCDR strategy by facilitating the backup and recovery of enterprise data.

You can deploy DPM for:

-   **Application-aware backup**: Application-aware backup of Microsoft workloads, including SQL Server, Exchange, and SharePoint.

-   **File backup**: Back up of files, folders and volumes for computers running Windows server and Windows client operating systems.

-   **System backup**: Back up system state or full bare metal backup for physical computers running Windows server and Windows client operating systems.

-   **Hyper-V backup**: Back up of Hyper-V virtual machines running Windows or Linux. You can back up an entire VM, or run application-aware backups of Microsoft workloads on Hyper-V VMs running Windows.

-   Get a full list in [What can DPM back up?](get-started/What-can-DPM-back-up-.md)

DPM stores back up data as follows:

-   **Disk**: For short-term storage DPM backs up data to disk pools.

-   **Azure**: For both short-term and long-term storage off-premises, DPM data stored in disk pools can be backed up to the Microsoft Azure cloud using the Azure Backup service.

-   **Tape**: For long-term storage you can back up data to tape, which can then be stored offsite.

When outages occur and source data is unavailable, you can easily restore data to the original source or to an alternate location. Then if the original data is unavailable because of planned or unexpected issues, you can easily restore data. DPM uses SQL Server as its database and you protect the DPM server itself for disaster recovery purposes. The following diagram provides an overview of DPM backup functionality.

![](../Media/DPM-backup.png)

## Next steps
Learn more in [How does DPM work?](get-started/How-does-DPM-work-.md)
