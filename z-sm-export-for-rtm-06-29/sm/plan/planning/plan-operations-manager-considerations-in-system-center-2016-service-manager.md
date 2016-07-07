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
# Operations Manager Considerations in System Center 2012 - Service Manager
This topic contains information to be aware of when you are combining Operations Manager and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Management Group Names Must be Unique  
 When you deploy both a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and data warehouse management server, you are asked to provide a management group name. You are also asked to provide a management group name when you deploy Operations Manager. The management group names that you use for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management group, the data warehouse management group, and the Operations Manager management group must be unique.  
  
> [!IMPORTANT]  
>  If Operations Manager and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] share the same management group name, you will have to reinstall the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. Because it is not possible to rename a management group, you will either have to completely reinstall [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] with a different management group name or choose not to manage your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation with Operations Manager.  
  
## Database Collations  
 You must use the same supported language collations if you intend to import data from [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)] into [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)]. However, this is true only for the OperationsManager database in Operations Manager and the SM DWStagingAndConfig database when you create an Operations Manager Data Source for the data warehouse. Specifically, this appears in the Service Manager console as a Data Warehouse Data Source. This does not affect either the System Center Operations Manager to System Center Service Manager Configuration Item connector or the System Center Operations Manager to System Center Service Manager Alert Incident connector.  
  
 [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] the SQL Server collation setting that might impact installation requirements in System Center 2012 Service Pack 1 \(SP1\) when you use Operations Manager and Service Manager, see [Clarification on SQL Server Collation Requirements for System Center 2012](http://blogs.technet.com/b/servicemanager/archive/2012/05/24/clarification-on-sql-server-collation-requirements-for-system-center-2012.aspx).  
  
> [!NOTE]  
>  If you have databases with collations that do not match, then you cannot use the Operations Manager to Service Manager data warehouse connector which imports alerts from the OperationsManager database  in Operations Manager to the Service Manager DWStagingAndConfig database.  
  
## Service Manager Compatibility With Other System Center Components  
 You can use any supported database collation of any System Center component with any supported collation of Service Manager.  
  
## Operations Manager Compatibility  
 This section describes the compatibility between [!INCLUDE[om2007r2short](../../../sm/deploy/upgrade/includes/om2007r2short_md.md)], [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] and [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1.  
  
### [!INCLUDE[om2007r2long](../../../sm/deploy/upgrade/includes/om2007r2long_md.md)]  
 [!INCLUDE[om2007r2long](../../../sm/deploy/upgrade/includes/om2007r2long_md.md)] is supported by [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] and [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] SP1 for connectors and agents. However, [!INCLUDE[om2007r2long](../../../sm/deploy/upgrade/includes/om2007r2long_md.md)] is not supported for data source registration. Only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  
  
 Because upgrading to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 is not supported, you must remove [!INCLUDE[om2007r2short](../../../sm/deploy/upgrade/includes/om2007r2short_md.md)] agents from the Service Manager and data warehouse management servers before you install. [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 includes a [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1 agent and it is automatically installed when you deploy [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. After [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
### [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)]  
 [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] is supported by [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] and [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] SP1 for connectors and agents. However, only corresponding System Center versions are supported when you register a data source in the Data Warehouse workspace.  
  
 [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] agents were not supported with [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. However, the agent that is automatically installed by [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 is compatible with [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] and [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1.  After [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open **Control Panel** and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
### Operations Manager Agents with the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] and [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]  
 If you want to monitor a server that will host Self\-Service Portal components or the Service Manager console that does not already host other Service Manager roles, then you should deploy the Operations Manager agent to the server before you install the Self\-Service portal or the Service Manager console. After you’ve installed either, you should give special consideration to removing the portal or Self Service console. If an Operations Manager agent is installed on the server that hosts the portal or console and you remove the either, then the Operations Manager agent is also removed.  
  
 If you have already installed the portal or console to a server that does not host other Service Manager roles, and you want to deploy an Operations Manager agent to it, then the agent deployment will fail. However, you can prevent agent deployment failure by using the following procedure to back up, remove, and restore the Service Manager product registry key.  
  
##### To back up, remove, and restore the Service Manager product registry key  
  
1.  Export the Service Manager key from HKEY\_CLASSES\_ROOT\\Installer\\Products\\\<ServiceManagerGUID\>. You can find the key by searching at the Products node for Data equal to Service Manager.  
  
2.  Delete the registry key.  
  
3.  Deploy the Operations Manager agent to the server.  
  
4.  Import the key you exported from step 2.