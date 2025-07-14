---
ms.assetid: 5c187754-29e7-41a8-ae85-cb2d1514b0a4
title: Web Application Transaction Monitoring template in Operations Manager management pack
description: This article provides an overview of web application transaction monitoring template.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Web Application Transaction Monitoring template



The _Web Application Transaction Monitoring_ template lets you test a website or web-based application by sending requests over HTTP, validating their response, and measuring their performance. This can be a simple test to determine if the website is responding, or it can be a complex set of requests to simulate a user who is performing such actions as signing in to the site and browsing through a set of pages.

The HTTP requests are sent from one or more [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29). The website that's being monitored can reside on any computer whether it has an agent for Operations Manager installed. It can be an external website, but it must be accessible from the watcher nodes. Each watcher node must have an Operations Manager agent installed.

## Scenarios

Use the  **Web Application Transition Monitoring**  template for monitoring the availability and performance of any website or web-based application to test both general availability and functionality. For internal websites, you can use watcher nodes in different network segments to ensure that the site is available to each segment.

In addition to general availability, you can check the functionality of the website by testing different pages and features. For example, you could check a sign-in process by performing a test sign-in with a test user account every few minutes. You could test the functionality of a search page by performing a sample search after the test user account is signed in. You can then analyze the HTML that's returned from these pages to verify whether the page functioned as expected. In addition to testing this functionality, you can analyze the time it takes to fill the request to measure the performance.

## Web Application Transaction Monitoring template articles

The  **Web Application Transaction Monitoring**  is more complex than the other management pack templates and supports various monitoring scenarios. The following articles provide details on the different tools and procedures that you can use for different scenarios.

- [How to Create a Single URL Web Application Monitor](/previous-versions/system-center/system-center-2012-R2/hh457541%28v%3dsc.12%29)

   This procedure explains how to run the _Web Application Transaction Monitoring_ wizard to create a simple  **Web Application Transaction Monitoring**  template that monitors a single URL. You can either use this simple monitor with no modification or insert additional requests once it's completed.

- [How to Capture Web Application Recording](/previous-versions/system-center/system-center-2012-R2/hh457597%28v%3dsc.12%29)

   This procedure explains how to use the  **Web Recorder**  to record a browser session with multiple requests. You can either use this session with no modification or edit the application and request settings once it's completed.

- [How to Edit Settings or Requests in a Web Application](/previous-versions/system-center/system-center-2012-R2/hh457602%28v%3dsc.12%29)

   This article includes procedures for editing a web application and its contained requests and for creating additional requests in an existing template.

- [How to Replace Parameters in a URL Request](how-to-replace-parameters-url-request.md)

   This article includes a method to retrieve information from one request and use it in a subsequent request.
