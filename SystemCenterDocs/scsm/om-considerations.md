---
title: Operations Manager deployment consideration in System Center - Service Manager
description: This article contains information to be aware of when you're combining Operations Manager and Service Manager.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: concept-article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Operations Manager deployment consideration in Service Manager



This article summarizes considerations for deploying System Center - Operations Manager together with System Center - Service Manager.

## Service Manager console

Installing the Service Manager console on an Operations Manager management server isn't supported. If you do install it, the Operations Manager SDK service stops.

## Management group names

When you deploy a Service Manager management server and a data warehouse, you need to provide a management group name. You also need to provide a management group name when you deploy Operations Manager.

- Each name must be unique.
- Renaming a management group isn't supported. If you do assign the same management group name to Operations Manager and Service Manager, you've to reinstall the Service Manager management server, or choose not to manage your Service Manager installation with Operations Manager.  

## Database collations

- You must use the same supported language collations if you want to import data from Operations Manager into Service Manager.
- This only applies to the Operations Manager database, and the SM DWStagingAndConfig database, when you create an Operations Manager Data Source for the data warehouse. Specifically, this appears in the Service Manager console as a Data Warehouse Data Source.
- This doesn't affect either the Operations Manager to Service Manager Configuration Item connector, or the Operations Manager to  Service Manager Alert Incident connector.  
- If you've databases with collations that don't match, you can't use the Operations Manager to Service Manager data warehouse connector. This connector imports alerts from the Operations Manager database, to the Service Manager DWStagingAndConfig database.

## Service Manager compatibility

You can use any supported database collation for any System Center component with any supported Service Manager collation.  

## Operations Manager compatibility  

This section describes the compatibility of Operations Manager and Service Manager.  

### Operations Manager

Operations Manager is supported by Service Manager, and Service Manager for connectors and agents. Other Operations Manager versions aren't supported for data source registration. When you register a data source in the Data Warehouse workspace, only corresponding System Center versions are supported.

### Operations Manager agents

Service Manager includes an Operations Manager agent. The agent is automatically installed when you deploy Service Manager. After installation, you must manually configure the agent to communicate with the Operations Manager management server.  

- To validate that the agent is installed, open **Control Panel**, and verify that the agent is present.
- To monitor a server running the Self-Service Portal, or the Service Manager console, deploy the Operations Manager agent on the server before you install the portal or console.
- If you remove the console or Self-Service Portal on a machine that's running the Operations Manager agent, the agent is also removed.
- If you've already installed the portal or console on a server that doesn't host other Service Manager roles, then agent deployment will fail. To prevent the failure, back up the registry key as follows:

  1. Export the Service Manager key from HKEY\_CLASSES\_ROOT\\Installer\\Products\\\<ServiceManagerGUID\>. You can find the key by searching at the Products node for Data equal to Service Manager.  
  2. Delete the registry key.  
  3. Deploy the Operations Manager agent to the server.  
  4. Import the key you exported from step 1.

## Next steps

[Review](sm-languages.md) languages supported by Service Manager.
