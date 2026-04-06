---
ms.assetid:
title: include file
description: Include file to summarize the supported storage arrays for VMM 2019.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/13/2025
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.update-cycle: 1095-days
---

## Supported storage arrays in VMM 2019


 Virtualized workloads in System Center - Virtual Machine Manager (VMM) need storage resources that meet capacity and performance requirements. VMM recognizes local and remote storage. It supports storage on block-level storage devices that expose logical unit numbers (LUNs) using fiber channel, iSCSCI, and SAS connections, and network file shares.


| **Device** | **Protocol** | **Min Controller Firmware** | **SMI-S** | **Details** |
| --- | --- | --- | --- | --- |
| Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: 3PAR v. 3.2.2 MU3 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000 | SMI-S CIM version 1.5 | [Link](https://www.hpe.com/us/en/storage/3par.html) |
|DELL <br/><br/> SC Series	| iSCSI/FC	| SCOS: 7.4.2 or later <br/><br/> DSM: 2019 R1 or later <br/><br/> DSM 2020 R1 (20.1.1) or later <br/><br/> | SMI-S <br/>version 1.6 | [Link](https://www.dell.com/en-us/work/shop/cty/sf/disk-arrays?dgc=IR&cid=emcstorcat&lid=1) |
|HPE <br/><br/> Primera	| SMI-S	| 4.0.0| 4.0.0 | [Link](https://www.hpe.com/us/en/storage/hpe-primera.html) |
|Pure Storage <br/><br/> FlashArray - X, C, M	| iSCSI/FC	| Purity 5.3.0+ 6.0.0+ and 6.1.0+ |version 1.6.1 | [Link](https://www.purestorage.com/products/nvme/flasharray-x.html) |

>[!NOTE]
>
> **Known issue**: Deletion of thinly provisioned storage volume (LUN) fails for HPE Primera through VMM 2019.
>
>**Workaround**: Delete LUN directly from the array.
