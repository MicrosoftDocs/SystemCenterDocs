---
title: Security for Servers Performing Network Discovery
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7264f94-f3d6-4fa9-977b-4778059926c1
author:mgoedtel
manager:cfreemanwa
---
# Security for Servers Performing Network Discovery
You must ensure the following firewall configuration for network monitoring:  
  
-   All firewalls between the management servers in the resource pool and the network devices need to allow SNMP \(UDP\) and ICMP bi\-directionally, and ports 161 and 162 need to be open bi\-directionally. This includes Windows Firewall on the management server itself.  
  
-   If your network devices are using a port other than 161 and 162, you need to open bi\-directional UDP traffic on these ports as well.  
  
> [!IMPORTANT]  
> Note for customers who used EMC Solutions for Microsoft System Center Operations Manager: EMC Smarts included tools to create an isolation layer to prevent denial of service attacks. In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], you need to protect your network against packet storms by using external tools.  
  
## See Also  
[Monitoring Networks by Using Operations Manager](../../om/manage/Monitoring-Networks-by-Using-Operations-Manager.md)  
[How to Discover Network Devices in Operations Manager](../../om/manage/How-to-Discover-Network-Devices-in-Operations-Manager.md)  
[Network Device Discovery Settings](../../om/manage/Network-Device-Discovery-Settings.md)  
[Run As Accounts for Network Monitoring in Operations Manager](../../om/manage/Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md)  
[How to Delete or Restore a Network Device in Operations Manager](../../om/manage/How-to-Delete-or-Restore-a-Network-Device-in-Operations-Manager.md)  
[Viewing Network Devices and Data in Operations Manager](../../om/manage/Viewing-Network-Devices-and-Data-in-Operations-Manager.md)  
[Tuning Network Monitoring](../../om/manage/Tuning-Network-Monitoring.md)  
[Network Devices Supported for Discovery by Operations Manager](../../om/manage/Network-Devices-Supported-for-Discovery-by-Operations-Manager.md)  
[Reports for Network Monitoring in Operations Manager](../../om/manage/Reports-for-Network-Monitoring-in-Operations-Manager.md)  
  
