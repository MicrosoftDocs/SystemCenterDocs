---
ms.assetid: 8e379e26-a604-4976-88ff-d291c48b8700
title: Features and enhancements in Management Pack for SQL Server Analysis Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Analysis Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server Analysis Services

This section covers new functionality and improvements in Management Pack for SQL Server Analysis Services.

## June 2021 - version 7.0.31.0 CTP

### What's New

- Improved performance of Discovery and Monitoring workflows

## December 2020 - version 7.0.29.0 RTM

### What's New

- Improved performance of partition discovery for multidimensional databases
- Updated and improved System Center Operations Manager 2019 HTML Dashboards to display SSAS health and alerts

## June 2020 - version 7.0.22.0 RTM

### Bug Fixes

- Added tasks Start/Stop Analysis Services Windows Service
- Updated display strings

## December 2019 - version 7.0.19.0 CTP

### What's New

- Added support for SQL Server Analysis Services 2012, 2014, and 2016 in addition to previously supported 2017 and up
- Implemented Database Status monitor
- Updated display strings

## October 2018  - version 7.0.10.0 RTM

### What's New

- Replaced the Core Library in the delivery with the version 7.0.7.0, that version which is delivered with the most recent RTM version of the management pack for SQL Server 2017+
- Improved displaying of the SSAS instance version (now shows Patch Level version instead of Version)
- Added missed dependency monitors required to roll up the instance health appropriately
- Updated Summary dashboards
- Updated display strings

### Bug Fixes

- Fixed alert for "Partition Storage Free Space" monitor