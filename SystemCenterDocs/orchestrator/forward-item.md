---
title: Forward Item
description: The Forward Item activity is used in a runbook to forward an existing email message or appointment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 147edef0-e9db-49e8-b6f8-f8539a7c610d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Forward Item

Applies To: System Center 2016 - Orchestrator

The Forward Item activity is used in a runbook to forward an existing email message or appointment.

The following tables list the required properties, optional properties, and published data for this activity.

## Forward Item Required Properties

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Body Prefix | The prefix that will be prepended to the original item's body when it is forwarded | String   |
| ID   | The ID of the item to be forwarded   | String   |
| To   | The list of recipients the response will be sent to   | Comma-separated list of email addresses |

## Forward Item Optional Properties

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Bcc   | The list of addresses this item will be sent to as Bcc recipients | Comma separated list of email addresses |
| Body Type   | The format of body of the email message   | Text<br>HTML   |
| Cc   | The list of addresses the item will be sent to as Cc recipients   | Comma separated list of email addresses |

## Forward Item Published Data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Bcc   | The list of Bcc recipients for this item   | String   |
| Body Prefix   | The prefix to prepend to the body   | String   |
| Body Type   | The format of the message body   | Text<br>HTML   |
| Cc   | The list of Cc recipients for the item   | String   |
| Domain   | Domain to which the computer that runs Exchange Server belongs   | String   |
| Exchange Server Address | Address of the computer that runs Exchange server   | String   |
| ID   | The ID of the forwarded item   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| To   | List of recipients   | String   |
| User Name   | User name used to log on to Exchange server   | String   |
| Use Autodiscover   | Indication of whether or not to use Autodiscover to check for changes | Boolean   |

