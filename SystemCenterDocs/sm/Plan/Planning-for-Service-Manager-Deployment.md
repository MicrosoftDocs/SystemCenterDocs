---
title: Planning for Service Manager Deployment
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e0bf098-9149-4194-bbc4-3b6eaf5f5e8e
---
# Planning for Service Manager Deployment
For [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)], several deployment options are available, and three options are presented in this guide.

The first deployment option uses one physical computer and one virtual computer. The physical computer hosts the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management server, the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] database, and the data warehouse databases, and it also hosts the virtual server. The virtual computer hosts the data warehouse management server. This deployment is used primarily for lightweight or first\-impression evaluation of [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)]. No scalability or performance estimates are available for this scenario.

A second deployment option requires the use of two computers. The first computer hosts the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management server and the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] database. The second computer hosts the data warehouse management server and the data warehouse databases. If you do not need reporting services, you can—at an absolute minimum—install  [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] on one computer that hosts both the Service Manager management server and the Service Manager database.

A third deployment option maximizes performance and scalability by using four computers. Two computers host the management servers, and the remaining two computers host the databases. The computers hosting the databases are the only two computers in this scenario that require the installation of Microsoft SQL Server 2008.

You might decide that, for the evaluation phase, you will choose the option to install [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] on two computers. After installing [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] in the lab, you can import data from Active Directory Domain Services \(AD DS\) and System Center Configuration Manager, and then you can import data and alerts from Operations Manager. You would then configure User Roles within [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] and, if necessary, manually add users that were not imported from AD DS. The following illustration represents an overview of this installation and initial configuration.

![](../../media/SM_Installation_Topology.gif)

You can limit the number of SQL Server licenses that you need by placing all of the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] databases on the same computer, as shown in the following illustration.

![](../../media/SM_Installation_Topology_Single_SQL.jpg)

You continue the deployment process by creating several templates; configuring initial parameters; creating queues, lists, and groups; and then creating a management pack to save these custom objects.

After the evaluation phase is complete, you might install [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] in a production environment and select the deployment scenario in which [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] is installed on four computers.

## Multiple Service Manager Management Servers and One Data Warehouse
The [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management server and its associated [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] database make up a [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management group. The data warehouse management server and its associated databases make up a data warehouse management group. After deploying [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)], you will register the [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management group with the data warehouse management group.

In your enterprise, you might create multiple [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management groups. You can centralize reporting for multiple [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management groups by registering multiple [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] management groups with a single data warehouse management group. For more information, see [How to Run the Data Warehouse Registration Wizard](http://go.microsoft.com/fwlink/p/?LinkID=232303).

## Planning for Deployment Topics

-   [Service Manager Parts](Service-Manager-Parts.md)

    Describes the six major parts of a [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] installation.

-   [Supported Configurations for Service Manager](Supported-Configurations-for-Service-Manager.md)

    Describes the hardware and software requirements for [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)]. Specific considerations about the software that you need to install to support [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] are included.

-   [Operations Manager Considerations in Service Manager](Operations-Manager-Considerations-in-Service-Manager.md)

    Describes information that you need to know if you are planning to deploy [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] in an environment that hosts Operations Manager 2007.

-   [Databases Created by Service Manager](Databases-Created-by-Service-Manager.md)

    Describes the four databases that will be created as a result of deploying [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)].

-   [Port Assignments for Service Manager](Port-Assignments-for-Service-Manager.md)

    Describes the TCP\/IP ports that [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] uses.

-   [Accounts Required During Setup](Accounts-Required-During-Setup.md)

    Describes the accounts thta you will need in order to setup [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)]


