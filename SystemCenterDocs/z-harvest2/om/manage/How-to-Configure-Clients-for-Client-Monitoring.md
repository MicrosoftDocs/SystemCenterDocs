---
title: How to Configure Clients for Client Monitoring
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec0035ba-4997-4340-88f1-05565b4ea796
author:mgoedtel
manager:cfreemanwa
---
# How to Configure Clients for Client Monitoring
This topic provides the procedure to configure clients for the Client Monitoring feature of [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)].  
  
> [!IMPORTANT]  
> You must first configure a management server for the server component of Client Monitoring by running the Client Monitoring Configuration Wizard. For more information, see [How to Configure a Management Server for Client Monitoring](../../om/manage/How-to-Configure-a-Management-Server-for-Client-Monitoring.md).  
  
### To configure clients for Client Monitoring in Operations Manager  
  
1.  Run the Group Policy Object Editor \(gpedit.msc\) for the domain or local computer.  
  
    > [!NOTE]  
    > For information about Group Policy, see [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=156845](http://go.microsoft.com/fwlink/?LinkId=156845).  
  
2.  If needed, disable the **Turn off Windows Error Reporting** policy. This policy can be found in Computer Configuration\/Administrative Templates\/System\/Internet Communication Management\/Internet Communication settings.  
  
3.  Add the Agentless Exception Monitoring \(AEM\) Group Policy administrative template \(*ServerName*.ADM\) to the domain or local computer policy. The ADM file is created when the Client Monitoring Configuration Wizard is run.  
  
    > [!NOTE]  
    > Use the same procedure to **Disable** the Group Policy settings, thereby disabling Client Monitoring on the clients.  
  
## See Also  
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../../om/manage/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)  
[How to Configure a Management Server for Client Monitoring](../../om/manage/How-to-Configure-a-Management-Server-for-Client-Monitoring.md)  
[How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups](../../om/manage/How-to-Customize-Client-Monitoring-Data-Collection-and-Solution-Response-URLs-for-Error-Groups.md)  
[How to Configure Error Transmission Settings for Client Monitoring in Operations Manager](../../om/manage/How-to-Configure-Error-Transmission-Settings-for-Client-Monitoring-in-Operations-Manager.md)  
[Forwarding Client Error Reports &#40;Client Monitoring&#41;](../../om/manage/Forwarding-Client-Error-Reports--Client-Monitoring-.md)  
  
