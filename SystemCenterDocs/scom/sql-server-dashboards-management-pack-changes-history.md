---
ms.assetid: 110aa866-00e8-4672-bd03-39cc8818e6b4
title: Features and Enhancements in Management Pack for SQL Server Dashboards
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Dashboards
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server Dashboards

This section covers new functionality and improvements in Management Pack for SQL Server Dashboards.

## September 2020 - 7.0.25.0 CTP

### What's New

  - Added tiles for Azure SQL Database Management Pack
  - Rename tiles for SSRS Management Pack and SQL Server Replication Management Pack

## June 2019 - 7.0.16.0

### What's New

  - Updated Dashboards configuration to show tiles for new MDX performance collections in Analysis Services management packs

## February 2018 - 7.0.2.0 RTM

### Bug Fixes

  - Fixed issue: "DW data early aggregation" rule crashes on SCOM 2016

## December - 2016 6.7.15.0 RTM

### Bug Fixes

  - Fixed issue: Tiles content is replaced with question signs after a long period of inactivity

## October 2016 - 6.7.7.0 RTM

### Bug Fixes

  - Fixed issue: expanding “arrow” has low-contrast color when a health group is collapsed in Instance view (High-Contrast #2 color scheme)
  - Fixed issue: in Web console, Dashboards continuously send requests to the database
  - Fixed issue: not the first object gets selected in the object list after drill-down
  - Fixed issue: horizontal scroll position resets after refreshing the Instance view
  - Fixed issue: “No Data” message is displayed on some tiles after upgrading Dashboards management pack from version 6.7.2.0 to 6.7.4.0 or later version
  - Fixed issue: on Web console, Dashboards crash when drilling down from Datacenter view to Instance view
  - Restored the correct group order in SQL Server Summary dashboard views

## September 2016 - 6.7.5.0 CTP2

### What's New

  - Improved Dashboards performance

### Bug Fixes

  - Fixed issue: Regular\Virtual group tile will show 0 objects if user adds a new group before the previous one has been saved
  - Fixed issue: virtual group filtering for Generic Distributor does not work
  - Fixed issue: tooltips on some menus appear in unexpected places
  - Fixed issue: Web Console is crashing upon right-clicking the hamburger button
  - Fixed issue: button captions are cropped in some dashboard localization packs
  - Fixed issue: Instance dashboard displays data for the item that is the first in the list if no items appear after applying a filter
  - Fixed issue: the first group object is not in focus after clearing “Filter” field if there were no search results
  - Fixed issue: Summary dashboards appear to be in a strange state if one installs only Dashboards MP without SQL MPs
  - Fixed issue: Bulk Add Tiles does not trigger the refresh action
  - Fixed issue: object and alert counters of Virtual groups containing real groups display zeros
  - Fixed issue: an error appears in Web Console when using keyboard for navigation in “Add Aggregated Monitor” dialog
  - Fixed issue: unexpected scrolling behavior in the instance view when using mouse scroll
  - Fixed issue: markup of the dialog for adding classes gets broken when the scrollbars are displayed
  - Fixed issue: wrong width value of the Edit dialog
  - Fixed issue: there is no refresh action after saving the edited Virtual Group configuration
  - Fixed issue: white-screen exception when working with a dialog in Web console
  - Fixed issue: Datacenter and Instance queries fail when a special set of classes is selected

## June 2016 - 6.7.2.0 RTM

### What's New

  - Changed some stored procedures to improve Dashboards performance

## June 2016 - 6.7.1.0 CTP2.1

### What's New

  - Improved Dashboards performance

## May 2016 - 6.7.0.0 CTP2

### What's New

  - Added a feature to support Virtual Groups (groups defined by classes, not by real group instance). This will help users with partial access to use our predefined dashboards
  - Added a feature to Bulk Add tiles from the class definition
  - Added a feature to ignore some states while calculating the worst state for the Datacenter View State Tile; added a feature to set this ignorance up for each group
  - Added a feature to show/hide Instance path in the list on the Instance view
  - Added instance path to the Instance Details
  - Implemented deferred loading of the instance tiles to make the instance view operation faster
  - Implemented a new format for Dashboards configuration providing a smaller size and a single binding
  - Implemented a converter from old to new format providing preservation of  user changes
  - Improved error reporting
  - Improved performance of initial load process
  - Improved data sources performance
  - Improved performance of instance selection (made it asynchronous)
  - Improved performance of Datacenter and Instance View Tiles, loading and loaded animations
  - Updated Summary dashboard
  - The “Known issues and Troubleshooting” section of the guide is updated

### Bug Fixes

  - Fixed animation issues and minor visual glitches (positioning, size of elements, fonts, main loading animation)

## April 2016 - 6.6.7.30

### What's New

  - Updated Path search and display
  - Added removal of unused elements
  - Implemented a deferred loader
  - Improved drill-down process
  - Added support for SQL Server Replication 2016 MP objects in Summary dashboard

### Bug Fixes

  - Fixed animation, styles and display issues
  - Fixed filter and search issues
  - Fixed "Show/Hide Path" button in Silverlight
  - Fixed group adding process
  - Fixed HighLight; simplified tile adding process

## March 2016 - 6.6.7.6 CTP1

### What's New

  - Replaced 999+ presentation with a new one (26.2k)
  - Added configurable rule to pre-aggregate data in the DW (see the corresponding Known Issue)
  - Added second row in the instance view to show Path of the object, and allow searching by Path
  - Fixed tooltip presentation on the Instance view
  - “Known issues and Troubleshooting” section of the guide is updated

### Bug Fixes

  - Fixed “The client has been disconnected from the server. Please call ManagementGroup.Reconnect() to reestablish the connection” exception

## November 2015 - 6.6.4.0
  
### Bug Fixes

  - Fixed an installation issue on SQL Server 2008
  - Fixed permission grants for Alert aggregation table

## November 2015 - 6.6.3.0

### What's New

  - Implemented batching to all data aggregation mechanisms to ensure low temp database space and log space usage
  - Implemented a control bit to divide group from non-group references to save space in aggregated data storage

## October 2015 - 6.6.2.0

### What's New

  - Improved performance
  - Objects with selected monitors are now displayed on the top of the tiles list while editing
  - If there are no child elements, Related Objects tile is not displayed in Instance View
  - Added Dark, Light and Contrast themes
  - Introduced an interface upgrade allowing to display the Dashboard errors
  - User rights are now considered in the Dashboard display: the user can see the groups according to his/her access level only;  Read-Only mode is implemented, it provides basic functions only: navigation, changing of the personalization settings
  - Introduced a Dashboard feature allowing to display data from any nesting level within the widgets

### Bug Fixes

  - Fixed some UI errors, UI design upgraded
  - Fixed synchronization errors of the personalization settings