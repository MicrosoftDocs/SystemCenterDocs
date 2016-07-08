---
title: Operations Manager Considerations in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee5b265f-1ffa-416d-a038-db9d06efc942
 

















---
# Operations Manager Considerations in System Center 2012 - Service Manager
This topic contains information to be aware of when you are combining Operations Manager and Service Manager.  
  
## Management Group Names Must be Unique  
 When you deploy both a Service Manager and data warehouse management server, you are asked to provide a management group name. You are also asked to provide a management group name when you deploy Operations Manager. The management group names that you use for the Service Manager management group, the data warehouse management group, and the Operations Manager management group must be unique.  
  
> [!IMPORTANT]  
>  If Operations Manager and Service Manager share the same management group name, you will have to reinstall the Service Manager management server. Because it is not possible to rename a management group, you will either have to completely reinstall Service Manager with a different management group name or choose not to manage your Service Manager installation with Operations Manager.  
  
## Database Collations  
 You must use the same supported language collations if you intend to import data from Operations Manager into Service Manager. However, this is true only for the OperationsManager database in Operations Manager and the SM DWStagingAndConfig database when you create an Operations Manager Data Source for the data warehouse. Specifically, this appears in the Service Manager console as a Data Warehouse Data Source. This does not affect either the System Center Operations Manager to System Center Service Manager Configuration Item connector or the System Center Operations Manager to System Center Service Manager Alert Incident connector.  
  
 For more information about the SQL Server collation setting that might impact installation requirements in System Center 2012 Service Pack 1 \(SP1\) when you use Operations Manager and Service Manager, see [Clarification on SQL Server Collation Requirements for System Center 2012](http://blogs.technet.com/b/servicemanager/archive/2012/05/24/clarification-on-sql-server-collation-requirements-for-system-center-2012.aspx).  
  
> [!NOTE]  
>  If you have databases with collations that do not match, then you cannot use the Operations Manager to Service Manager data warehouse connector which imports alerts from the OperationsManager database  in Operations Manager to the Service Manager DWStagingAndConfig database.  
  
## Service Manager Compatibility With Other System Center Components  
 You can use any supported database collation of any System Center component with any supported collation of Service Manager.  
  
## Operations Manager Compatibility  
 This section describes the compatibility between Operations Manager 2007 R2, System CenterÂ 2012 - Operations Manager and System Center 2012 - Service Manager SP1.  
  
### System Center Operations Manager 2007 R2  
 System Center Operations Manager 2007 R2 is supported by Service Manager and Service Manager SP1 for connectors and agents. However, System Center Operations Manager 2007 R2 is not supported for data source registration. Only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  
  
 Because upgrading to System Center 2012 - Service Manager SP1 is not supported, you must remove Operations Manager 2007 R2 agents from the Service Manager and data warehouse management servers before you install. System Center 2012 - Service Manager SP1 includes a System CenterÂ 2012 - Operations Manager SP1 agent and it is automatically installed when you deploy Service Manager. After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
### System CenterÂ 2012 - Operations Manager  
 System CenterÂ 2012 - Operations Manager is supported by Service Manager and Service Manager SP1 for connectors and agents. However, only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  
  
 System CenterÂ 2012 - Operations Manager agents were not supported with System Center 2012 - Service Manager. However, the agent that is automatically installed by System Center 2012 - Service Manager SP1 is compatible with System CenterÂ 2012 - Operations Manager and System CenterÂ 2012 - Operations Manager SP1.  After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open **Control Panel** and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
### Operations Manager Agents with the Self-Service Portal and Service Manager console  
 If you want to monitor a server that will host Self\-Service Portal components or the Service Manager console that does not already host other Service Manager roles, then you should deploy the Operations Manager agent to the server before you install the Self\-Service portal or the Service Manager console. After you’ve installed either, you should give special consideration to removing the portal or Self Service console. If an Operations Manager agent is installed on the server that hosts the portal or console and you remove the either, then the Operations Manager agent is also removed.  
  
 If you have already installed the portal or console to a server that does not host other Service Manager roles, and you want to deploy an Operations Manager agent to it, then the agent deployment will fail. However, you can prevent agent deployment failure by using the following procedure to back up, remove, and restore the Service Manager product registry key.  
  
##### To back up, remove, and restore the Service Manager product registry key  
  
1.  Export the Service Manager key from HKEY\_CLASSES\_ROOT\\Installer\\Products\\\<ServiceManagerGUID\>. You can find the key by searching at the Products node for Data equal to Service Manager.  
  
2.  Delete the registry key.  
  
3.  Deploy the Operations Manager agent to the server.  
  
4.  Import the key you exported from step 2.
