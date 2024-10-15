---
title: Run As Accounts for Network Monitoring in Operations Manager
description: This article describes how to configure the Run As accounts required to discover network devices in Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: f3631fac-5b64-4903-8343-8254b107db15
---

# Run As accounts for network monitoring in Operations Manager



System Center - Operations Manager uses Run As accounts to discover and monitor network devices. The information you include in the Run As account enables management servers to communicate with the network devices. You can monitor devices that use SNMP v1, v2, and v3.  

Network devices that use SNMP v1 or v2 require a Run As account that specifies a community string, which acts like a password to provide read-only access to the device.  

Each network device that uses SNMP v3 requires a unique Run As account that provides the following credentials:  

-   User name: Obtained from device configuration.  

-   Context: Name that together with the user name determines the access permissions of a request sent to the SNMPv3 agent.  

-   Authentication protocol: MD5 for Message Digest 5, SHA for Secure Hash Algorithm, or NONE  

-   Authentication key: String consisting of 1 to 64 characters; required if the authentication protocol is MD5 or SHA  

-   Privacy protocol: DES for Data Encryption Standard, AES for Advanced Encryption Standard, or NONE  

-   Privacy key: String consisting of 1 to 64 characters; required if the privacy protocol is DES or AES  

    > [!NOTE]  
    > The authentication key and privacy key are masked as you enter them.  

You can create the required Run As accounts when you create a network devices discovery rule, or you can create the Run As accounts beforehand and then select the appropriate account when you create the discovery rule.  

Two Run As profiles are created when you install Operations Manager: SNMP Monitoring Account and SNMPv3 Monitoring Account. When you create a discovery rule, the Run As accounts you create for network device discovery are automatically associated with the appropriate Run As profile.  

## Next steps

- Learn [How to discover network devices in Operations Manager](manage-monitor-networkdevice-overview.md).

- To understand how to stop monitoring a network device, see [How to Delete or Restore a Network Device in Operations Manager](manage-monitor-networkdevice-delete-restore.md).

- To view information about the network devices you're monitoring, see [Viewing Network Devices and Data in Operations Manager](manage-monitor-networkdevice-viewing-data.md).  

- Operations Manager includes several reports that help analyze performance of monitored network devices. To learn more, see [Reports for network monitoring in Operations Manager](manage-monitor-networkdevice-reports.md).
