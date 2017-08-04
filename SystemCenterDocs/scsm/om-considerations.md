---
title: Considerations for Operations Manager with Service Manager
description: This article contains information to be aware of when you are combining Operations Manager and Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 08/03/2017
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee5b265f-1ffa-416d-a038-db9d06efc942
---

# Considerations for Operations Manager with System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This topic contains information to be aware of when you are combining Operations Manager and Service Manager.  

## Service Manager console

Installing the Service Manager console on a Operations Manager management server is not supported. If you install the Service Manager console on an Operations Manager management server, then the System Center Operations Manager SDK service stops.

## Management group names

When you deploy both a Service Manager and data warehouse management server, you are asked to provide a management group name. You are also asked to provide a management group name when you deploy Operations Manager. The management group names that you use for the Service Manager management group, the data warehouse management group, and the Operations Manager management group must be unique.  

> [!IMPORTANT]  
>  If Operations Manager and Service Manager share the same management group name, you will have to reinstall the Service Manager management server. Because it is not possible to rename a management group, you will either have to completely reinstall Service Manager with a different management group name or choose not to manage your Service Manager installation with Operations Manager.  

## Database collations

You must use the same supported language collations if you intend to import data from Operations Manager into Service Manager. However, this is true only for the OperationsManager database in Operations Manager and the SM DWStagingAndConfig database when you create an Operations Manager Data Source for the data warehouse. Specifically, this appears in the Service Manager console as a Data Warehouse Data Source. This does not affect either the System Center Operations Manager to System Center Service Manager Configuration Item connector or the System Center Operations Manager to System Center Service Manager Alert Incident connector.  

> [!NOTE]  
>  If you have databases with collations that do not match, then you cannot use the Operations Manager to Service Manager data warehouse connector which imports alerts from the OperationsManager database  in Operations Manager to the Service Manager DWStagingAndConfig database.  

## Service Manager compatibility

You can use any supported database collation of any System Center component with any supported collation of Service Manager.  

## Operations Manager compatibility  

This section describes the compatibility between Operations Manager and Service Manager.  

### System Center - Operations Manager 2016

 System Center Operations Manager 2016 is supported by Service Manager and Service Manager for connectors and agents. However, other System Center Operations Manager versions are not supported for data source registration. Only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  

System Center 2016 - Service Manager includes a System Center 2016 - Operations Manager agent and it is automatically installed when you deploy Service Manager. After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  

To validate that the Operations Manager Agent was installed, open **Control Panel** and verify that the Operations Manager Agent is present.

### Operations Manager agents

If you want to monitor a server that will host Self\-Service Portal components or the Service Manager console that does not already host other Service Manager roles, then you should deploy the Operations Manager agent to the server before you install the Self\-Service portal or the Service Manager console. After you've installed either, you should give special consideration to removing the portal or Self Service console. If an Operations Manager agent is installed on the server that hosts the portal or console and you remove the either, then the Operations Manager agent is also removed.  

If you have already installed the portal or console to a server that does not host other Service Manager roles, and you want to deploy an Operations Manager agent to it, then the agent deployment will fail. However, you can prevent agent deployment failure by using the following procedure to back up, remove, and restore the Service Manager product registry key.  

##### To back up, remove, and restore the Service Manager product registry key  

1.  Export the Service Manager key from HKEY\_CLASSES\_ROOT\\Installer\\Products\\\<ServiceManagerGUID\>. You can find the key by searching at the Products node for Data equal to Service Manager.  
2.  Delete the registry key.  
3.  Deploy the Operations Manager agent to the server.  
4.  Import the key you exported from step 1.

## Next steps

- Review [Languages supported by Service Manager](sm-languages.md) to learn about the languages that are supported by the Service Manager console and the SQL Server database collations used with Windows locales.
