---
title: Connect Operations Manager With Other Management Systems
description: This article describes how to integrate Operations Manager with other enterprise management systems and System Center components.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 7fd5ca6b-cde4-4610-ba6d-6fbb7ca57373
---

# Connect Operations Manager with other management systems



Microsoft System Center - Operations Manager interoperates with other management solutions through [System Center - Orchestrator](../orchestrator/learn-about-orchestrator.md) or product connectors built on the [Operations Manager Connector Framework (OMCF)](/previous-versions/system-center/developer/hh328935(v=msdn.10)), which are developed from the Operations Manager Software Development Kit (SDK). The OMCF provides methods and types that you can use to initialize and manage a connector and to get or send operations data. With earlier versions of Operations Manager, the primary means of synchronizing alerts between Operations Manager and other systems was through a connector. An Operations Manager connector created for the other system was required for this purpose, and various connectors have been released by vendors of those management solutions.

Orchestrator integrates with System Center, other Microsoft products, and non-Microsoft products to enable interoperability across the data center.

In Operations Manager, alerts occur when an issue requires action. An ITSM incident management system can automatically create incident records it receives from an alert generated from Operations Manager via a product connector or Orchestrator runbook.

## Orchestrator runbooks

Orchestrator runbooks are the preferred method for synchronizing alert data between Operations Manager and other systems. Runbooks provide the following advantages over connectors:

- More complex logic that potentially includes multiple systems.

- A wider range of supported systems.

- No need for a specific connector since Integration Packs are general purpose.

The System Center Integration Pack for System Center Operations Manager includes activities that retrieve and modify alerts from an Operations Manager management group. The only requirement for the other system is to have an Integration Pack available.  An Integration Pack provides a set of activities that work with a particular application or component, and a single runbook can be made up of activities from multiple Integration Packs. In a connector scenario, the Integration Pack only needs activities specific to the other system and has no specific knowledge of Operations Manager. Information on the Integration Packs is currently available at [Integration Packs for System Center - Orchestrator](/archive/blogs/allthat/system-center-2016-integration-packs).

## Connections to other management systems  

Product connectors allow communication between Operations Manager and other management systems, regardless of whether Operations Manager is the highest level management system or not. If Operations Manager isn't the top-tier management system, a product connector can forward all Windows-generated alerts for consolidation at another management system. If the connector is bidirectional, Operations Manager can update the state of the monitored component in the Operations Console when it receives notification from the top-level management system. If Operations Manager is the top-tier management system, a product connector allows it to receive and consolidate alert information from another management system.  

The one challenge that Orchestrator runbooks have in comparison to connectors is throughput. System Center - Orchestrator is a scalable product with the ability to distribute runbooks across multiple servers. Alert synchronization though typically requires relatively few runbooks (or even a single runbook depending on requirements and complexity) running every time an alert is created or modified. This can create a bottleneck when handling a high volume of alerts.

The connector framework in Operations Manager was designed to be a lightweight technology focused on a single function supporting a high volume of alerts.

::: moniker range="sc-om-2016"
System Center 2016 and later has the same connector framework from Operations Manager 2012/2012 R2 and 2007 R2. New connectors can be created using the Operations Manager Connector Framework. Verify from your vendor if the existing connector released for Operations Manager 2012/2012 R2 will work without modification for Operations Manager 2016 and later.
::: moniker-end

## System Center Integration

### Virtual Machine Manager

In System Center, Virtual Machine Manager integrates directly with Operations Manager in addition to using the System Center Monitoring Pack for System Center - Virtual Machine Manager for monitoring of the health of all resources in a VMM environment. This additional integration is what allows VMM to display Operations Manager data in the VMM console and to control maintenance mode during VMM operations. You can also manage the installation of management packs through VMM rather than performing this installation directly in Operations Manager as you do with the other components. Guidance on configuring this integration is provided in [Configuring Operations Manager Integration with VMM](../vmm/monitors-ops-manager.md).

VMM performs some actions using the Operations Manager SDK that are typically performed with management packs for other products. For example, several VMM objects are created without using object discoveries. One example of this is the Virtual Machine object. If you select this class in the Object Discoveries node in the Authoring workspace of the Operations Manager, no object discoveries are listed. Instead of relying on a discovery in the management pack, VMM creates these objects through the Operations Manager SDK whenever a new virtual machine is created or modified.

There's nothing that the vendor of resources that are used by VMM must do to have those resources discovered and monitored. If the resource is recognized by VMM, then it will be discovered and monitored by the monitoring pack.  Vendors are still encouraged to create monitoring packs for their own resources though to provide any deep monitoring specific to their product.  While the VMM monitoring pack may be able to identify that the resource is offline, it would be unable to provide detailed analysis to the root cause of the problem and potential remedies.

