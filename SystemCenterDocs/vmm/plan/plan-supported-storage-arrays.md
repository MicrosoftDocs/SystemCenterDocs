---
ms.assetid: Supported storage arrays in VMM 2016
title: Plan VMM deployment
description: This article summarizes suupported storage arrays for VMM 2016
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  12/15/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Supported storage arrays in VMM 2016

>Applies To: System Center 2016 - Virtual Machine Manager


 Virtualized workloads in System Center 2016 - VMM need storage resources to meet capacity and performance requirements. VMM recognizes local and remote storage, and supports the use of block-level storage devices that expose logical unit numbers (LUNs) using fibre channel, iSCSCI, and SAS connections, and the use of network shares for storage.



 **Device** | **Protocol | **Min Controller Firmware** | **SMI-S** | **Details**
 --- | --- | --- | --- | ---
 Hewlett Packard Enterprise<br/><br/> 3PAR | SMI-S | 3PAR: IOS v. 3.2.2 MU2 or later<br/><br/> 3PAR 8000 & 20000, 7000 & 10000: IOS v.3.2.1 or later | SMI-S CIM version 1.5 |
 Tintri<br/><br/> VMstore | SMB | 4.2 and later | Embedded version 2.1 | [Support](https://identity.tintri.com/login?relayState=https://support.tintri.com/)




 ## Next steps

 - [Learn more](../manage/manage-storage-ad-device.md) about configuring storage in the VMM fabric.
 - Learn more about array SMI-S conformance in the [SMI-S Conformance Testing Program](http://www.snia.org/ctp/)
