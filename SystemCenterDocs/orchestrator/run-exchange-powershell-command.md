---
title: Run Exchange PowerShell Command
description: You can use the Run Exchange PowerShell Command activity in a runbook to run Exchange 2010 cmdlets.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d3f20506-1362-4290-af79-ef3f6d0f1b05
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Run Exchange PowerShell Command

> Applies To: System Center 2016 - Orchestrator

You can use the Run Exchange PowerShell Command activity in a runbook to run Exchange 2010 cmdlets.

The following tables list the required properties and published data for this activity.

## Required properties for the Run Exchange PowerShell command activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Command Text   | Specifies the full command text, to include the parameters.   | String   |
| Is Exchange Command | Specifies if the command is to be run against the configured Exchange server. The default value is True. | True or<br>False |

## Published data for the Run Exchange PowerShell command activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Command Output   | The output results from running the command. Each result consists of a collection of name-value pairs (format \[&lt;Name&gt;: &lt;Value&gt;\]) that represents the result object fields and their respective values. When the command returns multiple results, they are published as multi-valued data. | String   |
| Command Text   | The full command text, to include the parameters.   | String   |
| Command Warnings   | The warning stream contents that result from running the command.   | String   |
| Exchange Environment   | The type of Exchange environment where the activity will be executed.   | String   |
| Exchange PowerShell Application | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected Exchange server.   | String   |
| Exchange Server Port   | The connected Exchange server port.   | String   |
| Exchange User Name   | The username that is used to connect to Exchange Server.   | String   |
| Is Exchange Command   | Indicates if the command is to be run against the configured Exchange server.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol by using a Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
