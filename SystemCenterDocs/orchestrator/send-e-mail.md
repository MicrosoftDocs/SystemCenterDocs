---
title: Send E-Mail
description: The Send E-Mail activity is used in a runbook to send e-mail messages.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 30dc0550-1edc-40dc-8bdd-93e2fc10103e
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Send E-Mail

The Send E-Mail activity is used in a runbook to send email messages.

This activity publishes all the data from the required and optional properties into published data.

The following tables list the required and optional properties and published data for this activity.

## Send E-Mail required properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the email message to be sent | String   |

## Send E-Mail published data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address | Address of the Exchange server   | String   |
| ID   | ID of the email message to be sent   | String   |
| Timeout (seconds)   | Connection timeout   | Numbers   |
| Use Autodiscover   | Whether or not the Autodiscover service is being used | Boolean   |
| User Name   | Username to use to connect to the Exchange server   | String   |
