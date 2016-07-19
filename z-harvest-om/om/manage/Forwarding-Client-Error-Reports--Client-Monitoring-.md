---
title: Forwarding Client Error Reports (Client Monitoring)
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08d6365a-4a44-4c84-ac6d-b04291f45403
author:mgoedtel
manager:cfreemanwa
---
# Forwarding Client Error Reports (Client Monitoring)
The Microsoft Customer Experience Improvement Program \(CEIP\) collects information about how you use Microsoft programs and about some of the issues you might encounter. Microsoft uses this information to improve the products and features you use most often and to help solve issues. Participation in the program is strictly voluntary.  
  
When you choose to participate in the CEIP, you configure clients with Group Policy to redirect CEIP reports to a [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] management server, instead of reporting directly to Microsoft. The management servers are configured to forward these reports to Microsoft.  
  
> [!IMPORTANT]  
> The CEIP reports do not contain contact information about you or your organization, such as names or an address.  
  
The CEIP reports forwarded from your organization to Microsoft are combined with CEIP reports from other organizations and individual customers to help Microsoft solve issues and improve the Microsoft products and features that customers use most often. For more information about the CEIP, see [the CEIP page](http://go.microsoft.com/fwlink/p/?linkid=75040).  
  
Use the following procedure to configure CEIP settings. The management server must have access to the Internet to participate in the program.  
  
> [!IMPORTANT]  
> CEIP is a component of the Client Monitoring feature of [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)]. Client Monitoring must be enabled on at least one management server and managed computers to participate in the CEIP. For information about enabling the Client Monitoring feature of [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)], see [Client Monitoring Using Agentless Exception Monitoring](http://go.microsoft.com/fwlink/?LinkID=217096). After a management server has been configured for client monitoring, all agents that are participating in CEIP should be configured via Group Policy to send their CEIP data to that management server.  
  
### To configure the CEIP settings for Operations Manager  
  
1.  Log on to a management server with an account that is a member of the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] Administrators role for the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management group.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the **Administration** workspace, expand **Administration**, and then click **Settings**.  
  
4.  In **Settings**, expand **Type: General**, right\-click **Privacy**, and then click **Properties**.  
  
5.  In the **Global Management Server Group Settings \- Privacy** dialog box, on the  **CEIP** tab, click **Join the Customer Experience Improvement Program \(recommended\)** to join the CEIP program or click **I don't want to join the program at this time** to decline participation. Then click **OK**.  
  
    > [!NOTE]  
    > You can click **Tell me more about the program** to view information about the CEIP program, including the privacy statement.  
  
## See Also  
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../../om/manage/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)  
[How to Configure Clients for Client Monitoring](../../om/manage/How-to-Configure-Clients-for-Client-Monitoring.md)  
[How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups](../../om/manage/How-to-Customize-Client-Monitoring-Data-Collection-and-Solution-Response-URLs-for-Error-Groups.md)  
[How to Configure Error Transmission Settings for Client Monitoring in Operations Manager](../../om/manage/How-to-Configure-Error-Transmission-Settings-for-Client-Monitoring-in-Operations-Manager.md)  
[How to Configure a Management Server for Client Monitoring](../../om/manage/How-to-Configure-a-Management-Server-for-Client-Monitoring.md)  
  
