---
title: Using the Authoring Workspace in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a116b94-6bc4-4160-b539-4bd542b8ee5a
---
# Using the Authoring Workspace in Operations Manager
The options in the Authoring workspace allow you to create new monitoring scenarios. This could be to change or add monitoring in an existing management pack or to create a new management pack for an application that doesn’t have one.

Authoring is described in detail in the [Operations Manager 2012 Authoring Guide](http://go.microsoft.com/fwlink/p/?LinkID=212377). The sections below describe the different options in the Authoring workspace.

## Management Pack Templates
*Management Pack Templates* allow you to create complete monitoring scenarios with minimal input. Once you complete a wizard, the management pack template creates monitors, rules, and even classes to implement the particular scenario. There is no requirement for you to understand the management pack elements that are created since you can continue to use the template to perform configuration. It will make any necessary modifications to the underlying elements.

|||
|-|-|
|OLE DB Data Source|Monitor the availability and performance of a database. Sample queries can be executed from one or more watcher nodes.|
|Process Monitoring|Monitor the availability and performance of a wanted process or verify that an unwanted process is not running.|
|TCP Port|Monitor the availability of an application listening on a specific TCP port. Test can be performed from one or more watcher nodes.|
|Unix\/Linux LogFile|Monitor a Unix or Linux log file for a specific log entry one a specific computer or group of computers.|
|Unix\/Linux Service|Monitor the availability of a service on a Unix or Linux computer or group of computers.|
|Windows Service|Monitor the availability and performance of a service running on one or more Windows computers.|

## Distributed Applications
*Distributed Applications* allow you to group together multiple components that are part of a single application. The health of each included object are used to calculate an overall health for the application itself. This health can be used to support alerts, views, and reports.

## Groups
*Groups* contain a particular set of managed objects. They are used to scope views, reports, and certain monitoring scenarios. Criteria can be provided to automatically populate a group based on properties of the objects, or you can add specific objects to a group.You can create new groups and edit existing groups. You can also view the current members of a group. Once it has been created, a group can be used in the Monitoring workspace for scoping views, the Reporting workspace for scoping reports, or in the Authoring workspace for overrides, management pack templates, or service level objects.

## Management Pack Objects
The Management Pack Objects section provides access to the different elements that are available. Depending on the kind of object, you may be able to create new objects, edit existing objects, or view existing objects.

|||
|-|-|
|Attributes|An *attribute* is a property of a class in a management pack. You can add additional attributes to collect additional information about managed objects. These attributes can be used to support group membership or accessed by monitors or rules.|
|Monitors|*Monitors* are workflows that run on an agent and determine the current health of an object. Each monitor uses a particular data source as the event log, performance data, or a script to collect its information.<br /><br />You can create new monitors and edit existing monitors in the Operations console for specific monitoring scenarios which will address the requirements of most users. More complex monitors must be created and modified using the Authoring console.|
|Object Discoveries|*Object Discoveries* are workflows that run on an agent and discover objects to manage.<br /><br />You cannot create new object discoveries in the Operations console. You can view existing object discoveries in management packs and use overrides to modify the frequency that they run and potentially other parameters.|
|Overrides|*Overrides* are used to change parameters on workflows including monitors, rules, and discoveries.<br /><br />Overrides are created from the property page of the workflow that they apply to. This option allows you to view and modify existing overrides.|
|Rules|*Rules* are workflows that run on an agent that create an alert, collect information for analysis and reporting, or run a command on a schedule. Each rule uses a particular data source as the event log, performance data, or a script to collect its information.<br /><br />You can create new rules and edit existing rules in the Operations console for specific monitoring scenarios which will address the requirements of most users. More complex rules must be created and modified using the Authoring console.|
|Service Level Tracking|*Service Level Tracking* allows you to compare the availability of managed objects to a specific object.<br /><br />This option allows you to create new *Service Level Objectives* and edit existing Service Level Objectives.|
|Tasks|*Tasks* are workflows that run when you request them in the Operations console. *Agent tasks* run on one more agent computers. *Console tasks* run on the Operations console workstation.<br /><br />You can create new tasks and edit existing tasks in the Operations console for specific monitoring scenarios which will address the requirements of most users. More complex tasks must be created and modified using the Authoring console.|
|Views|*Views* display managed objects and collected data in the Operations Console.<br /><br />Views are created and modified in the Monitoring workspace. This option displays the existing views available for each target class.|

## See Also
[Using the Reporting Workspace in Operations Manager](./Using-the-Reporting-Workspace-in-Operations-Manager.md)
[Using the Administration Workspace in Operations Manager](./Using-the-Administration-Workspace-in-Operations-Manager.md)
[Using My Workspace in Operations Manager](./Using-My-Workspace-in-Operations-Manager.md)
[Using Health Explorer in Operations Manager](./Using-Health-Explorer-in-Operations-Manager.md)
[Using the Monitoring Workspace in Operations Manager](./Using-the-Monitoring-Workspace-in-Operations-Manager.md)
[How to Connect to the Web Console](./How-to-Connect-to-the-Web-Console.md)
[How to Connect to the Operations Console](./How-to-Connect-to-the-Operations-Console.md)
[Using the Operations Manager Consoles](./Using-the-Operations-Manager-Consoles.md)


