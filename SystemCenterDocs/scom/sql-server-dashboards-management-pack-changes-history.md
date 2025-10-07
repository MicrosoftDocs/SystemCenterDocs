---
ms.assetid: 110aa866-00e8-4672-bd03-39cc8818e6b4
title: Features and Enhancements in management pack for SQL Server Dashboards
description: This article explains the new functionality and bug fixes implemented in management pack for SQL Server Dashboards
author: epomortseva
ms.author: v-gajeronika
ms.date: 07/22/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Features and enhancements in management pack for SQL Server Dashboards

This article covers new functionality and improvements in Management Pack for SQL Server Dashboards.

## July 2024 - 7.6.2 RTM

### What's New

- Added Vertipaq tiles to Analysis Services dashboards:
  - Monitor tiles: VertiPaq memory consumed by SSAS Instance and VertiPaq memory paging indication
  - Perfomance tile: VertiPaq Memory Limit, VertiPaq Memory Limit(GB), VertiPaq Memory Usage on the Server (%), VertiPaq Memory Usage on the Server (GB), VertiPq Nonpaged Memory (GB) and VertiPaq Memory Paged (GB)
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - implemented [Keyboard Navigation](sql-server-dashboards-management-pack-instance-dashboard-navigation.md) using the A and D buttons on the tiles in the dashboard
  - added the ability for the screen reader to announce buttons and errors in the SQL Server wizard
  - redesigned dashboard list controls for greater accessibility

## January 2024 - 7.4.0.0 RTM

### What's new

- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - improved keyboard navigation
  - improved color contrast in dashboards for better legibility
  - reworked high contrast theme for dashboards
  - added support for screen-reading software

### Bug fixes

- Fixed the issue of Summary Dashboard view not working in the System Center Operations Manager Console when operational and data warehouse databases are hosted on SQL Server version 2022

## July 2023 - 7.2.0.0 RTM

### What's new

- Minor visual improvements

## December 2022 - 7.0.42.0 RTM

### What's new

- Removed Silverlight framework

## June 2022 - 7.0.38.0 RTM

### What's new

- Minor visual improvements

## June 2021 - 7.0.32.0 RTM

### What's new

- Added tiles for SQL Server Integration Services Management Pack
- Renamed some Dashboard tiles

### Bug fixes

- Fixed an issue with the wrong alert parameter reference in the Summary Dashboard view tiles

## October 2020 - 7.0.26.0 RTM

### What's new

- Added tiles for Azure SQL Database management pack
- Rename tiles for SQL Server Reporting Services management pack and SQL Server Replication management pack

## June 2019 - 7.0.16.0 RTM

### What's new

- Updated Dashboards configuration to show tiles for new MDX performance collections in the Analysis Services management pack

## February 2018 - 7.0.2.0 RTM

### Bug fixes

- Fixed issue: "DW data early aggregation" rule crashes on the System Center Operations Manager 2016
