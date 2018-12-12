---
title: Set Pending Service Update activity in System Center - Orchestra
description: The Set Pending Service Update activity is used in a runbook to set a specific service template as the pending service update.
ms.date: 01/22/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---
# Set Pending Service Update activity

The Set Pending Service Update activity is used in a runbook to set a specific service template as the pending service update.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Required properties

**Element**   | **Description**   |
|:---|:---|
| Service Name   |   |
| Service Template Name   |   |   
| Service Template Release |   |   
| Update Type   | Applying updates to the existing (in-place) virtual machines or Deploying new virtual machines with the updated settings |   

## Optional properties

There are no optional properties for this activity.

## Published data

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

