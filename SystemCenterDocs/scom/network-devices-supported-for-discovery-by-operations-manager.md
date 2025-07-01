---
title: Network Devices Supported for Discovery by Operations Manager
description: This article provides information on how to monitor physical network routers and switches including the interfaces and ports.
author: jyothisuri
ms.author: jsuri
ms.date: 04/09/2025
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 4ef0e1d1-8c39-4480-9ec0-cc6bfa915bbb
---

# Network Devices Supported for Discovery by Operations Manager

System Center - Operations Manager can monitor physical network routers and switches, including the interfaces and ports on those devices, and the virtual local area networks (VLANs) and Hot Standby Router Protocol (HSRP) groups that they participate in, as well as firewalls and load balancers. Operations Manager can monitor network devices that support SNMP, and can provide port monitoring for devices that implement interface MIB (RFC 2863) and MIB-II (RFC 1213) standards.  

Operations Manager provides more detailed processor or memory monitoring for some network devices, which are listed in the [Network Devices with Extended Monitoring Capability spreadsheet](https://www.microsoft.com/download/details.aspx?id=51219). The devices worksheet includes processor and memory columns for each device to indicate whether Operations Manager can provide extended monitoring for either or both aspects for each device.  

## Next steps

To understand how Operations Manager monitors network devices, what requirements must be met and how they align with your management and security policies for network devices, and how to prepare Operations Manager to monitor them, review [Monitoring Networks by using Operations Manager](manage-monitor-networkdevice-overview.md).  
