---
ms.assetid: 2e50e81c-96f5-4a4d-8dd1-dd57470e91be
title: Distributed Deployment of Operations Manager
description: This article highlights the distributed deployment configuration of Operations Manager and references each role to install.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Distributed deployment of Operations Manager

A distributed installation of management groups forms the foundation of most System Center Operations Manager deployments. It enhances scalability by allowing for the distribution of features and services across multiple servers. It can include all Operations Manager server roles, and it supports the monitoring of devices across trust boundaries by using the gateway server.

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
