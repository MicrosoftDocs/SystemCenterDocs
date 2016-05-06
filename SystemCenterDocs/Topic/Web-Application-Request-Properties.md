---
title: Web Application Request Properties
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f867812b-cdde-4d6e-8e05-7cfec9f88cb8
---
# Web Application Request Properties
The following sections describe the settings available for each request in a **Web Application Transaction Monitor** template in [!INCLUDE[om12short](../Token/om12short_md.md)]. You can set the properties of these requests by using the procedure in [How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md). Each section in the following sections represents a tab in the **Request Properties** dialog box.

## General Tab
Use the **General** tab to specify the general details of the request. The different options are explained in the following table.

|Item|Description|
|--------|---------------|
|Request URL|The URL that you are requesting. You can specify whether the protocol will be http or https.|
|HTTP Method|The method to use for the request. Most requests use a GET method. The POST method is typically used when selecting an option to submit information to a website, such as clicking a button to submit a name and password.|
|HTTP Version|The version of HTTP that the request specifies to the receiving website.|
|Request Body|Only enabled when the **HTTP method** is POST. This is the body of the request that the post submits.|
|Insert Parameter|There is an **Insert parameter** button for both the **Request URL** and the **Request Body**. Use these options to replace part of the text with a variable that is populated from a previous request. For more information, see [How to Replace Parameters in a URL Request](../Topic/How-to-Replace-Parameters-in-a-URL-Request.md).|

## HTTP Headers Tab
The **HTTP Headers** tab is used to define the different fields that will be included in the header of the request. If the request is from a recorded session, it includes the headers that your browser used. If you manually created the request, it includes a default set of headers and values. You can use the **Edit** button to modify an existing header field or the **Add** button to add a new field. The **Insert parameter** options are used to replace part of the text with a variable that is populated from a previous request. For more information, see [How to Replace Parameters in a URL Request](../Topic/How-to-Replace-Parameters-in-a-URL-Request.md).

## Performance Counter Tab
The **Performance Counter** tab lets you select the performance counters that will be collected for the request. Any selected counters are added to the list of counters specified in the **Web Application** settings which enable the counter for an aggregate of all requests in a browser session. The value for any selected counter is collected every time that the request is made.

## Monitoring
Use the **Monitoring** tab to control certain monitoring settings for the request and to specify the details of the request that will be collected when one of the monitors enters a warning or critical state. You can view this collected information in the **State Change Events** tab of the **Health Explorer** for the monitor. The different options are described in the following table.

|Item|Description|
|--------|---------------|
|Monitor SSL health on secure sites|If the request is using https, monitors that measure the health of the related Secure Sockets Layer \(SSL\) certificates.|
|Enable health evaluation and performance collection for resources|If selected, a monitor is enabled that displays the status of the resources for the page. Instead of measuring every resource, the total of all resources is evaluated. If this option is not selected, the resource monitor does not function for the request.|
|Enable health evaluation and performance collection for Internal links|Enables the collection of the status of each internal link and includes internal links in the evaluation of the **Links Status Code** monitor for the request. An internal link is a link that refers to a location on the same page.|
|Enable health evaluation and performance collection for External Links|Enables the collection of the status of each external link and includes external links in the evaluation of the **Links Status Code** monitor for the request. An external link is a link that refers to a location outside the current page.|
|Link traversal|Specifies the number of levels of external links to collect. If the value is 0, only the links on the page itself are evaluated. If the value is 1, the links on each target page are evaluated. If the value is 2, the links on those target pages are evaluated, and so on.|
|Process response body|Specifies whether to evaluate the response body. You must select this value if you want to use content matching or parameter extraction for the request to work. You can clear this option if you only want to perform simple tests for the page such as monitoring status code and response time.|
|Response body collection|Specifies whether to collect the body of the request response. Select one of the following options:<br /><br />-   **Always collect** if you want to collect the response body any time any monitor for the request enters a warning or error state.<br />-   **Do not collect** if you never want to collect the response body.<br />-   **Collect on content match criteria** if you want to collect the response body only when the Content Match monitor enters a warning or critical state.|
|Collect headers|If selected, the header of the request is collected.|
|Collect link headers|If selected, the header of each link is collected.|
|Collect resource headers|If selected, the header of each resource is collected.|

## Custom Error
The **Custom Error** tab lets you specify error criteria for the request by using information that is not available in the **Request Details** pane of the **Web Application Editor**. You can either provide simple criteria by using a single metric, or you can use multiple metrics to specify complex logic. Use the **Insert** button to add a criterion or a group specifying **AND** or **OR** logic. If the criteria that you specify resolve to `true` when the request is run, the monitor indicates an error for the web application.

## Custom Warning
The **Custom Warning** tab lets you specify error criteria for the request by using information that is not available in the **Request Details** pane of the **Web Application Editor**. You can either provide simple criteria by using a single metric, or you can use multiple metrics to specify complex logic. Use the **Insert** button to add a criterion or a group specifying **AND** or **OR** logic. If the criteria that you specify resolve to `true` when the request is run, the monitor indicates a warning for the web application.

## Extraction Rules
The **Extraction Rules** tab lets you extract a string of text from the body of the response of the request to use in one or more subsequent requests. For more information, see [How to Replace Parameters in a URL Request](../Topic/How-to-Replace-Parameters-in-a-URL-Request.md).

## See Also
[How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md)
[Web Application Properties](../Topic/Web-Application-Properties.md)

