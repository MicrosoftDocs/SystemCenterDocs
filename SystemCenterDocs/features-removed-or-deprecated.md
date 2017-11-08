---
description: This topic lists the features and functionality that have been removed or replaced in System Center 2016.
manager:  cfreeman
ms.topic:  article
author:  cfreemanwa
ms.author: raynew
ms.prod:  system-center-threshold
keywords:
ms.date:  2016-10-12
title:  Features Removed or Deprecated from System Center 2016
ms.technology:  system-center-2016
ms.assetid:  b6f468e0-fa52-41f3-8b2d-9e07ede377c9
---

# Features Removed or Deprecated from System Center 2016

The features and capabilities  listed below  are not included in the System Center 2016. Applications, code, or usage that depends  on these features will not function in this release unless you employ an alternate method. This list is subject to change in subsequent releases and may not include every removed feature or capability.

## Silverlight based Self Service Portal for System Center Service Manager
**Status in System Center 2016:** Removed.

**Replacement:** A new HTML based Self Service Portal is available with System Center 2016 - Service Manager.

## App Controller
**Status in System Center 2016:** Removed.

**Replacement:** For on-premises deployments, provision IaaS and PaaS solutions using [Windows Azure Pack](https://technet.microsoft.com/en-us/library/dn296435.aspx). Additionally, virtual machine and PaaS self-service solutions are available in Windows Azure Pack and Azure.


## Citrix XenServer and VMware vCenter 4.1/5.1 support in Virtual Machine Manager
**Status in System Center 2016:** Removed.

**Replacement:** Use VMware 5.5 and 5.8

## Microsoft IT GRC Process Management Pack SP1 for Service Manager
**Status in System Center 2016 :** Removed.

**Replacement:** We recommend that you engage with proactive governance partners that can integrate into your current System Center investments.

## Server App-V support
**Status in System Center 2016:** Removed.

**Replacement:** Migrate workloads to virtualized platforms using templates

You will not be able to either create or import a service templates with a Server App-V package in System Center 2016 - Virtual Machine Manager.  If you upgrade from System Center 2012 Virtual Machine Manager to System Center 2016 - Virtual Machine Manager, and you are managing applications based on service templates with Server App-V packages, you can continue to manage those applications with VMM, but you will not be able to upgrade the application. The following list describes the limitations for using Server App-V when you upgrade to System Center 2016 - Virtual Machine Manager:

## Service Manager Cloud Service Process Pack (CSPP)
**Status in System Center 2016:** Removed.

**Replacement:** Use Windows Azure Pack for Windows Server instead.

## Authoring Management Packs for Operations Manager with Visio
**Status in System Center 2016:** Removed.

**Replacement:** Use the complimentary version of Silect's MP Author to design and develop MPs for Operations Manager or customize existing MPs.

## Service Reporting
**Status in System Center 2016:** Removed

**Replacement:** Integrate your Windows Azure Pack installation with a third-party billing and utilization system.


## Next Steps

See [Upgrade to System Center 2016](upgrade-to-system-center-2016.md).
Go to the [System Center documentation center](index.md), to see all technologies in System Center 2016.
See the introductory information or important concepts about each of the technologies in System Center 2016. 

* [Data Protection Manager](/system-center/dpm/dpm-overview)
* [Operations Manager](/system-center/scom/key-concepts)
* [Orchestrator](/system-center/orchestrator/learn-about-orchestrator)
* [Service Manager](/system-center/scsm/service-manager)
* [Service Management Automation](/system-center/sma/overview-of-service-management-automation)
* [Virtual Machine Manager](/system-center/vmm/overview)
* [Service Provider Foundation](/system-center/spf/overview)