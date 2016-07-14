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
translation.priority.mt: 
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
# Configure Windows PowerShell to Run in System Center 2012 - Service Manager
Before you can run commands in the Windows PowerShell command\-line interface in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you must set execution policy to RemoteSigned and import the data warehouse cmdlet module.  
  
 The [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] cmdlets are implemented in the following two modules:  
  
-   **System.Center.Service.Manager**. This module is imported automatically every time a [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] Windows PowerShell session is opened.  
  
-   **Microsoft.EnterpriseManagement.Warehouse.Cmdlets**. This module must be imported manually.  
  
## Cmdlets in Authoring Tool Workflows  
 When you use the Service Manager SP1 version of the Authoring tool to create a workflow, then custom scripts using Windows PowerShell cmdlets called by the workflow fail. This is due to a problem in the Service Manager MonitoringHost.exe.config file.  
  
 To work around this problem, update the MonitoringHost.exe.config XML file using the following steps.  
  
1.  Navigate to %ProgramFiles%\\Microsoft System Center 2012\\Service Manager\\ or the location where you installed Service Manager.  
  
2.  Edit the MonitoringHost.exe.config file and add the section in italic type from the example below in the corresponding section of your file. You must insert the section before \<publisherPolicy apply\="yes" \/\>.  
  
3.  Save your changes to the file.  
  
4.  Restart the System Center Management service on the Service Manager management server.  
  
```  
<?xml version="1.0"?><configuration>  <configSections>    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  </configSections>  <uri>    <iriParsing enabled="true" />  </uri>    <runtime>    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">      <dependentAssembly>        <assemblyIdentity name="Microsoft.Mom.Modules.DataTypes" publicKeyToken="31bf3856ad364e35" />        <publisherPolicy apply="no" />        <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />      </dependentAssembly>      <dependentAssembly>        <assemblyIdentity name="Microsoft.EnterpriseManagement.HealthService.Modules.WorkflowFoundation" publicKeyToken="31bf3856ad364e35" />        <publisherPolicy apply="no" />        <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />      </dependentAssembly>    
<dependentAssembly>  
  
<assemblyIdentity name="Microsoft.EnterpriseManagement.Modules.PowerShell" publicKeyToken="31bf3856ad364e35" />  
  
<bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
  
</dependentAssembly>  
       <publisherPolicy apply="yes" />      <probing privatePath="" />    </assemblyBinding>    <gcConcurrent enabled="true" />  </runtime></configuration>  
```  
  
## In This Section  
 [How to Set Execution Policy](../Topic/How%20to%20Set%20Execution%20Policy.md)  
 Describes how to set execution policy to RemoteSigned.  
  
 [How to Import the Data Warehouse Cmdlet Module](../Topic/How%20to%20Import%20the%20Data%20Warehouse%20Cmdlet%20Module.md)  
 Describes how to manually import the data warehouse Windows PowerShell cmdlets.