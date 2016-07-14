---
title: Preparing for System Center 2012 - Service Manager Deployment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5b2cb5d-96d6-4b49-a2ce-251372baf9a5
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
# Preparing for System Center 2012 - Service Manager Deployment
Before you start the deployment of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you create a group of users in Active Directory Domain Services \(AD DS\), and you create or identify a domain account that will be used during the Setup process. Make sure that the domain account is a member of the appropriate groups that are necessary for proper operation of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] For more information see [Account Considerations for Running Setup](../../../sm/plan/planning/Account-Considerations-for-Running-Setup.md) in this guide. Keep the following in mind when you are installing [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and Operations Manager on the same server:  
  
-   Operations Manager 2007 or [!INCLUDE[om12add_remove_prog](../../../sm/plan/planning/includes/om12add_remove_prog_md.md)] can share the database server with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
-   For System Center 2012 Only: An Operations Manager 2007 R2 agent and the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server can coexist on the same server if you install the agent first and then install either the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse management server.  
  
-   [!INCLUDE[sc2012sp1note](../../../sm/plan/planning/includes/sc2012sp1note_md.md)] You must remove an Operations Manager 2007 R2 agent before you run Service Manager Setup. A [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1 agent is automatically installed as part of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1.  After Setup completes, you must manually configure the agent for use with the [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)] management server. The agent is compatible with [!INCLUDE[om2007r2long](../../../sm/deploy/upgrade/includes/om2007r2long_md.md)], [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)], and [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1.  
  
     To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
-   You can install both the Operations Manager 2007 R2 console and the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] on the same computer. The order in which you install the consoles does not matter.  
  
-   Do not attempt to use the same SQL Server Reporting Services \(SSRS\) instance for both Operations Manager and Service Manager.  
  
## Preparing for Deployment Topics  
  
-   [Account Considerations for Running Setup](../../../sm/plan/planning/Account-Considerations-for-Running-Setup.md)  
  
     Provides information about the accounts that are required to run Setup and that you must provide during the setup of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
-   [How to Prepare Computers for Service Manager Deployment](../../../sm/plan/planning/How-to-Prepare-Computers-for-Service-Manager-Deployment.md)  
  
     Describes the steps to take to prepare a computer before running Setup for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)  
  
-   [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670)  
  
-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)