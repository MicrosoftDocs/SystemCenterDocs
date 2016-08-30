---
title: Operations Manager Planning Guide
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Operations Manager Planning Guide

By deploying System Center 2016 - Operations Manager in your environment, you can provide your organization with a monitoring service that ensures IT and business service owners are able to effectively monitor and report on the availability and performance metrics of their services across on-premises, service provider, and cloud environments.  After you identify the deployment tasks and current environment for your organization, you can create the Operations Manager deployment strategy that meets your organization’s service operations needs.  

## About this guide

This guide provides recommendations to help you develop an Operations Manager deployment strategy based on the requirements of your organization and the particular design that you want to create.  This guide is intended for use by infrastructure specialists or system architects.  Before you read this guide, you should have a good understanding of how Operations Manager works on a functional level. You should also have a good understanding of the organizational and business requirements that need to be considered in your deployment strategy.  

This guide describes sets of tasks for several possible starting points of a System Center 2016 - Operations Manager deployment.  The guide helps you determine the most appropriate deployment strategy for your environment.

The strategies that are presented in this guide are appropriate for many common Operations Manager deployments, and they have been tested and validated for environments that contain up to the capacity limits stated in the [System Requirements](system-requirements.md) article.  


## Planning guide topics

[Planning a Management Group Design](planning-a-management-group-design.md)

Describes the components that an Operations Manager management group is composed of, such as a management server, a SQL Server hosting the operational and data warehouse databases, and the Operations Manager Operations console.  This section also includes important design considerations for each component.  

[SQL Server Design Considerations](planning-sqlserver-design.md)

Describes the most appropriate high availability, disaster recovery, and performance configuration for SQL Server hosting the Operations Manager databases in order to achieve optimal performance and scale in medium to enterprise deployments.

[Integration with other enterprise management products](planning-integration-with-other-management-solutions.md)

Integration with other ITSM management, monitoring solutions, or custom solutions that extend Operations Manager to support your service operations framework are discussed with design recommendations.

[Monitoring Agent Overview and Deployment Considerations](planning-agents.md)

Provides an overview of the Windows and UNIX/Linux agent and the software, security and deployment requirements and considerations that you need to understand before proceeding with your deployment of Operations Manager.




