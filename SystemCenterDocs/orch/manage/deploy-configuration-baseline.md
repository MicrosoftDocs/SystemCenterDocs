---
title: Deploy Configuration Baseline activity
description: Describes the configurable properties for the Deploy Configuration Baseline activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 15/03/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3f3137f-3e5a-44bc-9623-d541d1348e9e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Deploy Configuration Baseline activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The objective of this activity is to assign a configuration baseline to
a collection. It requires a pre-existing baseline as well as a
collection to which the baseline will be assigned.

The activity publishes all of the data from the required and optional
properties into published data. The following tables list the required
and optional properties and published data for this activity.

## Deploy Configuration Baseline required properties

|**Element**|**Description**|**Valid Values**
|--------------------------------------------------|-------------------------------------------------------------------------------------------------|------------------|
|Deployment Name|The desired name for the new deployment that will be shown in the Configuration Manager console||    
|Baseline|Performs a WMI query against Configuration Manager and returns the baseline information ||           
|Baseline Value Type|The type of baseline value|ID or Name|
|Collection|Performs a WMI query against Configuration Manager and returns the collection information||          
|Collection Value Type|The type of collection value|ID or Name|
|Remediate non-compliant rules when supported |Enables the remediation of non-compliant rules |True or False|
|Allow Remediation outside of Maintenance Windows|Enables the remediation of non-compliant rules outside of the maintenance window |True or False|

## Schedule Tab properties

 - Start: Defines a date and timestamp and how the time values are interpreted. Options are:

    -   **Client Local Time** (default): the times specified represent the local time on the client
    -   **UTC**: The times specified are UTC times.

- Recurrence Pattern: Determines how often the configuration baseline should be deployed. Options are:
    - **None** (default): The configuration baseline is deployed only once, at the date and time specified in **Start**.
    - **Weekly**: The configuration baseline is deployed on the specified day of the week at the interval of the specified number of weeks.
    -   **Monthly**: The configuration baseline is deployed at the interval of the specified number of months on:

        -   **Day**: the specified day of the month.
        -   **The Last Day of the Month**
        -   The specified occurrence of the specified day of the week within the month.
        -   **Custom Interval**: The configuration baseline is deployed at the interval of the specified number of minutes, hours, or days.

## Alerts Tab properties

 - Generate Alerts: True or False (Default = False) When set to **True**, an alert definition will be created for the configuration baseline deployment according to the settings below. When set to **False**, alert settings in this group are ignored.
 - When Compliance % Below: When compliance with this configuration baseline is below this percentage, an alert will be generated in Configuration Manager. Valid values: 1 - 99
 - After Date and Time: Alerts will be generated only after this period of time has elapsed from the configuration baseline’s deployment.
 - Also Generate a System Center Operations Manager Alert: True or False (Default = False).
    >[!NOTE]
    > Requires an Operations Manager connection with Configuration Manager

## Deploy Configuration Baseline published data

|Element|Description|
|---------------|-------------------------------------------------|
|Connection|Specifies the name of the connection to the Configuration Manager server|                                                                              
|Collection ID|Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).|   
