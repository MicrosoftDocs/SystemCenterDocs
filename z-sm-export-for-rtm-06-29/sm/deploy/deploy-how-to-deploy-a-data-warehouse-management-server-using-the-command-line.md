---
title: How to Deploy a Data Warehouse Management Server Using the Command Line
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 83a92df6-f2ad-450b-855b-9319c7059a9f


















---
# How to Deploy a Data Warehouse Management Server Using the Command Line
Use the following procedures to deploy a Service Manager data warehouse and databases, including the Operations Manager and Configuration Manager data mart databases, in System Center 2012 - Service Manager.  
  
## Deploying the Data Warehouse  
 Use the following procedures to deploy the data warehouse with the Operations Manager and Configuration Manager data mart databases. If you want to install the data warehouse management server and data warehouse databases on the same computer, use the same computer name that you are running Setup on for all instances of **\[computer name\]**. If you want to deploy the databases on a separate computer, adjust the **\[computer name\]** entries accordingly.  
  
 The **\/AnalysisServerDatabaseDataFilePath** is optional, and if it is not used, the default path will be used.  
  
 The DWStagingAndConfig database and the DWRepository database must reside on the same instance. Make sure that you specify the same computer and instance for the **\/StgConfigSqlServerInstance** and **\/RepositorySqlServerInstance** command\-line options.  
  
#### To deploy the data warehouse management server, data warehouse databases, and optional data marts  
  
1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  
  
2.  Open a command window.  
  
    > [!NOTE]  
    >  You must run the command prompt with administrative credentials.  
  
3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe   
    /Install:Datawarehouse   
    /AcceptEula:[YES/NO]   
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /CreateNewDatabase   
    /AdminRoleGroup:[domain\account name]   
    /StgConfigSqlServerInstance:[computer name]   
    /RepositorySqlServerInstance:[computer name]   
    /DataMartSqlServerInstance:[computer name]   
    /ReportingServer:[computer name]   
    /ReportingWebServiceURL:"http://[computer name]:80/ReportServer"   
    /ServiceRunUnderAccount:[domain\account name\password]   
    /DatasourceAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]   
    /ManagementGroupName:DW_improvement   
    /OMDataMartSqlServerInstance:[computer name]   
    /CMDataMartSqlServerInstance:[computer name]   
    /AnalysisServerInstance:[computer name]   
    /AnalysisServerDatabaseDataFilePath:[path to analysis database]   
    /ASRunUnderAccount:[domain\account name\password]   
    /Silent  
    ```  
  
## See Also  
 [Deploying Service Manager from a Command Line](assetId:///a918e488-349d-4955-b401-52f09e78bb9e)
