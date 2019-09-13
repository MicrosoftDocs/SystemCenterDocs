---
ms.assetid:
title: include file
description: Include file to summarize the supported storage arrays for VMM 2019.
author: JYOTHIRMAISURI
ms.author: V-jysur
manager: vvithal
ms.date: 09/12/2019
ms.topic: include
ms.prod: system-center
ms.technology: virtual-machine-manager
---

## Supported storage arrays in VMM 2019


 Virtualized workloads in System Center - Virtual Machine Manager (VMM) need storage resources that meet capacity and performance requirements. VMM recognizes local and remote storage. It supports storage on block-level storage devices that expose logical unit numbers (LUNs) using fiber channel, iSCSCI, and SAS connections, and network file shares.


| **Device** | **Protocol** | **Min Controller Firmware** | **SMI-S** | **Details** |
| --- | --- | --- | --- | --- |
| Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: 3PAR v. 3.2.2 MU3 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000 | SMI-S CIM version 1.5 | [Link](https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=System_Center) |
|NEC / NEC Storage M-Series M510, M710, M710F, M320, M320F|iSCSI/FC |010A <br/><br/>M510/M710 Storage Control Software revision 0973 or later <br/><br/>M320/M320F Storage Control Software revision 1028 or later |SMI-S 1.6.1|[Link](https://www.nec.com/en/global/prod/storage/product/san/index.html)
|DELL <br/><br/> SC Series	| iSCSI/FC	| SCOS: 7.4.2 or later <br/><br/> DSM: 2019 R1 or later <br/><br/> | SMI-S <br/>version 1.6 | [Link](https://www.dell.com/en-us/work/shop/cty/sf/disk-arrays?dgc=IR&cid=emcstorcat&lid=1) |
