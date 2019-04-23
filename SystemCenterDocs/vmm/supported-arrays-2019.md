---
ms.assetid: Supported storage arrays in VMM 2016
title: Supported storage arrays in VMM 2016
description: This article summarizes suupported storage arrays for VMM 2016
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 04/23/2019
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
monikerRange: 'sc-vmm-2019'
---

# Supported storage arrays




 Virtualized workloads in System Center - Virtual Machine Manager (VMM) need storage resources that meet capacity and performance requirements. VMM recognizes local and remote storage. It supports storage on block-level storage devices that expose logical unit numbers (LUNs) using fiber channel, iSCSCI, and SAS connections, and network file shares.

 This article provides the details of currently supported storage devices for VMM 2019.


| **Device** | **Protocol** | **Min Controller Firmware** | **SMI-S** | **Details** |
| --- | --- | --- | --- | --- |
| Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: 3PAR v. 3.2.2 MU3 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000 | SMI-S CIM version 1.5 | [Link](https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=System_Center) |


## Next steps

 - [Learn more](storage-device.md) about configuring storage in the VMM fabric.
 - Learn more about array SMI-S [Conformance Testing Program](http://www.snia.org/ctp/).