### Service Manager

Service Manager integrates with Operations Manager through two types of connectors that are both created and configured in the Service Manager console.

* The Configuration Items connector imports objects from Operations Manager as Configuration Items in Service Manager.  Discoveries in Operations Manager locate resources and their properties on managed computers, and the connector allows these objects to be automatically imported into Service Manager.
* The Alerts connector imports alerts as they're created from Operations Manager into Service Manager.  They're created in Service manager as incidents where they can be managed. The incident then remains in synchronization with the alert, allowing it to be closed when the incident is resolved.

#### Management Pack

The System Center Monitoring Pack for System Center - Service Manager allows Operations Manager to monitor the health of a Service Manager environment. It discovers Service Manager management servers and data warehouse and measures the health of its services.

The Operations Manager agent can't be installed on a Service Manager management server because Service Manager uses the System Center Management service to process its own management packs. To monitor a Service Manager management server, you must configure it to use agentless monitoring, which allows Operations Manager to process its management packs on an Operations Manager management server.  Once the computer is added to the Operations Manager management group in this manner, it's monitored like any other computer.  The only exception is that it won't run any rules or monitors that don't support an agentless scenario.

## Orchestrator

The System Center Integration Pack for System Center Operations Manager includes activities that allow you to create a runbook in System Center - Orchestrator that interacts with Operations Manager.  You can perform many of the functions that you can perform with Windows PowerShell cmdlets only within the context of an Orchestrator runbook.
The activities included in the Operations Manager Integration Pack address the following scenarios:

* Retrieve and modify alerts. This includes the ability to monitor for an alert to be created or changed, a feature that directly supports the connector scenario with other management systems.  
* Get the current health state of one or more monitored objects.  
* Start and stop maintenance mode.  

The Operations Manager Integration Pack allows you to create one or more connections to Operations Manager management servers that can be used by its activities. Each connection holds the security configuration required to access a management group. You can create a runbook with multiple activities that share a single configuration so that you don’t have to maintain separate credentials and connections for each activity.

If you need to perform an Operations Manager action from a runbook that doesn’t have an activity, then you can write a script using one or more of the Operations Manager cmdlets  and then run this script from a [Run .NET Script](/previous-versions/system-center/system-center-2012-R2/hh206103(v=sc.12)) activity.  In this case, the Operations Manager cmdlets would need to be installed on the runbook server.  The script would also need to include a connection to the Operations Manager management group using the [New-SCOMManagementGroupConnection](/previous-versions/system-center/powershell/system-center-2012-r2/hh920188(v=sc.20)) cmdlet.  If the account used for the Orchestrator Runbook Service doesn't have authority to the Operations Manager management group, then alternate credentials would need to be provided for this connection.  In this case, the name and password could be stored as encrypted variables in Orchestrator so that they wouldn't have to be hardcoded into the script.

The activities in the Operations Manager Integration Pack connect to Operations Manager using the Operations Manager SDK, which means that they connect to the Data Access service on a management server.

### Management Pack

In System Center, the [management pack for Orchestrator](https://www.microsoft.com/download/details.aspx?id=54058) discovers and measures the health of Orchestrator components such as management servers and runbook servers.  It doesn't discover runbooks, nor does it monitor at the runbook level.  For example, the management pack will send an alert if the runbook service on a runbook server fails, but it won't alert if a runbook fails.

The recommended strategy to raise an alert in Operations Manager if a runbook fails is to include one or more [Create Alert](/previous-versions/system-center/packs/hh830722(v=technet.10)) activities that raise an alert if a previous activity doesn't succeed.

## Product Connector installation  

If you want to connect to a particular management system, you should ask the vendor of that management system for a product connector. Installation instructions should be included in the download of the product connector files. After a product connector is installed, you can configure which events you want the product connector to accept or forward using subscriptions. The product connectors you install are displayed in the Administration workspace in **Product Connectors**. For more information, see [How to Configure a Product Connector Subscription](manage-integration-config-integration.md).  

## Next steps

- To learn more about System Center - Orchestrator and how it can support integration between Operations Manager and other System Center or third-party management systems, see [Getting Started with Orchestrator](../orchestrator/learn-about-orchestrator.md).

- To understand how to write a custom product connector to integrate with an enterprise management system or automate and extend Operations Manager depending on your advanced requirements, review the [Operations Manager SDK](/previous-versions/system-center/developer/hh329086(v=msdn.10)).
