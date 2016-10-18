---
title: Deploying System Center - Service Manager
description: This guide helps you deploy System Center 2016 - Service Manager in one of several different scenarios.
ms.custom: na
manager:  cfreeman
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 125912d9-f349-498d-920c-74519c667f48
---

# Deploying System Center - Service Manager

>Applies To: System Center 2016 - Service Manager

This guide helps you deploy System Center - Service Manager in one of several different scenarios. The scenarios range from a simple, one\-computer scenario to a four\-computer scenario that is designed to support production\-type environments. In addition, this guide shows you how to register a Service Manager management group with the Service Manager data warehouse so that you can generate reports. You have the option of deploying the Self-Service Portal so you can provide access to Service Manager through a web browser. To improve performance and provide for redundancy, you can deploy additional secondary Service Manager management servers.  

> [!NOTE]  
>  It is assumed in this guide that you are installing Service Manager on a computer where no previous version of Service Manager is installed. For information about upgrading to System Center 2016 - Service Manager, see the [Upgrade Guide for System Center 2016 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209667).  

 This guide also describes how to find and read the Setup log if you encounter issues when you deploy Service Manager. And, finally, information about backing up Service Manager management server encryption keys is included. After you run Setup, the Encryption Key Backup and Restore Wizard starts automatically.  

## Deployment Guide Topics  

-   [Planning Guide System Center - Service Manager](../plan/plan-planning-for-system-center-2016-service-manager.md)  

     Contains information about the various parts of Service Manager, the hardware and software requirements, the port assignments, and the information about the accounts you must use to deploy Service Manager. it also contains information about the accounts that you need to create for use with Service Manager.

-   [Turkish Language Collations](deploy-turkish-language-collations.md)  

     Describes a potential problem with the installation of a Service Manager database that is not supported on a computer running SQL&nbsp;Server that uses a Turkish language collation.  

-   [Prerequisite Checker for System Center - Service Manager](deploy-prerequisite-checker-for-system-center-2016-service-manager.md)  

     Describes the prerequisite checker that runs as a part of the setup procedure.  

-   [Deployment Scenarios for System Center - Service Manager](deploy-deployment-scenarios-for-system-center-2016-service-manager.md)  

     Describes how to deploy Service Manager in one\-server, two\-server, and four\-server topologies.  

-   [Guidance for Installing System Center - Service Manager on Virtual Machines](deploy-guidance-for-installing-system-center-2016-service-manager-on-virtual-machines.md)  

     Provides information that you have to consider when you install Service Manager in a Hyper\-V virtual environment.  

-   [Registering with the Service Manager Data Warehouse to Enable Reporting](deploy-registering-with-the-service-manager-data-warehouse-to-enable-reporting.md)  

     Describes how to run the Data Warehouse Registration Wizard to register the Service Manager management group with the Service Manager data warehouse management server. Registering with the data warehouse makes it possible for you to run reports.  

-   [Deploying Additional Service Manager Management Servers](deploy-deploying-additional-service-manager-management-servers.md)  

     Describes how to install additional Service Manager management servers to improve performance.  

-   [Deployment Considerations with a Disjointed Namespace](deploy-deployment-considerations-with-a-disjointed-namespace.md)  

     Describes additional steps you must take when you deploy either an additional Service Manager management server or Self-Service Portal in an environment with a disjoint namespace.  

-   [Self\-Service Portal for System Center 2016 - Service Manager](deploy-deploy-the-self-service-portal-for-service-manager.md)  

     Describes how to deploy and troubleshoot the Service Manager Self-Service Portal.  

-   [Guidance for Load Balancing System Center - Service Manager](deploy-guidance-for-load-balancing-system-center-2016-service-manager.md)  

     Describes how you can configure Windows&nbsp;Server&nbsp;2008 Network Load Balancing with Service Manager.  

-   [Completing Deployment by Backing Up the Encryption Key](deploy-completing-deployment-by-backing-up-the-encryption-key.md)  

     Describes how to use the Encryption Key Backup or Restore Wizard to back up and restore encryption keys.  

-   [Indexing Non\-English Knowledge Articles](deploy-indexing-non-english-knowledge-articles.md)  

     Describes how to resolve an indexing issue in SQL&nbsp;Server&nbsp;2008 Service Pack&nbsp;1 \(SP1\) in an environment where you create, or plan to create, knowledge articles in any language other than English.  

-   [Deploying Service Manager from a Command Line](deploy-deploying-service-manager-from-a-command-line.md)  

     Describes how to deploy Service Manager using command\-line parameters.  

-   [Appendix A \- Command\-Line Option Error Codes](deploy-appendix-a-command-line-option-error-codes.md)  

     Lists error codes used in command\-line installation.  

-   [Appendix B \- Guidance for Moving the Service Manager and Data Warehouse Databases](deploy-appendix-b-guidance-for-moving-the-service-manager-and-data-warehouse-databases.md)  

     Provides prescriptive and how\-to guidance about moving Service Manager databases.  
