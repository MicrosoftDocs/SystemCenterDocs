---
ms.assetid: 2e50e81c-96f5-4a4d-8dd1-dd57470e91be
title:  Distributed Deployment of Operations Manager
description: This article highlights the distributed deployment configuration of Operations Manager and references each role to install. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Distributed deployment of Operations Manager

>Applies To: System Center 2016 - Operations Manager

The distributed management group installation will form the foundation of 99 percent of Operations Manager deployments. It allows for the distribution of features and services across multiple servers to allow for scalability. It can include all Operations Manager server roles and supports the monitoring of devices across trust boundaries through the use of the gateway server.

## System Center 2016 - Operations Manager features

This configuration supports all System Center 2016 - Operations Manager features:

-   Monitoring and alerting, targeted for up to 15,000 agents

-   Monitoring across trust boundaries

-   Reporting

-   Audit collection

-   Agentless exception management

-   Agent failover between management servers

-   Gateway failover between management servers

-   Clustering high availability for database roles

## Operations Manager server roles

This configuration supports all Operations Manager server roles:

-   Audit Collection Services (ACS) collector

-   ACS database

-   ACS forwarder (on agent-managed devices)

-   Gateway server

-   Management server

-   Operational database

-   Operations console

-   Operations Manager Reporting server

-   Reporting data warehouse database

-   Web console server


This section of the Deployment Guide contains the following topics:

-   [How to install an Operations Manager management server](../om/deploy/how-to-install-an-operations-manager-management-server.md)

-   [How to install the Operations console](../om/deploy/how-to-install-the-operations-console.md)

-   [How to install the Operations Manager Web console](../om/deploy/how-to-install-the-operations-manager-web-console.md)

-   [How to install an Audit Collection Services (ACS) collector and database](../om/deploy/how-to-install-an-audit-collection-services-acs-collector-and-database.md)

-   [How to install the Operations Manager Reporting server](../om/deploy/how-to-install-the-operations-manager-reporting-server.md)

-   [How to deploy a gateway server](../om/deploy/how-to-install-a-gateway-server.md)





