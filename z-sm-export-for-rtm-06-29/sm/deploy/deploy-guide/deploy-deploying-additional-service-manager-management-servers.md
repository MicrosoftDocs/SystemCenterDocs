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
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Deploying Additional Service Manager Management Servers
You can deploy additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers to load\-balance additional [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]s or as part of your disaster recovery strategy.  
  
 This section describes how you can install additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers. The additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers can improve performance in a high\-use environment.  
  
## Management Servers  
 You create a management server when you click **Service Manager management server** in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Setup Wizard. The initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server hosts data access, workflow services, and authorization services.  
  
### Initial and Additional Management Servers  
 When you run Setup for the first time, you install the initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and define the management group for your installation. The initial management server handles all of the workflows in your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] environment. Any additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers that you deploy are used to load\-balance additional [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] connections. With this release of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], we recommend that you deploy an additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server for every 40 to 50 [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]s that you intend to deploy.  
  
 To associate your additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers with the initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and management group, you must specify the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database that you used for your initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
## Disjoint Namespace Considerations  
 If you are installing an additional management server in an environment with a disjointed namespace, see [Deployment Considerations with a Disjointed Namespace](../../../sm/deploy/deploy-guide/Deployment-Considerations-with-a-Disjointed-Namespace.md).  
  
## Installing additional management server topics  
  
-   [How to Install an Additional Management Server](../../../sm/deploy/deploy-guide/How-to-Install-an-Additional-Management-Server.md)  
  
     Describes how to install an additional Service Manager management server.