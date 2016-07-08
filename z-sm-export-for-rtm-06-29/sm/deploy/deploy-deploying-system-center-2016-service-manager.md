---
title: Deploying System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 125912d9-f349-498d-920c-74519c667f48
 

















---
# Deploying System Center 2012 - Service Manager
This guide helps you deploy System Center 2012 - Service Manager in one of several different scenarios. The scenarios range from a simple, one\-computer scenario to a four\-computer scenario that is designed to support production\-type environments. In addition, this guide shows you how to register a Service Manager management group with the Service Manager data warehouse so that you can generate reports. You have the option of deploying the Self-Service Portal so you can provide access to Service Manager through a web browser. To improve performance and provide for redundancy, you can deploy additional secondary Service Manager management servers.  
  
> [!NOTE]  
>  It is assumed in this guide that you are installing Service Manager on a computer where no previous version of Service Manager is installed. For information about upgrading System Center 2012 - Service Manager, see the [Upgrade Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209667).  
  
 This guide also describes how to find and read the Setup log if you encounter issues when you deploy Service Manager. And, finally, information about backing up Service Manager management server encryption keys is included. After you run Setup, the Encryption Key Backup and Restore Wizard starts automatically.  
  
## Deployment Guide Topics  
  
-   [Before You Deploy System Center 2012 \- Service Manager](../../../sm/deploy/deploy-guide/Before-You-Deploy-System-Center-2012---Service-Manager.md)  
  
     Contains preliminary information you must consider before you can deploy Service Manager.  
  
-   [Turkish Language Collations](../../../sm/deploy/deploy-guide/Turkish-Language-Collations.md)  
  
     Describes a potential problem with the installation of a Service Manager database that is not supported on a computer running SQL Server that uses a Turkish language collation.  
  
-   [Prerequisite Checker for System Center 2012 \- Service Manager](../../../sm/deploy/deploy-guide/Prerequisite-Checker-for-System-Center-2012---Service-Manager.md)  
  
     Describes the prerequisite checker that runs as a part of the setup procedure.  
  
-   [Deployment Scenarios for System Center 2012 \- Service Manager](../../../sm/deploy/deploy-guide/Deployment-Scenarios-for-System-Center-2012---Service-Manager.md)  
  
     Describes how to deploy Service Manager in one\-server, two\-server, and four\-server topologies.  
  
-   [Guidance for Installing System Center 2012 \- Service Manager on Virtual Machines](../../../sm/deploy/deploy-guide/Guidance-for-Installing-System-Center-2012---Service-Manager-on-Virtual-Machines.md)  
  
     Provides information that you have to consider when you install Service Manager in a Hyper\-V virtual environment.  
  
-   [Registering with the Service Manager Data Warehouse to Enable Reporting](../../../sm/deploy/deploy-guide/Registering-with-the-Service-Manager-Data-Warehouse-to-Enable-Reporting.md)  
  
     Describes how to run the Data Warehouse Registration Wizard to register the Service Manager management group with the Service Manager data warehouse management server. Registering with the data warehouse makes it possible for you to run reports.  
  
-   [Deploying Additional Service Manager Management Servers](../../../sm/deploy/deploy-guide/Deploying-Additional-Service-Manager-Management-Servers.md)  
  
     Describes how to install additional Service Manager management servers to improve performance.  
  
-   [Deployment Considerations with a Disjointed Namespace](../../../sm/deploy/deploy-guide/Deployment-Considerations-with-a-Disjointed-Namespace.md)  
  
     Describes additional steps you must take when you deploy either an additional Service Manager management server or Self-Service Portal in an environment with a disjoint namespace.  
  
-   [Self\-Service Portal for System Center 2012 \- Service Manager](../../../sm/deploy/deploy-guide/Self-Service-Portal-for-System-Center-2012---Service-Manager.md)  
  
     Describes how to deploy and troubleshoot the Service Manager Self-Service Portal.  
  
-   [Guidance for Load Balancing System Center 2012 \- Service Manager](../../../sm/deploy/deploy-guide/Guidance-for-Load-Balancing-System-Center-2012---Service-Manager.md)  
  
     Describes how you can configure Windows Server 2008 Network Load Balancing with Service Manager.  
  
-   [Completing Deployment by Backing Up the Encryption Key](../../../sm/deploy/deploy-guide/Completing-Deployment-by-Backing-Up-the-Encryption-Key.md)  
  
     Describes how to use the Encryption Key Backup or Restore Wizard to back up and restore encryption keys.  
  
-   [Indexing Non\-English Knowledge Articles](../../../sm/deploy/deploy-guide/Indexing-Non-English-Knowledge-Articles.md)  
  
     Describes how to resolve an indexing issue in SQL Server 2008 Service Pack 1 \(SP1\) in an environment where you create, or plan to create, knowledge articles in any language other than English.  
  
-   [Troubleshooting System Center 2012 \- Service Manager Deployment Issues](../../../sm/deploy/deploy-guide/Troubleshooting-System-Center-2012---Service-Manager-Deployment-Issues.md)  
  
     Describes the logs files that are created when you install Service Manager and how you can use these logs to troubleshoot deployment issues.  
  
-   [Deploying Service Manager from a Command Line](../../../sm/deploy/deploy-guide/Deploying-Service-Manager-from-a-Command-Line.md)  
  
     Describes how to deploy Service Manager using command\-line parameters.  
  
-   [Appendix A \- Command\-Line Option Error Codes](../../../sm/deploy/deploy-guide/Appendix-A---Command-Line-Option-Error-Codes.md)  
  
     Lists error codes used in command\-line installation.  
  
-   [Appendix B \- Guidance for Moving the Service Manager and Data Warehouse Databases](../../../sm/deploy/deploy-guide/Appendix-B---Guidance-for-Moving-the-Service-Manager-and-Data-Warehouse-Databases.md)  
  
     Provides prescriptive and how\-to guidance about moving Service Manager databases.  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)  
  
-   [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670)  
  
-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)  
  
## Downloadable Documentation  
 You can download a [copy of this technical documentation from the Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=246620). Always use the TechNet library for the most up\-to\-date information.
