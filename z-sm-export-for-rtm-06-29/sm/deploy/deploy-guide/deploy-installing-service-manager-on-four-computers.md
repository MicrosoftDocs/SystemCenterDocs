---
title: Installing Service Manager on Four Computers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 474fd861-01b0-44a6-b917-cf320a5d725b
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
# Installing Service Manager on Four Computers
When you are ready to move [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] into a production environment, or if you want to maximize performance and scalability, you can consider an installation topology in which each part of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation resides on its own computer. This topology requires the use of four computers, as shown in figure 3.  
  
 **Figure 3: Four\-computer topology**  
  
 ![Four&#45;computer installation of Service Manager 2012](../../../sm/deploy/deploy-guide/media/Four_Computer_Install_SCSM2012.gif "Four\_Computer\_Install\_SCSM2012")  
  
 In this deployment scenario, you install Microsoft SQL Server only on the computers that hosts databases \(computers 2 and 4\). You install SQL Server Reporting Services \(SSRS\) and SQL Server Analysis Services \(SSAS\) on the computer that hosts the data warehouse databases \(computer 4\).  
  
## Installing Service Manager on four computers  
  
-   [How to Install the Service Manager Management Server \(Four\-Computer Scenario\)](../../../sm/deploy/deploy-guide/How-to-Install-the-Service-Manager-Management-Server--Four-Computer-Scenario-.md)  
  
     Describes how to install the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database.  
  
-   [How to Install the Service Manager Data Warehouse \(Four\-Computer Scenario\)](../../../sm/deploy/deploy-guide/How-to-Install-the-Service-Manager-Data-Warehouse--Four-Computer-Scenario-.md)  
  
     Describes how to install the data warehouse management server and data warehouse databases.  
  
-   [How to Validate the Four\-Computer Installation](../../../sm/deploy/deploy-guide/How-to-Validate-the-Four-Computer-Installation.md)  
  
     Describes how to validate the installation of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and the configuration of SSRS.  
  
> [!IMPORTANT]  
>  For this release, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] does not support case\-sensitive instance names. Setup will display a warning if you attempt to install [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] on a case\-sensitive instance of Microsoft SQL Server.