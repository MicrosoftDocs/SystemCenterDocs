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
For System Center 2016 Technical Preview \- Service Manager, several deployment options are available, and three options are presented in this guide.

The first deployment option uses one physical computer and one virtual computer. The physical computer hosts the System Center 2016 Technical Preview \- Service Manager management server, the System Center 2016 Technical Preview \- Service Manager database, and the data warehouse databases, and it also hosts the virtual server. The virtual computer hosts the data warehouse management server. This deployment is used primarily for lightweight or first\-impression evaluation of System Center 2016 Technical Preview \- Service Manager. No scalability or performance estimates are available for this scenario.

A second deployment option requires the use of two computers. The first computer hosts the System Center 2016 Technical Preview \- Service Manager management server and the System Center 2016 Technical Preview \- Service Manager database. The second computer hosts the data warehouse management server and the data warehouse databases. If you do not need reporting services, you can—at an absolute minimum—install  System Center 2016 Technical Preview \- Service Manager on one computer that hosts both the Service Manager management server and the Service Manager database.

A third deployment option maximizes performance and scalability by using four computers. Two computers host the management servers, and the remaining two computers host the databases. The computers hosting the databases are the only two computers in this scenario that require the installation of Microsoft SQL Server 2008.

You might decide that, for the evaluation phase, you will choose the option to install System Center 2016 Technical Preview \- Service Manager on two computers. After installing System Center 2016 Technical Preview \- Service Manager in the lab, you can import data from Active Directory Domain Services \(AD DS\) and System Center Configuration Manager, and then you can import data and alerts from Operations Manager. You would then configure User Roles within System Center 2016 Technical Preview \- Service Manager and, if necessary, manually add users that were not imported from AD DS. The following illustration represents an overview of this installation and initial configuration.

![](../../media/SM_Installation_Topology.png)

You can limit the number of SQL Server licenses that you need by placing all of the System Center 2016 Technical Preview \- Service Manager databases on the same computer, as shown in the following illustration.

![](../../media/SM_Installation_Topology_Single_SQL.jpg)

You continue the deployment process by creating several templates; configuring initial parameters; creating queues, lists, and groups; and then creating a management pack to save these custom objects.

After the evaluation phase is complete, you might install System Center 2016 Technical Preview \- Service Manager in a production environment and select the deployment scenario in which System Center 2016 Technical Preview \- Service Manager is installed on four computers.

## Multiple Service Manager Management Servers and One Data Warehouse
The System Center 2016 Technical Preview \- Service Manager management server and its associated System Center 2016 Technical Preview \- Service Manager database make up a System Center 2016 Technical Preview \- Service Manager management group. The data warehouse management server and its associated databases make up a data warehouse management group. After deploying System Center 2016 Technical Preview \- Service Manager, you will register the System Center 2016 Technical Preview \- Service Manager management group with the data warehouse management group.

In your enterprise, you might create multiple System Center 2016 Technical Preview \- Service Manager management groups. You can centralize reporting for multiple System Center 2016 Technical Preview \- Service Manager management groups by registering multiple System Center 2016 Technical Preview \- Service Manager management groups with a single data warehouse management group. For more information, see [How to Run the Data Warehouse Registration Wizard](http://go.microsoft.com/fwlink/p/?LinkID=232303).

## Planning for Deployment Topics

-   [Service Manager Parts](Service-Manager-Parts.md)

    Describes the six major parts of a System Center 2016 Technical Preview \- Service Manager installation.

-   [Supported Configurations for Service Manager](Supported-Configurations-for-Service-Manager.md)

    Describes the hardware and software requirements for System Center 2016 Technical Preview \- Service Manager. Specific considerations about the software that you need to install to support System Center 2016 Technical Preview \- Service Manager are included.

-   [Operations Manager Considerations in Service Manager](Operations-Manager-Considerations-in-Service-Manager.md)

    Describes information that you need to know if you are planning to deploy System Center 2016 Technical Preview \- Service Manager in an environment that hosts Operations Manager 2007.

-   [Databases Created by Service Manager](Databases-Created-by-Service-Manager.md)

    Describes the four databases that will be created as a result of deploying System Center 2016 Technical Preview \- Service Manager.

-   [Port Assignments for Service Manager](Port-Assignments-for-Service-Manager.md)

    Describes the TCP\/IP ports that System Center 2016 Technical Preview \- Service Manager uses.

-   [Accounts Required During Setup](Accounts-Required-During-Setup.md)

    Describes the accounts thta you will need in order to setup System Center 2016 Technical Preview \- Service Manager


