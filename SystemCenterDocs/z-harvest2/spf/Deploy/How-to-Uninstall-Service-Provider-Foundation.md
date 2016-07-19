---
title: How to Uninstall Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a5353ec-11e0-45c8-aea9-b4b7419647bd
author:bwren
manager:cfreemanwa
---
# How to Uninstall Service Provider Foundation
When you uninstall [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)], you remove all [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] features, including all web services that are associated with [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
You can also run a silent, unattended, uninstallation. For more information, see [Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md).  
  
You must use a domain user account with administrative privileges on the computers on which you want to uninstall Service Provider Foundation.  
  
If there is a problem with the uninstallation, consult the log files in the **%SYSTEMDRIVE%\\%TEMP%\\** folder in which you want to uninstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
When you uninstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], you can keep or remove the Service Provider Foundation database.  
  
### To uninstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] and all associated web services  
  
1.  On the computer on which [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] is installed, click **Start**, and then click **Control Panel**.  
  
2.  In **Programs**, click **Uninstall a program**.  
  
3.  Under **Name**, right\-click **System Center 2012 R2 Service Provider Foundation** \(or an earlier version\), and then click **Uninstall**.  
  
4.  On the **Summary** page, review your selections and do one of the following:  
  
    -   Click **Previous** to change any selections.  
  
    -   Click **Uninstall** to uninstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
    After you click **Uninstall**, the **Uninstalling web services** page appears and an uninstallation progress indicator appears.  
  
5.  After [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] is uninstalled, on **The selected components were removed successfully** page, click **Close**.  
  
## See Also  
[How to Install Service Provider Foundation for System Center 2012 R2](../../spf/Deploy/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-R2.md)  
[Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Architecture Overview of Service Provider Foundation](../../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
  
