---
ms.assetid: 2e50e81c-96f5-4a4d-8dd1-dd57470e91be
title: Distributed Deployment of Operations Manager
description: This article highlights the distributed deployment configuration of Operations Manager and references each role to install.
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.date: 02/03/2026
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.update-cycle: 1095-days
---

# Distributed deployment of Operations Manager

Most System Center Operations Manager deployments use a distributed installation of management groups. This installation enhances scalability by distributing features and services across multiple servers. A distributed deployment can include all Operations Manager server roles. By using the gateway server, it supports monitoring devices across trust boundaries.

## Operations Manager features

This configuration supports all Operations Manager features:

- Monitoring and alerting, targeted for up to 15,000 agents
- Monitoring across trust boundaries
- Reporting
- Audit collection
- Agentless exception management
- Agent failover between management servers
- Gateway failover between management servers
- Clustering high availability for database roles

## Operations Manager server roles

This configuration supports all Operations Manager server roles:

- Audit Collection Services (ACS) collector
- ACS database
- ACS forwarder (on agent-managed devices)
- Gateway server
- Management server
- Operational database
- Operations console
- Reporting server
- Reporting data warehouse database
- Web console server

## Related content

This section of the deployment guide contains the following topics:

- [Install an Operations Manager management server](deploy-install-mgmt-server.md)
- [Install the Operations Manager operations console](deploy-install-ops-console.md)
- [Install the Operations Manager web console](deploy-install-web-console.md)
- [Create folders from the Operations Manager web console](support-folders-monitoring-view-web-console.md)
- [Install an Audit Collection Services collector and database](deploy-install-acs.md)
- [Install an Operations Manager reporting server](deploy-install-reporting-server.md)
- [Connect to the reporting data warehouse across a firewall](deploy-connect-reportingdw-firewall.md)
- [Install an Operations Manager gateway server](deploy-install-gateway-server.md)
