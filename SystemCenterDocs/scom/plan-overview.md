---
ms.assetid: d101c474-7a4d-4a01-b52a-a22270c475d0
title: Operations Manager Planning Guide
description: This article is the landing page for the planning guide supporting System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Operations Manager Planning Guide


By deploying System Center Operations Manager in your environment, you can provide your organization with a monitoring service that ensures IT and business service owners are able to effectively monitor and report on the availability and performance metrics of their services across on-premises, service provider, and cloud environments.  After you identify the deployment tasks and current environment for your organization, you can create the Operations Manager deployment strategy that meets your organization’s service operations needs.  

## About this guide

This guide provides recommendations to help you develop an Operations Manager deployment strategy based on the requirements of your organization and the particular design that you want to create.  This guide is intended for use by infrastructure specialists or system architects.  Before you read this guide, you should have a good understanding of how Operations Manager works on a functional level. You should also have a good understanding of the organizational and business requirements that need to be considered in your deployment strategy.  

This guide describes sets of tasks for several possible starting points of a System Center Operations Manager deployment.  The guide helps you determine the most appropriate deployment strategy for your environment.

The strategies that are presented in this guide are appropriate for many common Operations Manager deployments, and they have been tested and validated for environments that contain up to the capacity limits stated in the [System Requirements](./system-requirements.md) article.  


## Planning guide topics

- [System Requirements for Operations Manager](./system-requirements.md)

    Provides information about the supported operating systems, hardware configurations, software requirements, installation combinations, and other important design planning considerations that are summarized and recommended for Operations Manager.

- [Supported Versions of Linux and UNIX](plan-supported-crossplat-os.md)

    Provides the supported and required UNIX and Linux operating systems and package dependencies for Operations Manager.  

- [Review the Cloud Monitoring guide](/azure/architecture/cloud-adoption/operations/monitor/)

    Provides information to help you plan your cloud monitoring strategy, which includes monitoring platform considerations and recommendations, in order to  effectively monitor workloads transitioning to Azure.

- [Planning a Management Group Design](plan-mgmt-group-design.md)

    Describes the components that an Operations Manager management group is composed of, such as a management server, a SQL Server hosting the operational and data warehouse databases, and the Operations Manager Operations console.  This section also includes important design considerations for each component.  

- [SQL Server Design Considerations](plan-sqlserver-design.md)

    Describes the most appropriate high availability, disaster recovery, and performance configuration for SQL Server hosting the Operations Manager databases in order to achieve optimal performance and scale in medium to enterprise deployments.

- [Resource Pool Design Considerations](plan-resource-pool-design.md)

    This section provides information to help you make design decisions and to understand the behavior and deployment options with resource pools to provide high availability for the monitoring of network devices, Linux and UNIX computers, and other workloads in Operations Manager.  

- [Design for High Availability and Disaster Recovery](plan-hadr-design.md)

    Describes the supported and most appropriate high availability and disaster recovery options for your Operations Manager management group to maintain minimum functionality and continued operational insight of the IT services monitored.  

- [Integration with other enterprise management products](plan-thirdparty-integration.md)

    Integration with other ITSM management, monitoring solutions, or custom solutions that extend Operations Manager to support your service operations framework are discussed with design recommendations.

- [Monitoring Agent Overview and Deployment Considerations](plan-planning-agent-deployment.md)

    Provides an overview of the Windows and UNIX/Linux agent and the software, security and deployment requirements and considerations that you need to understand before proceeding with your deployment of Operations Manager.

- [Security Design](plan-security-accounts.md)

    This section provides you with security-related information as it pertains to the planning of security accounts, roles and privileges required for your deployment of Operations Manager.
