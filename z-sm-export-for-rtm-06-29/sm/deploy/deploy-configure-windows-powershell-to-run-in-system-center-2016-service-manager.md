---
title: Configure Windows PowerShell to Run in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b785d6a-2011-4fd9-987b-46e5eb164896


















---
# Configure Windows PowerShell to Run in System Center 2012 - Service Manager
Before you can run commands in the Windows&nbsp;PowerShell command\-line interface in System Center 2012 - Service Manager, you must set execution policy to RemoteSigned and import the data warehouse cmdlet module.  
  
 The Service Manager cmdlets are implemented in the following two modules:  
  
-   **System.Center.Service.Manager**. This module is imported automatically every time a Service Manager Windows&nbsp;PowerShell session is opened.  
  
-   **Microsoft.EnterpriseManagement.Warehouse.Cmdlets**. This module must be imported manually.  
  
## Cmdlets in Authoring Tool Workflows  
 When you use the Service Manager SP1 version of the Authoring tool to create a workflow, then custom scripts using Windows PowerShell cmdlets called by the workflow fail. This is due to a problem in the Service Manager MonitoringHost.exe.config file.  
  
 To work around this problem, update the MonitoringHost.exe.config XML file using the following steps.  
  
1.  Navigate to %ProgramFiles%\\Microsoft System Center 2012\\Service Manager\\ or the location where you installed Service Manager.  
  
2.  Edit the MonitoringHost.exe.config file and add the section in italic type from the example below in the corresponding section of your file. You must insert the section before \<publisherPolicy apply\="yes" \/\>.  
  
3.  Save your changes to the file.  
  
4.  Restart the System Center Management service on the Service Manager management server.  
  
```  
<?xml version="1.0"?><configuration>&nbsp; <configSections>&nbsp;&nbsp;&nbsp; <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />&nbsp; </configSections>&nbsp; <uri>&nbsp;&nbsp;&nbsp; <iriParsing enabled="true" />&nbsp; </uri>&nbsp; &nbsp;&nbsp;<runtime>&nbsp;&nbsp;&nbsp; <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <dependentAssembly>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <assemblyIdentity name="Microsoft.Mom.Modules.DataTypes" publicKeyToken="31bf3856ad364e35" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="no" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </dependentAssembly>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <dependentAssembly>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <assemblyIdentity name="Microsoft.EnterpriseManagement.HealthService.Modules.WorkflowFoundation" publicKeyToken="31bf3856ad364e35" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="no" />&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </dependentAssembly>&nbsp;&nbsp;  
<dependentAssembly>  
  
<assemblyIdentity name="Microsoft.EnterpriseManagement.Modules.PowerShell" publicKeyToken="31bf3856ad364e35" />  
  
<bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
  
</dependentAssembly>  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="yes" />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <probing privatePath="" />&nbsp;&nbsp;&nbsp; </assemblyBinding>&nbsp;&nbsp;&nbsp; <gcConcurrent enabled="true" />&nbsp; </runtime></configuration>  
```  
  
## In This Section  
 [How to Set Execution Policy](../Topic/How%20to%20Set%20Execution%20Policy.md)  
 Describes how to set execution policy to RemoteSigned.  
  
 [How to Import the Data Warehouse Cmdlet Module](../Topic/How%20to%20Import%20the%20Data%20Warehouse%20Cmdlet%20Module.md)  
 Describes how to manually import the data warehouse Windows&nbsp;PowerShell cmdlets.
