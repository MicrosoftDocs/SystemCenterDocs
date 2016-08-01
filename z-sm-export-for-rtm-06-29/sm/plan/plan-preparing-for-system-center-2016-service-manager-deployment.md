---
title: Preparing for System Center 2016 - Service Manager Deployment
ms.custom: na
ms.prod: system-center-2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5b2cb5d-96d6-4b49-a2ce-251372baf9a5
---

# Preparing for System Center 2016 - Service Manager Deployment

Before you start the deployment of System Center 2012 - Service Manager, you create a group of users in Active Directory Domain Services \(AD DS\), and you create or identify a domain account that will be used during the Setup process. Make sure that the domain account is a member of the appropriate groups that are necessary for proper operation of Service Manager For more information see [Account Considerations for Running Setup](plan-account-considerations-for-running-setup.md) in this guide. Keep the following in mind when you are installing Service Manager and Operations Manager on the same server:  

- Operations Manager can share the database server with Service Manager.  

- An Operations Manager agent is automatically installed as part of Service Manager. After Setup completes, you must manually configure the agent for use with the Operations Manager management server.

     To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present.

-   You can install both the Operations Manager console and the Service Manager console on the same computer. The order in which you install the consoles does not matter.  

-   Do not attempt to use the same SQL Server Reporting Services \(SSRS\) instance for both Operations Manager and Service Manager.  

## Preparing for Deployment Topics  

-   [Account Considerations for Running Setup](plan-account-considerations-for-running-setup.md)  

     Provides information about the accounts that are required to run Setup and that you must provide during the setup of Service Manager.  

-   [How to Prepare Computers for Service Manager Deployment](plan-how-to-prepare-computers-for-service-manager-deployment.md)  

     Describes the steps to take to prepare a computer before running Setup for Service Manager.  
