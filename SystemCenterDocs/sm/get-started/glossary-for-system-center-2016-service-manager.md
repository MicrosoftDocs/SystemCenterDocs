---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Glossary for System Center 2016 Service Manager
ms.technology:  service-manager
ms.assetid:  70310c2d-c8f0-4e6c-a276-1284c52f096f
---

# Glossary for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

|Term|Definition|
|--------|--------------|
|action log|A record of the actions that have been taken during the lifetime of an incident to resolve the incident. Examples include comments by the analyst, communications from the user, attachments, and task outputs.|
|activity|A unit of work that is performed as part of managing a problem, resolving an incident, or completing a change request or any other work item.|
|activity implementer|A user who has been assigned the Activity Implementer role and who implements an assigned manual activity.|
|automated activity|An activity that is automatically completed by Service Manager.|
|business hours|Working hours and holiday hours that are defined in a calendar.|
|business service|A collection of features and functions that enable a business process, including configuration items, metadata, and the people associated with the process.|
|change creator|The user who creates a new change request.|
|change manager|A user who coordinates change requests. Some of the tasks include adding or removing activities, voting on behalf of the change advisory board, overriding votes, or putting change requests on hold.|
|change request|A means of proposing a change to any component of an IT infrastructure or any aspect of an IT Service. It may be a document or record in which the nature and details of and the justification and authorization for the proposed change are entered.|
|child record|A work item that is subordinate to a parent.|
|class|A named descriptor for a set of objects that share the same attributes, operations, methods, relationships, and behaviors.|
|classification|The placement of an incident into a hierarchy of descriptors that indicate what the incident is generally about. For example, an incident could be classified as being related to software, and then to Microsoft, and then to Word 2016.|
|combination class|A feature in Service Manager that is used mostly in reports and in views to display information from multiple classes that are defined in Service Manager.|
|configuration item|Any component that needs to be managed to deliver a service. In Service Manager, configuration items might include services, hardware, software, buildings, people, and formal documentation, such as process documentation and service level agreements (SLA).|
|configuration item class|A collection of configuration items. Groups can contain members of different configuration items classes (for example, a computer and a user).|
|connector|A software component that is the integration mechanism between Service Manager and an external system. It is used for data transfers from these external systems to Service Manager.|
|dependent change management activity|A change management activity that is used to link change requests to a release record.|
|DWDataMart database|The database that includes the reporting data, stored for the long-term.|
|DWRepository database|The database that includes the transformed data from the DWStagingAndConfig database.|
|DWStagingAndConfig database|The database that includes copies of management packs, configuration items, and work items.|
|extraction, transformation, and loading|The act of extracting data from various sources, transforming data to consistent types, and loading the transformed data for use by applications.|
|filtered view|A view to which a set of conditions have been applied to reduce the total number of displayed objects.|
|groom|To permanently remove data from the data warehouse.|
|history|A record of all the changes to an object&trade;s properties and relationships. History exists for all objects, such as configuration items and work items."|
|incident|A way of tracking any event that is not part of the standard operation of a service and that causes, or may cause, an interruption to, or a reduction in, the quality of that service.|
|knowledge|Information that can help an end-user or analyst solve a problem.|
|list|An administrator-defined customization that enables users to classify objects such as incidents, change requests, activities, or configuration items. For example, a list might be "Location" or "Organization."|
|list item|An option that constrains the values that users can enter for a specific list. For example, "Redmond" might be a list item for "Location."|
|management pack|A grouping of classes, workflows, views, forms, reports, and knowledge that extends Service Manager with the information necessary to implement all or part of a service management process. For example, the Incident management pack provides the necessary information to enable Service Manager to implement the incident management process.|
|notification subscriber|The user who receives notifications.|
|notification subscriber address|A package that contains information about how to reach a particular user. It includes items such as the protocol to use and the target address.|
|notification subscription|A package that contains the notification subscriber, the notification subscriber address, and any additional information, such as when to send specific types of notifications|
|parent record|The highest-level container of one or more work items that includes new and changed configuration items.|
|problem management|The process by which the root cause of one or more incidents is identified and by which a workaround or a permanent fix is found.|
|problem record|A record that tracks the identification, investigation, and resolution of a root cause.|
|queue|A holding container for work items. Members of a queue must be of the same work item class (for example, only incidents).|
|recurring notification|A repeating type of notification that is based on a specified time interval.|
|release activity|A type of activity that is part of a release record, including dependent, manual, parallel, review, and sequential activities.|
|review activity|A step in a review process in which users approve or deny change requests.|
|reviewer|The user who completes an approval activity.|
|role-based security|A method of limiting access to the Service Manager console.|
|runbook|The sequence of activities that orchestrate actions on computers and networks.|
|Self-Service Portal|A Web interface that is configured by an administrator so that end users can search knowledge, create requests, and read IT announcements.|
|service catalog|The list of published service offerings.|
|service component|The set of configuration items that are used to deliver a business service, such as computers, Web sites, databases, and other application components.|
|service dependent|The person or service in an enterprise that relies on a business service. These people and services are affected by the output and downtime of the business service.|
|Service Manager console|The console that is used by help desk analysts and administrators for help desk functions such as change, incident, problem, and configuration management.|
|Service Manager data warehouse management server|The Service Manager management server that performs the management functions for the data warehouse.|
|Service Manager database|A database that includes all the work items, configuration items, and administrative settings for the product.|
|Service Manager IT portal|A Web interface designed for information technology (IT) managers and IT professionals so that they can view and manage incidents, changes, and assets. It can also be used to examine metrics and reports.|
|Service Manager management server|The server that hosts the System Center Data Access Service service and Microsoft Office SharePoint sites.|
|Service Manager reporting server|The server that hosts Microsoft SQL Server Reporting Services (SSRS).|
|service map|A representation of a service from the perspective of the business and user that shows critical dependencies, settings, and areas of responsibility.|
|service offering|The item or work effort that is available to customers through the Self-Service Portal in the service catalog.|
|service request|A work item that is used to request an existing IT service that is being offered.|
|service request fulfillment|The process for managing service requests.|
|SLA|An industry-wide term that is detailed in the Microsoft Operations Framework (MOF) and Information Technology Infrastructure Library (ITIL). Microsoft Solutions Framework (MSF) definition: An agreement between an IT organization and the user community that defines the responsibilities of all participating parties and that binds IT management to provide a particular service of a specific agreed-on quality and quantity. An SLA limits the demands that users may place on the service to the limits that are defined by the agreement.|
|SLA metric|A calculated time interval that Service Manager determines between the date and time fields in incidents and service requests. For example, the SLA metric resolution time is defined as the difference between the Incident Created Date and the Incident Resolved Date.|
|SLA target|The specified duration of time in which the IT organization must respond to or resolve an incident or service request.|
|SQL Server Analysis Services cube|(Analysis Services cube for short.) A conceptual view, consisting of descriptive categories (dimensions) and quantitative values (measures). The generic industry term is "OLAP data cube."|
|task|An action that a user accomplishes by using the Actions pane and the context-sensitive menu that affects non-Service Manager objects.|
|Tasks pane|A pane in the Service Manager console that contains tasks that a user can perform.|
|template|A method that is used to populate initial values in a class, such as a change request or incident.|
|user role|A method of granting permissions to specific users for groups of data. These permissions are based on a user role profile.|
|user role profile|A set of permitted operations and classes of data that users need access to so they can perform specific job duties.|
|workflow|A sequence of activities, actions, or tasks through which documents or items are passed as part of an automated business process.|
