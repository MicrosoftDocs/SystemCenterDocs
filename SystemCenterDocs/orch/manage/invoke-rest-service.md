---
title: Invoke REST Service
description: The Invoke REST Service activity is used in a runbook to make requests to RESTful web services and retrieve data or execute functions.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e13d6ae-5c53-48dc-912d-ba132e5eeb11
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Invoke REST Service
===================

Applies To: System Center 2016 - Orchestrator

The Invoke REST Service activity is used in a runbook to make requests to RESTful web services and retrieve data or execute functions.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Invoke REST Service Required Properties
---------------------------------------

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| HTTP Version   | The version of HTTP to use.   | 1.0, 1.1   |
| HTTP Method   | The HTTP method to use.   | The supported HTTP methods are GET, PUT, POST, and DELETE   |
| URL   | The URL to use.   | Any valid URL   |
| Encode URL   | Whether or not to encode the URL.   | True, False   |
| Timeout   | The maximum time to wait for a response.   | Positive integer   |
| Authentication Type   | The authentication scheme to use when connecting to the REST service.   | Default, Basic, Negotiate, Digest   |
| Accept Invalid Certificate | When using HTTPS, set this switch to **True** to accept an invalid server certificate or set it to **False** to not accept it. | True or False   |
| Domain   | The domain to use for authentication.   | String. Can be blank.   |
| User   | The user name to use for authentication.   | String. Can be blank.   |
| Password   | The password to use for authentication.   | String. Can be encrypted. Can be blank.   |
| Request Header   | Special request headers entered in this format:<br>&lt;Parameter&gt;: &lt;Value&gt;   | Valid HTTP request header parameters and values. Can be blank.<br>Each parameter: value pair must be on a separate line. |
| Request Body   | The request body. If not blank, then Payload File Path must be blank.   | String. Can be blank.   |
| Payload File Path   | The location of the payload file to use with the request. If not blank, Request Body must be blank.   | A valid file location. Can be blank.   |
| PFX File Path   | The location of the encrypted client certificate file used for requests to Windows Azure.   | A valid file location. Can be blank.   |
| PFX File Password   | The password to the encrypted file ini .PFX format.   | String. Can be encrypted. Can be blank.   |

Invoke REST Service Optional Properties
---------------------------------------

There are no optional properties for this activity.

Invoke REST Service Published Data
----------------------------------

| **Element**   | **Description**   | **Value type**   |
|:---|:---|:---|
| Accept Invalid Certificate | When using HTTPS, set this switch to **True** to accept an invalid server certificate or set it to **False** to not accept it. | Boolean   |
| Authentication Type   | The authentication scheme to use when connecting to the REST service.   | String   |
| Encode URL   | Whether or not to encode the URL.   | Boolean   |
| HTTP Method   | The HTTP method to use.   | String   |
| HTTP Version   | The version of HTTP to use.   | String   |
| PFX File Path   | The location of the encrypted client certificate file used for requests to Windows Azure.   | String   |
| Payload File Path   | The location of the payload file to use with the request. If not blank, Request Body must be blank.   | String   |
| Request Body   | The request body. If not blank, then Payload File Path must be blank.   | String   |
| Request Header   | Special request headers entered in this format:<br>&lt;Parameter&gt;: &lt;Value&gt;   | String   |
| Response Cookies   | HTTP response cookies.   | String in HTTP response cookie format  |
| Response Header   | HTTP response header.   | String in HTTP response header format  |
| Response Message Body   | HTTP response message body.   | String in HTTP response message format |
| Response Status Code   | The response status code (for example, 200).   | A valid response status code   |
| Response Status Line   | The response status line.   | A valid response status line   |
| Timeout   | The maximum time to wait for a response.   | Integer   |
| URL   | The URL to use.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
