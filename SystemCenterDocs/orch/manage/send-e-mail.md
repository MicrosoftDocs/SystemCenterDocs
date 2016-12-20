---
title: Send E-Mail
description: The Send E-Mail activity is used in a runbook to send e-mail messages.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30dc0550-1edc-40dc-8bdd-93e2fc10103e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Send E-Mail
===========

Applies To: System Center 2016 - Orchestrator

The Send E-Mail activity is used in a runbook to send e-mail messages.

This activity publishes all of the data from the required and optional properties into published data.

The following tables list the required and optional properties and published data for this activity.

Send E-Mail Required Properties
-------------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the email message to be sent | String   |

Send E-Mail Published Data
--------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address | Address of the Exchange server   | String   |
| ID   | ID of the email message to be sent   | String   |
| Timeout (seconds)   | Connection timeout   | Numbers   |
| Use Autodiscover   | Whether or not the Autodiscover service is being used | Boolean   |
| User Name   | Username to use to connect to the Exchange server   | String   |

#### Other Resources

[Using Runbooks in System Center 2016](https://technet.microsoft.com/en-us/library/hh403791.aspx) <br> <br>
