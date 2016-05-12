---
title: Web Application Transaction Monitoring Template_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8e1d1cf-7a9c-4274-8027-8bc0b0856e45
---
# Web Application Transaction Monitoring Template_1
The *Web Application Transaction Monitoring* template lets you test a website or web\-based application by sending requests over HTTP, validating their response, and measuring their performance. This can be a simple test to determine if the website is responding, or it can be a complex set of requests to simulate a user who is performing such actions as logging on to the site and browsing through a set of pages.

The HTTP requests are sent from one or more [Watcher Nodes](Watcher-Nodes.md). The website that is being monitored can reside on any computer whether it has an agent for [!INCLUDE[om12short](Token/om12short_md.md)] installed. It can be an external website, but it must be accessible from the watcher nodes. Each watcher node must have an [!INCLUDE[om12short](Token/om12short_md.md)] agent installed.

## Scenarios
Use the **Web Application Transition Monitoring** template for monitoring the availability and performance of any website or web\-based application to test both general availability and functionality. For internal websites, you can use watcher nodes in different network segments to ensure that the site is available to each segment.

In addition to general availability, you can check the functionality of the website by testing different pages and features. For example, you could check a logon process by performing a test logon with a test user account every few minutes. You could test the functionality of a search page by performing a sample search after the test user account is logged on. You can then analyze the HTML that is returned from these pages to verify whether the page functioned as expected. In addition to testing this functionality, you can analyze the time it takes to fill the request to measure the performance.

## Web Application Transaction Monitoring Template Topics
The **Web Application Transaction Monitoring** is more complex than the other management pack templates and supports a variety of monitoring scenarios. The following topics provide details on the different tools and procedures that you can use for different scenarios.

-   [How to Create a Single URL Web Application Monitor](How-to-Create-a-Single-URL-Web-Application-Monitor.md)

    This procedure explains how to run the *Web Application Transaction Monitoring* wizard to create a simple **Web Application Transaction Monitoring** template that monitors a single URL. You can either use this simple monitor with no modification or insert additional requests once it is completed.

-   [How to Capture Web Application Recording](How-to-Capture-Web-Application-Recording.md)

-   This procedure explains how to use the **Web Recorder** to record a browser session with multiple requests. You can either use this session with no modification or edit the application and request settings once it is completed.

-   [How to Edit Settings or Requests in a Web Application](How-to-Edit-Settings-or-Requests-in-a-Web-Application.md)

    This topic includes procedures for editing a web application and its contained requests and for creating additional requests in an existing template.

-   [How to Replace Parameters in a URL Request](How-to-Replace-Parameters-in-a-URL-Request.md)

-   This topic includes a method to retrieve information from one request and use it in a subsequent request.


