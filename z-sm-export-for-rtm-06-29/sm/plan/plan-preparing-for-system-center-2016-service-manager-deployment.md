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
 

















---
# Preparing for System Center 2012 - Service Manager Deployment
Before you start the deployment of System Center 2012 - Service Manager, you create a group of users in Active Directory Domain Services \(AD DS\), and you create or identify a domain account that will be used during the Setup process. Make sure that the domain account is a member of the appropriate groups that are necessary for proper operation of Service Manager For more information see [Account Considerations for Running Setup](../../../sm/plan/planning/Account-Considerations-for-Running-Setup.md) in this guide. Keep the following in mind when you are installing Service Manager and Operations Manager on the same server:  
  
-   Operations Manager 2007 or SystemÂ CenterÂ 2012Â -Â OperationsÂ Manager can share the database server with Service Manager.  
  
-   For System Center 2012 Only: An Operations Manager 2007 R2 agent and the Service Manager management server can coexist on the same server if you install the agent first and then install either the Service Manager or data warehouse management server.  
  
-   For System Center 2012 SP1 only: You must remove an Operations Manager 2007 R2 agent before you run Service Manager Setup. A System CenterÂ 2012 - Operations Manager SP1 agent is automatically installed as part of Service Manager SP1.  After Setup completes, you must manually configure the agent for use with the Operations Manager management server. The agent is compatible with System Center Operations Manager 2007 R2, System CenterÂ 2012 - Operations Manager, and System CenterÂ 2012 - Operations Manager SP1.  
  
     To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
-   You can install both the Operations Manager 2007 R2 console and the Service Manager console on the same computer. The order in which you install the consoles does not matter.  
  
-   Do not attempt to use the same SQL Server Reporting Services \(SSRS\) instance for both Operations Manager and Service Manager.  
  
## Preparing for Deployment Topics  
  
-   [Account Considerations for Running Setup](../../../sm/plan/planning/Account-Considerations-for-Running-Setup.md)  
  
     Provides information about the accounts that are required to run Setup and that you must provide during the setup of Service Manager.  
  
-   [How to Prepare Computers for Service Manager Deployment](../../../sm/plan/planning/How-to-Prepare-Computers-for-Service-Manager-Deployment.md)  
  
     Describes the steps to take to prepare a computer before running Setup for Service Manager.  
  
## Other Resources for This Component  
  
-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)  
  
-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)  
  
-   [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670)  
  
-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)  
  
-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)
