---
title: Configuring Service Level Management in System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8f84795-11fd-4c62-8f50-0929cedd3b20
---
# Configuring Service Level Management in System Center 2016 - Service Manager
This section provides an overview of how to configure service level management in Service Manager. This section also contains procedures that cover service level management configuration scenarios.

Service level management is the process that you use to measure incident and service request timeliness. In Service Manager, you create a service level item that consist of queues that correspond to each service level, plus time metrics to measure and warn for. Separately, you can also send notifications to users that occur before and after service level breach. In the [!INCLUDE[smcons](../../includes/smcons_md.md)], you manage this process in the Administration workspace using the following nodes:

-   Calendar

-   Metric

-   Service Level Objectives

## Calendar
The Calendar node is used to define work days, work hours, and holidays as a calendar item in the [!INCLUDE[smcons](../../includes/smcons_md.md)]. Each calendar item is a distinct work schedule that represents time available for analysts to resolve incidents and fulfill service requests. Calendar items correspond to at least one service level objective where it is measured by a time metric, such as resolution time.

## Metric
The Metric node is used to define time metrics against a calendar item, corresponding to a service level objective. A time metric is the measurement between start and end dates. There are two predefined metrics in [!INCLUDE[smshort](../../includes/smshort_md.md)]:

-   Resolution Time

-   Completion Time

The Resolution Time metric is used to measure the maximum length of time that incidents should take before they are resolved. By default, the two points in time that define Resolution Time are the start date as the date and time that each incident is created and the end date as the date and time that each incident is resolved.

The Completion Time metric is used to measure the maximum length of time that service requests should take before they are completed. By default, the two points in time that define Completion Time are the start date as the date and time that each service request is created and the end date as the date and time that each service request is completed.

## Service Level Objectives
The Service Level Objectives node is used to create relationships between a queue and a service level. It is also used to define the relationship between a calendar item and a time metric. Separately, you can also send notifications to users that occur before and after service level breach. [!INCLUDE[crabout](../../includes/crabout_md.md)] sending notifications, see [How to Send SLA Notification Information to the Assigned-To User](How-to-Send-SLA-Notification-Information-to-the-Assigned-To-User.md).


