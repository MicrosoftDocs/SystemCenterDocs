---
title: Use the Authoring Workspace in Operations Manager
description: This article describes how to use the Operations Manager Operations console to perform authoring tasks.
author: jyothisuri
ms.author: jsuri
ms.date: 04/22/2025
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 8a116b94-6bc4-4160-b539-4bd542b8ee5a
---

# Use the Authoring Workspace in Operations Manager

This article describes how to use the Operations Manager Operations console to perform authoring tasks.

The options in the Authoring workspace allow you to create new monitoring scenarios. This could be to change or add monitoring in an existing management pack or to create a new management pack for an application that doesn't have one.  

Authoring is described in detail in the [Operations Manager Authoring Guide](https://social.technet.microsoft.com/wiki/contents/articles/15251.system-center-management-pack-authoring-guide.aspx). The sections below describe the different options in the Authoring workspace.  

## Management Pack Templates  
*Management Pack Templates* allow you to create complete monitoring scenarios with minimal input. Once you complete a wizard, the management pack template creates monitors, rules, and even classes to implement the particular scenario. There's no requirement for you to understand the management pack elements that are created since you can continue to use the template to perform configuration. It will make any necessary modifications to the underlying elements.  

|Elements|Description|  
|-|-|  
|.NET Application Performance Monitoring|Monitor your Windows ASP.NET and WCF Applications hosted on IIS 7.0, 8.0 and 10.0, including Windows Services that use .NET Framework.|  
|OLE DB Data Source|Monitor the availability and performance of a database. Sample queries can be executed from one or more watcher nodes.|  
|Process Monitoring|Monitor the availability and performance of a wanted process or verify that an unwanted process isn't running.|  
|TCP Port|Monitor the availability of an application listening on a specific TCP port. Test can be performed from one or more watcher nodes.|
|TFS Work Item Synchronization|Links Operations Manager alerts and Team Foundation Server work items.|  
|Unix/Linux LogFile|Monitor a Unix or Linux log file for a specific log entry one a specific computer or group of computers.|  
|Unix/Linux Service|Monitor the availability of a service on a Unix or Linux computer or group of computers.|  
|Windows Service|Monitor the availability and performance of a service running on one or more Windows computers.|  
|Web Application Availability Monitoring|Create an availability monitoring test for one or more Web Application URLs.|  
|Web Application Transaction Monitoring|Create a monitoring test of a Web Application to verify availability and performance.|  

## Distributed Applications  
*Distributed Applications* allow you to group together multiple components that are part of a single application. The health of each included object is used to calculate an overall health of the application itself. This health can be used to support alerts, views, and reports.  

## Groups  
*Groups* contain a particular set of managed objects. They're used to scope views, reports, and certain monitoring scenarios. Criteria can be provided to automatically populate a group based on properties of the objects, or you can add specific objects to a group. You can create new groups and edit existing groups. You can also view the current members of a group. Once it has been created, a group can be used in the Monitoring workspace for scoping views, the Reporting workspace for scoping reports, or in the Authoring workspace for overrides, management pack templates, or service level objects.  

## Management Pack Objects  
The Management Pack Objects section provides access to the different elements that are available. Depending on the kind of object, you may be able to create new objects, edit existing objects, or view existing objects.  

|Elements|Description|  
|-|-|  
|Attributes|An *attribute* is a property of a class in a management pack. You can add additional attributes to collect additional information about managed objects. These attributes can be used to support group membership or accessed by monitors or rules.|  
|Monitors|*Monitors* are workflows that run on an agent and determine the current health of an object. Each monitor uses a particular data source as the event log, performance data, or a script to collect its information.<br><br>You can create new monitors and edit existing monitors in the Operations console for specific monitoring scenarios, which will address the requirements of most users. More complex monitors must be created and modified using the Authoring console.|  
|Object Discoveries|*Object Discoveries* are workflows that run on an agent and discover objects to manage.<br><br>You can't create new object discoveries in the Operations console. You can view existing object discoveries in management packs and use overrides to modify the frequency that they run and potentially other parameters.|  
|Overrides|*Overrides* are used to change parameters on workflows including monitors, rules, and discoveries.<br><br>Overrides are created from the property page of the workflow that they apply to. This option allows you to view and modify existing overrides.|  
|Rules|*Rules* are workflows that run on an agent that create an alert, collect information for analysis and reporting, or run a command on a schedule. Each rule uses a particular data source as the event log, performance data, or a script to collect its information.<br><br>You can create new rules and edit existing rules in the Operations console for specific monitoring scenarios, which will address the requirements of most users. More complex rules must be created and modified using the Authoring console.|  
|Service Level Tracking|*Service Level Tracking* allows you to compare the availability of managed objects to a specific object.<br><br>This option allows you to create new *Service Level Objectives* and edit existing Service Level Objectives.|  
|Tasks|*Tasks* are workflows that run when you request them in the Operations console. *Agent tasks* run on one or more agent computers. *Console tasks* run on the Operations console workstation.<br><br>You can create new tasks and edit existing tasks in the Operations console for specific monitoring scenarios, which will address the requirements of most users. More complex tasks must be created and modified using the Authoring console.|  
|Views|*Views* display managed objects and collected data in the Operations Console.<br><br>Views are created and modified in the Monitoring workspace. This option displays the existing views available for each target class.|  

## Next steps

* To learn how to access and interact with the operational data or perform administrative tasks, see [Connect to the Operations and Web Console](manage-consoles-how-to-connect.md).

* To learn how to create a custom writeable management pack to store your overrides, see [How to create a management pack for overrides](manage-mp-create-unsealed-mp.md).

* To learn how to use groups to collect monitoring objects into manageable units for granular configuration management in the management group, review [Create and manage groups](manage-create-manage-groups.md).  
