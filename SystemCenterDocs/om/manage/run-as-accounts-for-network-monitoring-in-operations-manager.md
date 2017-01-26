---
title: Run As Accounts for Network Monitoring in Operations Manager
description: This article describes how configure the Run As accounts required to discover network devices in Operations Manager.   
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/25/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: f3631fac-5b64-4903-8343-8254b107db15
---

# Run As accounts for network monitoring in Operations Manager

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager uses Run As accounts to discover and monitor network devices. The credentials in the Run As account enable management servers to communicate with the network devices. You can monitor devices that use SNMP v1, v2, and v3.  
  
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

- Learn [How to discover network devices in Operations Manager](how-to-discover-network-devices-in-operations-manager.md).    

- To understand how to stop monitoring a network device, see [How to Delete or Restore a Network Device in Operations Manager](how-to-delete-or-restore-a-network-device-in-operations-manager.md).    

- To view information about the network devices you are monitoring, see [Viewing Network Devices and Data in Operations Manager](viewing-network-devices-and-data-in-operations-manager.md).  

-  Operations Manager includes several reports that help analyze performance of monitored network devices.  To learn more, see [Reports for network monitoring in Operations Manager](reports-for-network-monitoring-in-operations-manager.md).   
