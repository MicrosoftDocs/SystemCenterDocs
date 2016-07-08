---
title: How to Connect to the Web Console
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12dba3ee-d394-4575-8fc0-2c403b2818ed
author:mgoedtel
manager:cfreemanwa
---
# How to Connect to the Web Console
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], the web console provides a monitoring interface for a management group that can be opened on any computer that has connectivity to the web console server. The web console is limited to My Workspace and the Monitoring workspace.  
  
> [!NOTE]  
> You must use Internet Explorer 7, Internet Explorer 8, or Internet Explorer 9 to connect to the Operations Manager web console. In addition, the Operations Manager web console requires that JavaScript be enabled. To enable JavaScript in Internet Explorer, open **Internet Options**, and click the **Security** tab. Select the zone for the web console \(Internet, Local intranet, or Trusted sites\), and then click **Custom level**. Enable **Active scripting**, click **OK**, click **OK**, and then connect to the web console.  
  
The Operations Manager environment must have the web console installed on a management server for users to connect to the web console by using a web browser.  
  
By default, the web console session is limited to 30 minutes. You can change this limit by editing the web.config file \(Program Files\\System Center Operations Manager 2012\\WebConsole\\WebHost\) and changing the autoSignOutInterval value from “30” to a shorter or longer interval, or disable the session limit by changing the value to “0”, as shown in the following example.  
  
```  
<connection autoSignIn=”true” autoSignOutInterval=”0”>  
```  
  
> [!NOTE]  
> After you change the web.config file, you must open a new web console session for the changes to take effect.  
  
### To connect to a web console  
  
-   Open a web browser on any computer and enter **http:\/\/***servername*\/**OperationsManager**, where *servername* is the name of the computer hosting the web console.  
  
For information on installing the web console, see [Deployment Guide for Operations Manager 2012](http://go.microsoft.com/fwlink/p/?LinkID=213291).  
  
## See Also  
[Comparing the Operations Console and Web Console in Operations Manager](../../om/manage/Comparing-the-Operations-Console-and-Web-Console-in-Operations-Manager.md)  
[Using the Monitoring Workspace in Operations Manager](../../om/manage/Using-the-Monitoring-Workspace-in-Operations-Manager.md)  
[Using My Workspace in Operations Manager](../../om/manage/Using-My-Workspace-in-Operations-Manager.md)  
[Managing Alerts](../../om/manage/Managing-Alerts.md)  
  
