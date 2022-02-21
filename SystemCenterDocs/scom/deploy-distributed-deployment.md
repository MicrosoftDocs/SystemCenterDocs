---
ms.assetid: 2e50e81c-96f5-4a4d-8dd1-dd57470e91be
title: Distributed Deployment of Operations Manager
description: This article highlights the distributed deployment configuration of Operations Manager and references each role to install.
author: jyothisuri
ms.author: jsuri
manager: carmonm
ms.date: 11/08/2017
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Distributed deployment of Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

The distributed management group installation will form the foundation of 99 percent of Operations Manager deployments. It allows for the distribution of features and services across multiple servers to allow for scalability. It can include all Operations Manager server roles and supports the monitoring of devices across trust boundaries through the use of the gateway server.

## System Center - Operations Manager features

This configuration supports all System Center - Operations Manager features:

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

-   [How to install an Operations Manager management server](deploy-install-mgmt-server.md)

-   [How to install the Operations console](deploy-install-ops-console.md)

-   [How to install the Operations Manager Web console](deploy-install-web-console.md)

-   [How to install an Audit Collection Services (ACS) collector and database](deploy-install-acs.md)

-   [How to install the Operations Manager Reporting server](deploy-install-reporting-server.md)

-   [How to deploy a gateway server](deploy-install-gateway-server.md)
