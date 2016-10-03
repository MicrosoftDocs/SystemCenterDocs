---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  About Importing Data from System Center Configuration Manager
ms.technology:  service-manager
ms.assetid:  6c77a473-3189-443b-b63a-f835cbe72ec1
---

# About Importing Data from System Center Configuration Manager

>Applies To: System Center 2016 - Service Manager

You can import data from the System Center Configuration Manager site database into the Service Manager database. This automatically creates and populates configuration items for the hardware and software that you want to manage in Service Manager. After you import data from System Center Configuration Manager, you can attach the respective configuration items to relevant incidents, and the information in the configuration items will be available to analysts working on the incident.

By using a Configuration Manager connector, you can import configuration baselines from System Center Configuration Manager and then use these configuration baselines to automatically generate incidents for noncompliant configuration items.

For information about Microsoft Operations Framework (MOF) implementation of change and configuration, see [Position of the Change and Configuration SMF Within the MOF IT Service Lifecycle](http://go.microsoft.com/fwlink/p/?LinkID=115631).

## Complete the Data Warehouse Registration Process
Before you create the Configuration Manager connector, you must make sure that the Data Warehouse Registration process is complete.

## Additional Data in Configuration Manager
Additional data in Configuration Manager includes User-Device Affinity (UDA), Mobile Device Data, and Software Request Data. UDA data from Configuration Manager more accurately determines who the primary user of a computer or device is. The UDA data collected by the Service Manager Configuration Manager connector is used to populate the UsesComputer and PrimaryUser information in the Service Manager database.

Mobile device data for Windows Phones, Windows Mobile Phones, and Nokia devices will be collected by the Service Manager Configuration Manager connector. Data from other mobile devices such as iPhone, BlackBerry, and Android-based phones will be collected when you are using the Configuration Manager Exchange Server connector. Mobile device data will be imported into the Service Manager database as configuration items, and it can be associated with work items, incident management, and change management.

Software request data will be used in support of self-service software request integration with Configuration Manager. The administrative category data from Configuration Manager will be used to select which Service Request templates to apply when creating a request from the Self-Service Portal.

## Schedule
You can configure the Configuration Manager connector to update the Service Manager database on a recurring schedule. You can also temporarily suspend the importation of data from Configuration Manager by disabling the connector. For example, you can disable the connector when maintenance is performed on the Configuration Manager site database because you know that the maintenance process temporarily creates inaccurate data. When appropriate, you can re-enable the connector and resume importing data.

## Extended Hardware Inventory with Configuration Manager
In Configuration Manager, you can extend the hardware inventory by collecting an inventory of additional Windows Management Instrumentation (WMI) classes, additional WMI class attributes, registry keys, and other customizations to accommodate your organization's requirements. For more information about extending the hardware inventory in Configuration Manager, see [How to Extend Hardware Inventory](http://go.microsoft.com/fwlink/p/?LinkID=160640).

If you have extended the hardware inventory in Configuration Manager, you must create a new Configuration Manager Connector management pack in Service Manager to collect the extended hardware inventory. This new management pack can contain only the information required to collect the extended hardware inventory from Configuration Manager, or it can consist of everything from the original Configuration Manager Connector management pack plus the new extended hardware inventory. For information about creating a new connector management pack, see [How to Configure a Configuration Manager Connector for an Extended SMS_def.mof File](admin-how-to-configure-a-configuration-manager-connector-for-an-extended-sms-def.mof-file.md).

## Importing Software Configuration Items
You can import software configuration items with the Configuration Manager Connector by importing  the following asset intelligence reporting classes in System Center Configuration Manager. These classes should be enabled in Configuration Manager before you configure the Configuration Manager connector in Service Manager. For more information about enabling Asset  Intelligence in Configuration Manager, see [How to Enable Asset Intelligence](http://go.microsoft.com/fwlink/p/?LinkId=262404).

-   SMS_InstalledSoftware

-   SMS_SystemConsoleUsage

-   SMS_SystemConsoleUser

-   SoftwareLicensingService

-   SoftwareLicensingProduct

If software for a particular computer does not appear in the **All Software** view in the Configuration Items workspace, you should review the Operations Manager event log on the Service Manager primary management server. You should look for events with sources of OpsMgr Connector and Lfx Service to determine if there are any errors.
