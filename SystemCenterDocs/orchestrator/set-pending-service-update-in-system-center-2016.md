---
title: Set Pending Service Update in System Center 2016
description: The Set Pending Service Update activity is used in a runbook to set a specific service template as the pending service update.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18e965c9-7f74-4259-96ae-14e0b4a19efa
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Set Pending Service Update in System Center 2016

Applies To: System Center 2016 - Orchestrator

The Set Pending Service Update activity is used in a runbook to set a specific service template as the pending service update.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Set Pending Service Update Required Properties

**Element**   | **Description**   |
|:---|:---|
| Service Name   |   |
| Service Template Name   |   |   
| Service Template Release |   |   
| Update Type   | Applying updates to the existing (in-place) virtual machines or Deploying new virtual machines with the updated settings |   

## Set Pending Service Update Optional Properties

There are no optional properties for this activity.

## Set Pending Service Update Published Data

| **Element**   | **Description** | **Value Type** |
|:---|:---|:---|
| Accessibility   |   |   |
| All VMs Accessible   |   |   |
| Application Hosts   |   |   |
| Cloud Name   |   |   |
| Computer Tier Names   |   |   |
| Cost center   |   |   |
| Custom Property names/values   |   |   |
| Date added   |   |   |
| Date modified   |   |   |
| Deployed To   |   |   |
| Description   |   |   |
| Enabled   |   | Boolean   |
| Global Settings   |   |   |
| Granted To List   |   |   |
| Host Group Name   |   |   |
| In Servicing Mode   |   | Boolean   |
| Is in servicing window   |   | Boolean   |
| Overall Status   |   |   |
| Owner Name   |   |   |
| Owner Sid   |   |   |
| Pending Global Settings   |   |   |
| Pending Service Template Name   |   |   |
| Pending Service Template Present |   |   |
| Pending Service Template Release |   |   |
| Priority   |   |   |
| Service Configuration Name   |   |   |
| Service ID   |   |   |
| Service Name   |   |   |
| Service State   |   |   |
| Service Status   |   |   |
| Service Template ID   |   |   |
| Service Template Name   |   |   |
| Service Template Release   |   |   |
| Servicing Windows   |   |   |
| Tag   |   |   |
| User Role ID   |   |   |
| User Role Name   |   |   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
