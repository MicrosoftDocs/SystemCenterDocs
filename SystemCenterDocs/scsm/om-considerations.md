---
title: Operations Manager deployment considers in System Center - Service Manager
description: This article contains information to be aware of when you are combining Operations Manager and Service Manager.
manager: carmonm
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
---

# Operations Manager deployment consideration in Service Manager

This article summarizes considerations for deploying System Center - Operations Manager with System Center- Service Manager.

## Service Manager console

Installing the Service Manager console on a Operations Manager management server isn't supported. If you do, then the System Center Operations Manager SDK service stops.

## Management group names

When you deploy both a Service Manager and data warehouse management server, you are asked to provide a management group name. You are also asked to provide a management group name when you deploy Operations Manager.

- The names that you use for each of these must be unique.
- If Operations Manager and Service Manager share the same management group name, you will have to reinstall the Service Manager management server, because a management group can't be renamed. Alternatively, if you do this, you can choose not to manage your Service Manager installation with Operations Manager.  

## Database collations

- You must use the same supported language collations if you intend to import data from Operations Manager into Service Manager. 
- This is true only for the OperationsManager database in Operations Manager and the SM DWStagingAndConfig database, when you create an Operations Manager Data Source for the data warehouse.
- Specifically, this appears in the Service Manager console as a Data Warehouse Data Source.
- This does not affect either the Operations Manager to Service Manager Configuration Item connector, or the Operations Manager to  Service Manager Alert Incident connector.  
- If you have databases with collations that don't match, then you can't use the Operations Manager to Service Manager data warehouse connector which imports alerts from the OperationsManager database  in Operations Manager to the Service Manager DWStagingAndConfig database. 


## Service Manager compatibility

You can use any supported database collation of any System Center component, with any supported collation of Service Manager.  

## Operations Manager compatibility  

This section describes the compatibility between Operations Manager and Service Manager.  

### Operations Manager

Operations Manager is supported by Service Manager and Service Manager for connectors and agents. However, other Operations Manager versions aren't supported for data source registration. Only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  

### Operations Manager agents

Service Manager includes an Operations Manager agent, and it is automatically installed when you deploy Service Manager. After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  

- To validate that the Operations Manager Agent was installed, open **Control Panel** and verify that the agent is present.
- If you want to monitor a server that will host Self\-Service Portal components or the Service Manager console that does not already host other Service Manager roles, then deploy the Operations Manager agent on the server, before you install the Self\-Service portal or the Service Manager console.
- If you remove the console or Self-Service Portal on a machine that's running the Operations Manager agent, the agent is also removed.
- If you have already installed the portal or console on a server that doesn't host other Service Manager roles, and you want to deploy the agent, then the agent deployment will fail. To prevent the failure, back up the registry key as follows:

 1. Export the Service Manager key from HKEY\_CLASSES\_ROOT\\Installer\\Products\\\<ServiceManagerGUID\>. You can find the key by searching at the Products node for Data equal to Service Manager.  
 2.  Delete the registry key.  
 3.  Deploy the Operations Manager agent to the server.  
 4.  Import the key you exported from step 1.

## Next steps

[Review](sm-languages.md) languages supported by Service Manager.
