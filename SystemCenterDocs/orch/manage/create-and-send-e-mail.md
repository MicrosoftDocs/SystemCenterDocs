---
title: Create and Send E-Mail
description: The Create and Send E-Mail activity is used in a runbook to create and send an email message to one or more recipients.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42303d7c-eb1c-4343-93d2-3123b93f1464
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create and Send E-Mail

Applies To: System Center 2016 - Orchestrator

The Create and Send E-Mail activity is used in a runbook to create and send an email message to one or more recipients.

The following tables list the required properties, optional properties, and published data for this activity.

## Create and Send E-Mail Required Properties

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| Body   | The body of the email message   | String   |
| Subject   | The subject of the email message   | String   |
| To   | The intended recipients of the email message | Comma separated list of email addresses |

## Create and Send E-Mail Optional Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Attachments   | List of any attachments for this email message   | Comma separated list of file paths   |
| Bcc   | Bcc recipients for this email message   | Comma separated list of email addresses   |
| Body Type   | Email body content format type   | Text<br>HTML   |
| Categories   | List of any categories that are associated with this email message   | Comma separated list   |
| Cc   | Cc recipients for this email message   | Comma separated list of email addresses   |
| Destination Folder   | Alternative destination folder of the sent email   | String   |
| From   | Sets the content of the From field in the email header   | String   |
| Importance   | Importance of the message   | Low<br>Normal<br>High   |
| In Reply To   | Sets the In-Reply-To reference of the email   | String   |
| Is Delivery Receipt Requested | Indicates whether a delivery receipt is requested for this email message | True<br>False   |
| Is Read Receipt Requested   | Indicates whether a read receipt is requested for the email message   | True<br>False   |
| Is Response Requested   | Indicates whether a response is requested for the email message   | True<br>False   |
| References   | Sets the references of the email message   | String   |
| Sender   | Sets the sender of the email message   | String   |
| Sensitivity   | The sensitivity of this item   | Confidential<br>Normal<br>Personal<br>Private |

## Create and Send E-Mail Published Data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Destination Folder   | The folder where the item is stored   | String   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address | Address of the Exchange server   | String   |
| Timeout (seconds)   | Timeout value for the Exchange server connection   | Number   |
| Use Autodiscover   | Indicates whether or not to use Autodiscover to check for changes | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx) <br> <br>
