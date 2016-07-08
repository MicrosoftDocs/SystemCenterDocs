---
title: Deploying Additional Service Manager Management Servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80e03b05-c500-4b96-8ca0-4193e9cc07b1
 

















---
# Deploying Additional Service Manager Management Servers
You can deploy additional Service Manager management servers to load\-balance additional Service Manager consoles or as part of your disaster recovery strategy.  
  
 This section describes how you can install additional Service Manager management servers. The additional Service Manager management servers can improve performance in a high\-use environment.  
  
## Management Servers  
 You create a management server when you click **Service Manager management server** in the Service Manager Setup Wizard. The initial Service Manager management server hosts data access, workflow services, and authorization services.  
  
### Initial and Additional Management Servers  
 When you run Setup for the first time, you install the initial Service Manager management server and define the management group for your installation. The initial management server handles all of the workflows in your Service Manager environment. Any additional Service Manager management servers that you deploy are used to load\-balance additional Service Manager console connections. With this release of Service Manager, we recommend that you deploy an additional Service Manager management server for every 40 to 50 Service Manager consoles that you intend to deploy.  
  
 To associate your additional Service Manager management servers with the initial Service Manager management server and management group, you must specify the Service Manager database that you used for your initial Service Manager management server.  
  
## Disjoint Namespace Considerations  
 If you are installing an additional management server in an environment with a disjointed namespace, see [Deployment Considerations with a Disjointed Namespace](../../../sm/deploy/deploy-guide/Deployment-Considerations-with-a-Disjointed-Namespace.md).  
  
## Installing additional management server topics  
  
-   [How to Install an Additional Management Server](../../../sm/deploy/deploy-guide/How-to-Install-an-Additional-Management-Server.md)  
  
     Describes how to install an additional Service Manager management server.
