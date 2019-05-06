---
ms.assetid:
title: include file
description: Include file to summarize the supported storage arrays for VMM 2019.
author: JYOTHIRMAISURI
ms.author: V-jysur
manager: vvithal
ms.date: 04/23/2019
ms.topic: include
ms.prod: system-center
ms.technology: virtual-machine-manager
---

## Supported storage arrays in VMM 2019


 Virtualized workloads in System Center - Virtual Machine Manager (VMM) need storage resources that meet capacity and performance requirements. VMM recognizes local and remote storage. It supports storage on block-level storage devices that expose logical unit numbers (LUNs) using fiber channel, iSCSCI, and SAS connections, and network file shares.


| **Device** | **Protocol** | **Min Controller Firmware** | **SMI-S** | **Details** |
| --- | --- | --- | --- | --- |
| Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: 3PAR v. 3.2.2 MU3 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000 | SMI-S CIM version 1.5 | [Link](https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=System_Center) |
| DELL <br/><br/> SC Series | iSCSI/FC | SCOS: 7.4.2 or later <br/><br/> DSM: 2019 R1.10 or later  | SMI-S M version 1.6 | [Link](https://nam06.safelinks.protection.outlook.com/?url=http%3A%2F%2Fwww.dell.com%2Fus%2Fbusiness%2Fp%2Fdell-compellent%3Fdgc%3DIR%26cid%3Demcstorcat%26lid%3D1&data=01%7C01%7Cv-jysur%40microsoft.com%7C18a8d13c93e1490831ce08d6d2056b90%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=DGV9mP3Ex77nqwZpRaRw74WCVNPSmRqz3rbx3BKT45g%3D&reserved=0) |
