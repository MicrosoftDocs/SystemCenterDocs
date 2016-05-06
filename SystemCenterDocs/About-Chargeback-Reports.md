---
title: About Chargeback Reports
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d4d2c54-b812-4d83-af58-9345b43a05d5
---
# About Chargeback Reports
As traditional IT transitions into a cloud\-optimized IT, service providers are facing a new set of challenges that places a high demand on them. One of the goals of System Center 2016 is to enable and help you, the service provider, to manage the transition, and to help you succeed in your offerings.

In traditional IT, infrastructure was largely physical, service level agreements \(SLAs\) were typically periods of weeks and months, and capacity was owned and managed by the consumers. However, this is no longer true. With the arrival of centrally pooled resources, on\-demand self\-service, and short SLAs, service consumers can continue their old habits, which are to over\-subscribe and underutilize, without having to carry the burden of managing the acquired capacity. If not managed properly, the ability of the service provider can be compromised in these situations.

In System Center, chargeback is one of the tools that help you communicate with business units about how they consume capacity. This helps you by utilize existing investments, proportionate to your customer’s requests. System Center components help you manage the following processes:

-   Quotas

-   Leases

-   Approvals

-   Chargeback or showback

The theme of chargeback is cloud based pricing, where each cloud has its own price, based on SLA. Most often, you’ll have many clouds with various SLAs for the clouds for different business units or organizations. Chargeback uses a price sheet, or rate card, for each cloud. This means you can have one price represented in a price sheet that contains various clouds addressing one SLA, and you can have another price sheet for a different SLA.

Specifically, Chargeback in [!INCLUDE[smshort12]./Token/smshort12_md.md)] uses information discovered from the Operations Manager CI connector about the Virtual Machine Manager fabric that you manage. The private cloud information from Virtual Machine Manager, such as clouds and virtual machines, is what helps define a successful private cloud by offering centrally pooled resources that are metered and charged based on consumption.

Price sheets, or rate cards, are created in [!INCLUDE[smshort]./Token/smshort_md.md)] for Virtual Machine Manager clouds. The clouds are then assigned to prices sheets. For example, you might have price sheets that are associated to silver and bronze clouds in order to differentiate levels of service.

Service Manager comes with a sample report, but its reporting infrastructure is OLAP cube\-based, so you can easily create your own reports. You can easily customize the sample report with colors, logos, or whatever you can think of that will best suit your needs. You can use the OLAP cube information presented in the Data Warehouse workspace to easily create a simple pivot table in Microsoft Excel. After you select fields you like, you can format the data any way you like just like you would any other information in Excel.

It’s important to let customers know that IT resources are limited in their capacity. You can use chargeback or showback reports to show resource utilization and the associated costs to influence consumption behaviors.

## Operations Manager Requirements
Before you can use chargeback reports, you must create and synchronize an Operations Manager CI connector so that Operations Manager discovers virtual machine resources from Virtual Machine Manager. Earlier versions of Virtual Machine Manager are not supported with Chargeback. During this process, you must synchronize the VMM.2016.Discovery management pack. [!INCLUDE[crabout]./Token/crabout_md.md)] creating and synchronizing an Operations Manager CI connector, see [How to Create a System Center Operations Manager Connector](http://go.microsoft.com/fwlink/p/?LinkId=229670). The following object properties are imported into [!INCLUDE[smshort]./Token/smshort_md.md)] using the connector:

-   virtual machine CPU count

-   virtual machine memory

-   virtual machine storage

-   virtual network interface cards

-   virtual disks

-   virtual machines – this is used to collect a fixed price for virtual machines other than for virtual machine components

-   clouds – used to collect cloud membership price for clouds other than virtual machine or virtual machine component costs




