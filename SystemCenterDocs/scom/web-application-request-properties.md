---
ms.assetid: 4380f888-a7fa-4913-8715-9f1f524d4590
title: Web Application Request Properties
description: This article provides information about how to manage the web application requests properties in Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 04/21/2025
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
monikerRange: '>=sc-om-2019'
ms.custom: UpdateFrequency3, engagement-fy24
---

# Web Application Request Properties

This article provides information about how to manage the web application requests properties in Operations Manager.

The following sections describe the settings available for each request in a **Web Application Transaction Monitor** template in Operations Manager. You can set the properties of these requests by using the procedure in [Edit Settings or Requests in a Web Application](edit-web-application-settings.md). Each section in the following sections represents a tab in the **Request Properties** window.

## General tab

Use the **General** tab to specify the general details of the request. The different options are explained in the following table.

| **Item** | **Description** |
| --- | --- |
| Request URL | The URL that you're requesting. You can specify whether the protocol will be http or https. |
| HTTP Method | The method to use for the request. Most requests use a GET method. The POST method is typically used when selecting an option to submit information to a website, such as clicking a button to submit a name and password. |
| HTTP Version | The version of HTTP that the request specifies to the receiving website. |
| Request Body | Only enabled when the **HTTP method** is POST. This is the body of the request that the post submits. |
| Insert Parameter | There's an **Insert parameter** button for both the **Request URL**  and the **Request Body**. Use these options to replace part of the text with a variable that is populated from a previous request. For more information, see [Replace Parameters in a URL Request](/previous-versions/system-center/system-center-2012-R2/hh457573%28v%3dsc.12%29). |

## HTTP headers tab

The **HTTP Headers** tab is used to define the different fields that will be included in the header of the request. If the request is from a recorded session, it includes the headers that your browser used. If you manually created the request, it includes a default set of headers and values. You can use the  **Edit**  button to modify an existing header field or the **Add** button to add a new field. The **Insert parameter** options are used to replace part of the text with a variable that is populated from a previous request. For more information, see [Replace Parameters in a URL Request](/previous-versions/system-center/system-center-2012-R2/hh457573%28v%3dsc.12%29).

## Performance counter tab

The **Performance Counter** tab lets you select the performance counters that will be collected for the request. Any selected counters are added to the list of counters specified in the **Web Application** settings, which enable the counter for an aggregate of all requests in a browser session. The value for any selected counter is collected every time the request is made.

## Monitoring

Use the **Monitoring** tab to control certain monitoring settings for the request and to specify the details of the request that will be collected when one of the monitors enters a warning or critical state. You can view this collected information in the **State Change Events** tab of the **Health Explorer** for the monitor. The different options are described in the following table.

| **Item** | **Description** |
| --- | --- |
| Monitor SSL health on secure sites | If the request is using https, monitors that measure the health of the related Secure Sockets Layer (SSL) certificates. |
| Enable health evaluation and performance collection for resources | If selected, a monitor is enabled that displays the status of the resources for the page. Instead of measuring every resource, the total of all resources is evaluated. If this option isn't selected, the resource monitor doesn't function for the request. |
| Enable health evaluation and performance collection for Internal links | Enables the collection of the status of each internal link and includes internal links in the evaluation of the **Links Status Code** monitor for the request. An internal link is a link that refers to a location on the same page. |
| Enable health evaluation and performance collection for External Links | Enables the collection of the status of each external link and includes external links in the evaluation of the **Links Status Code** monitor for the request. An external link is a link that refers to a location outside the current page. |
| Link traversal | Specifies the number of levels of external links to collect. If the value is 0, only the links on the page itself are evaluated. If the value is 1, the links on each target page are evaluated. If the value is 2, the links on those target pages are evaluated, and so on. |
| Process response body | Specifies whether to evaluate the response body. You must select this value if you want to use content matching or parameter extraction for the request to work. You can clear this option if you only want to perform simple tests for the page such as monitoring status code and response time. |
| Response body collection | Specifies whether to collect the body of the request response. Select one of the following options:<br>**Always collect** if you want to collect the response body any time any monitor for the request enters a warning or error state.<br>**Do not collect** if you never want to collect the response body.<br>**Collect on content match criteria** if you want to collect the response body only when the Content Match monitor enters a warning or critical state.|
| Collect headers | If selected, the header of the request is collected. |
| Collect link headers | If selected, the header of each link is collected. |
| Collect resource headers | If selected, the header of each resource is collected. |

## Custom error

The **Custom Error** tab lets you specify error criteria for the request by using information that isn't available in the **Request Details** pane of the **Web Application Editor**. You can either provide simple criteria by using a single metric, or you can use multiple metrics to specify complex logic. Click the **Insert** button to add a criterion or a group specifying **AND** or **OR** logic. If the criteria that you specify resolve to true when the request is run, the monitor indicates an error for the web application.

## Custom warning

The **Custom Warning** tab lets you specify error criteria for the request by using information that isn't available in the **Request Details** pane of the **Web Application Editor**. You can either provide simple criteria by using a single metric, or you can use multiple metrics to specify complex logic. Click the **Insert** button to add a criterion or a group specifying **AND** or **OR** logic. If the criteria that you specify resolve to true when the request is run, the monitor indicates a warning for the web application.

## Extraction rules

The **Extraction Rules** tab lets you extract a string of text from the body of the response of the request to use in one or more subsequent requests. For more information, see [Replace Parameters in a URL Request](/previous-versions/system-center/system-center-2012-R2/hh457573%28v%3dsc.12%29).

## Next steps

- [Edit Settings or Requests in a Web Application](edit-web-application-settings.md).
- [Web Application Properties](web-application-properties.md).
