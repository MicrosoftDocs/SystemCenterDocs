---
title: Reply To E-Mail
description: The Reply To E-Mail activity is used in a runbook to reply to email messages.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a81c1b1-081b-4b2d-b292-90030263fd96
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Reply To E-Mail
===============

Applies To: System Center 2016 - Orchestrator

The Reply To E-Mail activity is used in a runbook to reply to email messages.

The following tables list the required properties, optional properties, and published data for this activity.

Reply To E-Mail Required Properties
-----------------------------------

| **Element**  | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the existing e-mail message to reply to   | String   |
| Reply To All | Indicates whether the response should be sent to all recipients of the original message   | True<br>False   |
| Body Prefix  | The prefix that will be prepended to the original message's body when the reply is created | String   |

Reply To E-Mail Optional Properties
-----------------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Body Type   | Indicates the format of the email message body   | Text<br>Html   |
| Cc   | List of addresses the response will be sent to as Cc recipients  | String   |
| Bcc   | List of addresses the response will be sent to as Bcc recipients | String   |

Reply To E-Mail Published Data
------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Bcc   | List of Bcc recipients for this reply   | String   |
| Body Prefix   | The prefix to prepend to the email message body   | String   |
| Body Type   | The format of the email message body   | String   |
| Cc   | List of Cc recipients for this reply   | String   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address | Address of the Exchange server   | String   |
| ID   | The ID of the item   | String   |
| Reply To All   | Indicates whether the response should be send to all recipients of the original message | Boolean   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Use Autodiscover   | Whether or not the Autodiscover service is being used   | Boolean   |
| User Name   | User name used to log on to Exchange Server   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx) <br> <br>
