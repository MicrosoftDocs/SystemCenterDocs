---
title: Connecting Operations Manager With Other Management Systems
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7fd5ca6b-cde4-4610-ba6d-6fbb7ca57373
---
# Connecting Operations Manager With Other Management Systems
Product connectors are used to synchronize [!INCLUDE[om12long](./Token/om12long_md.md)] data with other management systems, such as those that monitor non\-Windows computers or create trouble\-tickets. Product connectors can integrate a deployment of Operations Manager into another management platform or connect other management systems into a full Operations Manager management solution.

A unidirectional connector forwards alerts to another management system. A bidirectional connector both forwards alerts to another management system and receives messages from the originating system when the issue is resolved.

## Connections to Other Management Systems
Product connectors allow communication between Operations Manager and other management systems, regardless of whether Operations Manager is the highest level management system or not. If Operations Manager is not the top\-tier management system, a product connector can forward all Windows\-generated alerts for consolidation at another management system. If the connector is bidirectional, Operations Manager can update the state of the monitored component in the Operations Console when it receives notification from the top\-level management system. If Operations Manager is the top\-tier management system, a product connector allows it to receive and consolidate alert information from another management system.

## Operations Manager and Trouble\-Ticketing Systems
In [!INCLUDE[om12short](./Token/om12short_md.md)], alerts occur when an issue requires action. A trouble\-ticketing system can automatically open trouble tickets when it receives an alert generated from Operations Manager via a product connector.

## Product Connector Installation
If you want to connect to a particular management system, you should ask the vendor of that management system for a product connector. Installation instructions should be included in the download of the product connector files. After a product connector is installed, you can configure which events you want the product connector to accept or forward using subscriptions. The product connectors you install are displayed in the Administration workspace in **Product Connectors**. See [How to Configure a Product Connector Subscription](./How-to-Configure-a-Product-Connector-Subscription.md) for more information.

## Connecting Operations Manager With Other Management Systems topics
[How to Configure a Product Connector Subscription](./How-to-Configure-a-Product-Connector-Subscription.md)

## Other resources for this component

-   [TechNet Library main page for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=223634)

-   [Operations Guide for System Center 2012 - Operations Manager](./Operations-Guide-for-System-Center-2012---Operations-Manager.md)

-   [Initial Monitoring After Operations Manager Is Installed](./Initial-Monitoring-After-Operations-Manager-Is-Installed.md)

-   [Managing Access in Operations Manager](./Managing-Access-in-Operations-Manager.md)

-   [Getting Information from Operations Manager](./Getting-Information-from-Operations-Manager.md)

-   [General Tasks in Operations Manager_1](./General-Tasks-in-Operations-Manager_1.md)

-   [Maintenance of Operations Manager](./Maintenance-of-Operations-Manager.md)

-   [Operations Manager Report Authoring Guide](http://go.microsoft.com/fwlink/p/?LinkID=217092)

-   [Managing Discovery and Agents](./Managing-Discovery-and-Agents.md)


