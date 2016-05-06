---
title: Web Application Properties
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1eb0d2ce-be9a-4bcf-be18-a2ae9321adbb
---
# Web Application Properties
The following sections describe the settings available for a **Web Application Transaction Monitoring** template in [!INCLUDE[om12short](../Token/om12short_md.md)]. You can set the properties of these requests by using the procedure in [How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md). Each section in this topic represents a tab in the **Web Application Properties** dialog box.

## General Tab
Use the **General** tab to specify the general details of the application. The various options are explained in the following table.

|Item|Description|
|--------|---------------|
|Web Application Name|The name of the application that appears in the Operations console.|
|Description|Optional description of the application that appears in the **Details** pane in the Operations console.|
|Retry Count|Number of times to retry connecting to a site if the first attempt fails.|
|Management Pack|The management pack in which the **Web Application Transaction Monitoring** template is stored. This cannot be changed.|
|Authentication Method|Specifies the authentication method to use for the website. If no authentication is required, select **None**.|
|User Account|The Run As account to use for authenticating on the site. Only existing accounts that match the selected authentication method are listed. For more information about Run As accounts, see [Managing Run As Accounts and Profiles](../Topic/Managing-Run-As-Accounts-and-Profiles.md).|
|Use a proxy server to connect|Select this option if the watcher nodes must connect to the website through a proxy server.|
|Address|The address of the proxy server if one is required.|
|Port|The port for the proxy server if one is required.|
|Authentication Method|Specifies the authentication method to use for the proxy server. If no authentication is required, select **None**.|
|User Account|The Run As account to use for authenticating on the proxy server. Only existing accounts that match the selected authentication method are listed. For more information about Run As accounts, see [Managing Run As Accounts and Profiles](../Topic/Managing-Run-As-Accounts-and-Profiles.md).|

## Watcher Node Tab
Use the **Watcher Node** tab to specify the watcher nodes that you want to use for this web application and the frequency that you want to run the web application. For more information about watcher nodes, see [Watcher Nodes](../Topic/Watcher-Nodes.md).

## Performance Criteria Tab
Use the **Performance Criteria** tab to enable the **Transaction response time** monitor for the application that monitors for the transaction time of all of the requests in the browser session. The various options are explained in the following table.

|Item|Description|
|--------|---------------|
|Error Transaction Response Time|Select this option and provide a criteria and number of seconds if you want to monitor for a critical state. If the time to process the complete set of requests matches this criteria, the monitor is set to a critical state.|
|Warning Transaction Response Time|Select this option and provide a criteria and number of seconds if you want to monitor for a warning state. If the time to process the complete set of requests matches this criteria, and the error criteria is not also true, the monitor is set to a warning state.|

## Performance Counter Tab
Use the **Performance Counter** tab to enable collection of performance counters for the web application. The various options are explained in the following table.

|Item|Description|
|--------|---------------|
|Transaction Response Time|If this option is selected, then the collective time to process all the requests in the browser session is collected.|
|Request Performance Counters|Select the performance counters that are collected for the application. Any selected counters are collected as an aggregate for all requests in the browser session. Each will also be added to the list of counters for every request in the browser session.|
|Reduction Factor|Select to reduce the number of counters selected for the web application and the requests. It specifies how many query intervals must be completed before each collection. If the value is 1, the counters are collected every time  the browser session is run. If it is 2, the counters are only collected every second time the browser session is run, and so on.|

## See Also
[How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md)
[Web Application Request Properties](../Topic/Web-Application-Request-Properties.md)

