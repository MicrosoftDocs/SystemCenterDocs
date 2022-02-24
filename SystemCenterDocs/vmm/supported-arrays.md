---
ms.assetid: 0ebd1dcd-cfe8-42ae-9c5f-cd9b91d582f8
title: Supported storage arrays in VMM
description: This article summarizes supported storage arrays for VMM.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 04/15/2021
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Supported storage arrays

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

::: moniker range="<sc-vmm-2019"

 Virtualized workloads in System Center - Virtual Machine Manager (VMM) need storage resources that meet capacity and performance requirements. VMM recognizes local and remote storage. It supports storage on block-level storage devices that expose logical unit numbers (LUNs) using fiber channel, iSCSCI, and SAS connections, and network file shares.

 This article provides a list of supported storage devices for VMM 2016, 1801, 1807.



| **Device** | **Protocol** | **Min Controller Firmware** | **SMI-S** | **Details** |
| --- | --- | --- | --- | --- |
| Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: 3PAR v. 3.2.2 MU3 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000 | SMI-S CIM version 1.5 | [Link](https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=System_Center) |
| Tintri<br/><br/> VMstore | SMB | 4.2 and later | Embedded version 2.1 | [Support](https://identity.tintri.com/login?relayState=https://support.tintri.com/) |
| NEC / NEC Storage M-Series <br/><br/> M310, M510, M710, M310F, M710F, M320, M320F  | iSCSI/FC | Min Controller Firmware: 010A(Storage Control Software Revision 0941 or later) | SMI-S v1.6.1 | [Details](https://www.nec.com/en/global/prod/storage/product/san/index.html) |
|Fujitsu/ETERNUS<br/><br/>DX60 S3, DX60 S4, DX100 S3, DX100 S4, DX200 S3, DX200 S4<br/>DX500 S3, DX500 S4, DX600 S3,  DX600 S4, DX8700 S3, <br/>DX8900 S3, DX8900 S4, DX200F, AF250, AF250 S2, AF650, AF650 S2|iSCSI/FC|V10L60 or later | EMBEDDED SMI-S v1.6.0 | [Storage System ETERNUS](http://www.fujitsu.com/global/products/computing/storage/) |
|DELL-EMC <br/><br/> XtremIO All Flash Array	| iSCSI/FC	| XtremIO XMS Server Versions: 4.2.0 and 4.2.1 | Embedded SMI-S V1.6.1 | [Link](http://www.emc.com/en-us/storage/xtremio/benefits.htm) |
|DELL <br/><br/> SC Series	| iSCSI/FC	| SCOS: 7.2 or later <br/> DSM: 2016 R3 or later <br/><br/> SCOS 7.3.5 or later, DSM 2018 R1.20 or later <br/><br/> SCOS 7.4.x and later, DSM 2020 R1 (20.1.1) or later | SMI-S <br/>version 1.6 | [Link](http://www.dell.com/us/business/p/dell-compellent?dgc=IR&cid=emcstorcat&lid=1) |
|NetApp <br/><br/> FAS	| iSCSI/FC/SMB	| 8.2 and later | Proxy NetApp SMIS Provider 5.2.4 or later | [Link](https://now.netapp.com) |
|Huawei <br/><br/> OceanStor V3 Series	| iSCSI/FC	| V300R006  and later|Huawei SMI-S <br/>version 2.1.01 or later | [Link](https://e.huawei.com/in/products/cloud-computing-dc/storage/massive-storage/mid-range) |
|Huawei <br/><br/> OceanStor Dorado V3 Series	| iSCSI/FC	| V300R001 and later|Huawei SMI-S <br/>version 2.1.01 or later | [Link](http://e.huawei.com/en/products/cloud-computing-dc/storage/unified-storage/dorado-v3) |
|Huawei  <br/><br/> OceanStor V5 Series	| iSCSI/FC	| V500R007  and later |Huawei SMI-S Provider<br/>v 2.1.03 and later | TBA |
|IBM <br/><br/> XIV Storage System Gen3	| iSCSI/FC	| 11.6.0 and later|embedded SMI-S <br/>v1.6.1 | [Link](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/xiv_apicontainer.html) |
|IBM <br/><br/> FlashSystem A9000/A9000R	| iSCSI/FC	| 12.1.0  and later|embedded SMI-S <br/>v1.6.1 | [Link](https://www.ibm.com/support/knowledgecenter/STJKMM_12.1.0/fs9k_kc_api_reference.html) |
|IBM <br/><br/> Spectrum Virtualize Family Product - SAN Volume Controller(SVC)/Storwize V7000, Storwize V5000, IBM FlashSystem V9000	| iSCSI/FC	| 7.8.0 and later|embedded SMI-S <br/>v1.6.1 | [Link](https://www.ibm.com/support/knowledgecenter/STVLF4_7.8.1/spectrum.virtualize.781.doc/svc_sdkintro_215ebp.html) |
|Pure Storage <br/><br/> FlashArray M	| iSCSI/FC	| Purity 4.9 and later|SMI-S <br/>v1.6.1 | [Link](https://support.purestorage.com/Solutions/Microsoft_Platform_Guide/System_Center_Suite/SMI-S_Provider_Guide) |
|DELL-EMC <br/><br/> PS Series | iSCSI	| PS Firmware: v8.1 or later <br/><br/> HIT Kit: v5.1 or later | SMP v5.1| [Link](https://www.microsoft.com/download/details.aspx?id=42295) |

::: moniker-end

::: moniker range="sc-vmm-2019"

This article details the supported arrays for System Center 2019 - Virtual Machine Manager (VMM).

[!INCLUDE [supported-arrays-2019.md](../includes/supported-arrays-2019.md)]

::: moniker-end

## Next steps

 - [Learn more](storage-device.md) about configuring storage in the VMM fabric.
 - Learn more about array SMI-S [Conformance Testing Program](http://www.snia.org/ctp/)
