---
title: How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5bc45b16-63f3-4489-b8bd-d4c2bd272aca
author:mgoedtel
manager:cfreemanwa
---
# How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups
You can help decrease the time it takes to diagnose and resolve operating system and application errors in your organization by customizing the data that is collected in error reports by computers experiencing errors and the solution response URL for an error group. The solution response URL can point to an appropriate location in a knowledge base.  
  
### To customize client monitoring data collection and the solution response URL for an error group  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrator role.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the **Monitoring** workspace, expand **Agentless Exception Monitoring**, and then click **Error Group View**.  
  
4.  In the **Error Group View**, select an entry.  
  
5.  In the **Tasks** pane, click **Show or Edit Error Group Properties**.  
  
6.  In the **Error Group Responses** dialog box, select **Custom Collection**, and then click **Edit**.  
  
7.  In the **Diagnostic Data Collection Configuration** dialog box, specify the **Files**, **WMI Queries**, and **Registry Keys** you want to collect from the computers experiencing the error, and then click **OK**. A computer will send the specified data in an error report to the management server on the next occurrence of an error in the error group.  
  
    > [!NOTE]  
    > You can use variables, such as **%ProgramFiles%**, for file paths. For information about WMI, see [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=71799](https://go.microsoft.com/fwlink/?LinkId=71799).  
  
8.  In the **Error Group Responses** dialog box, select **Custom error information**, type the URL for the custom error information, such as **http:\/\/server\/errors\/100.htm**, click **Test Link**, and then click **OK**.  
  
## See Also  
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../../om/manage/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)  
[How to Configure Clients for Client Monitoring](../../om/manage/How-to-Configure-Clients-for-Client-Monitoring.md)  
[How to Configure a Management Server for Client Monitoring](../../om/manage/How-to-Configure-a-Management-Server-for-Client-Monitoring.md)  
[How to Configure Error Transmission Settings for Client Monitoring in Operations Manager](../../om/manage/How-to-Configure-Error-Transmission-Settings-for-Client-Monitoring-in-Operations-Manager.md)  
[Forwarding Client Error Reports &#40;Client Monitoring&#41;](../../om/manage/Forwarding-Client-Error-Reports--Client-Monitoring-.md)  
  
