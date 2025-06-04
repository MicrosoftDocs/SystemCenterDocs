---
description: Learn about the components of offline backup in DPM
ms.topic: article
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Overview of offline backup
ms.subservice: data-protection-manager
ms.assetid: 87b6a324-15df-41ae-86a3-546901bdd369
author: jyothisuri
ms.author: jsuri
monikerRange: '>=sc-dpm-2019'
ms.custom: UpdateFrequency2, engagement-fy24
---

# Overview of offline backup in DPM

This article gives an overview of offline backup and the offline backup modes that DPM supports.

Initial full backups to Azure typically transfer large amounts of data online and require more network bandwidth compared to subsequent backups that transfer only incremental changes. Remote offices or datacenters in certain geographies don't always have sufficient network bandwidth. So, these initial backups take several days. During this time, the backups continuously use the same network that was provisioned for applications running in the on-premises datacenter.

DPM supports offline backup, which transfers initial backup data offline without the use of network bandwidth. Offline backup provides a mechanism to copy backup data onto physical storage devices. The devices are then shipped to a nearby Azure datacenter and uploaded onto a Recovery Services vault. This process ensures a robust transfer of backup data without using any network bandwidth.

## Offline backup options

You can do the Offline backup in two modes based on the ownership of the storage devices:

- [Offline backup using Azure Data Box](#offline-backup-using-azure-data-box)
- [Offline backup based using Azure Import/Export service](#offline-backup-using-azure-importexport-service)

## Offline backup using Azure Data Box

This mode is currently supported with the Microsoft Azure Recovery Services (MARS) Agent. This option takes advantage of [Azure Data Box](https://azure.microsoft.com/services/databox/) to ship Microsoft-proprietary, secure, and tamper-resistant transfer appliances with USB connectors to your datacenter or remote office. Backup data is directly written onto these devices. This option saves the effort required to procure your own Azure-compatible disks and connectors or to provision temporary storage as a staging location. Microsoft also handles the end-to-end transfer logistics, which you can track through the Azure portal.

Here's the architecture to depict the movement of backup data.

![Diagram showing the Azure Backup Data Box architecture.](./media/offline-backup-overview/azure-backup-databox-architecture.png)

Here's the summary of the architecture:

- DPM directly copies backup data to these preconfigured devices.
- You can then ship these devices back to an Azure datacenter.
- Azure Data Box copies the data onto a customer-owned storage account.
- Azure Backup automatically copies backup data from the storage account to the designated Recovery Services vault. Incremental online backups are scheduled.

For detailed procedure on how to use the offline backup using Azure Data Box, see [Offline backup using Azure Data Box](offline-seeding-azure-data-box.md).

## Offline backup using Azure Import/Export service

In this scenario, Offline backup is done using the [Azure Import/Export service](/azure/storage/common/storage-import-export-service). You can transfer initial backup data to Azure by using your own Azure-compatible disks and connectors. This approach requires that you provision temporary storage known as the staging location and use prebuilt utilities to format and copy the backup data onto customer-owned disks.

Here's the architecture to depict the movement of backup data.

![Diagram showing Azure Backup Import/Export service architecture.](./media/offline-backup-overview/azure-backup-import-export.png)

Here's the summary of the architecture:

- Instead of sending the backup data over the network, DPM writes the backup data to a staging location.
- The data in the staging location is written to one or more SATA disks by using a custom utility.
- As part of the preparatory work, the utility creates an Azure import job. The SATA drives are shipped to the nearest Azure datacenter and reference the import job to connect the activities.
- At the Azure datacenter, the data on the disks is copied to an Azure storage account.
- Azure Backup copies the backup data from the storage account to the Recovery Services vault. Incremental backups are scheduled.

For detailed procedure on how to use offline backup based on the Azure Import/Export service, see [Offline backup workflow in Azure Backup](offline-backup-workflow.md).

## Offline backup support summary

The following table compares the two available options so that you can make the appropriate choices based on your scenario.

| **Consideration**                                            | **Offline backup based on Azure Data Box**                     | **Offline backup based on the Azure Import/Export service**                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Maximum backup data per device | [Azure Data Box disk](/azure/databox/data-box-disk-overview) - 7.2 TB <br> [Azure Data Box](/azure/databox/data-box-overview) - 80 TB       | 80 TB (up to 10 disks of 8 TB each)                          |
| Security (data, device, and service)                           | [Data](/azure/databox/data-box-security#data-box-data-protection) - AES 256-bit encrypted <br> [Device](/azure/databox/data-box-security#data-box-device-protection) - Rugged case, proprietary, credential-based interface to copy data <br> [Service](/azure/databox/data-box-security#data-box-service-protection) - Protected by Azure security features | Data - BitLocker encrypted                                 |
| Temporary staging location provisioning                     | Not required                                                | More than or equal to the estimated backup data size        |
| Supported regions                                           | [Azure Data Box disk regions](/azure/databox/data-box-disk-overview#region-availability) <br> [Azure Data Box regions](/azure/databox/data-box-disk-overview#region-availability) | [Azure Import/Export service regions](/azure/storage/common/storage-import-export-service#region-availability) |
| Cross-country shipping                                     | Not supported  <br>    Source address and destination Azure datacenter must be in the same country/region* | Supported                                                    |
| Transfer logistics (delivery, transport, pickup)           | Fully Microsoft managed                                     | Customer managed                                            |
| Pricing                                                      | [Azure Data Box pricing](https://azure.microsoft.com/pricing/details/databox/) <br> [Azure Data Box disk pricing](https://azure.microsoft.com/pricing/details/databox/disk/) | [Azure Import/Export service pricing](https://azure.microsoft.com/pricing/details/storage-import-export/) |

> [!NOTE]
> *If your country/region doesn't have an Azure datacenter, you need to ship your disks to an Azure datacenter in another country/region.

## Next steps

- [Offline seeding using Azure Data Box](offline-seeding-azure-data-box.md)
- [Offline seeding using own disk (using Azure Import/Export service)](offline-backup-workflow.md)
