---
title: List of the Service Manager Cmdlets
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98804667-754e-417a-ac2e-6ae4d47e65d2
---
# List of the Service Manager Cmdlets
About Managing the Data Warehouse supports the following Windows PowerShell cmdlets, which are implemented in two modules: the administrator module and the data warehouse module.

## Administrator Cmdlets in the System.Center.Service.Manager Module

|Cmdlet|Description|
|----------|---------------|
|Add-SCSMAllowListClass|Adds the specified classes to the Allow list of classes that is used by the Service Manager Operations Manager CI Connector during synchronization.|
|Export-SCSMManagementPack|Exports a management pack as a valid XML-formatted file that you can later import into Service Manager or Operations Manager.|
|Get-SCSMAllowList|Retrieves the Allow list of classes that is used by the Service Manager Operations Manager CI Connector during synchronization.|
|Get-SCSMAnnouncement|Retrieves announcements that are defined in Service Manager.|
|Get-SCSMChannel|Retrieves the Email Notification channels that are defined in Service Manager.|
|Get-SCSMClass|Retrieves a class.|
|Get-SCSMClassInstance|Retrieves class instance objects.|
|Get-SCSMCommand||
|Get-SCSMConnector|Retrieves connectors that are defined in Service Manager.|
|Get-SCSMDCMWorkflow|Retrieves the list of desired configuration management workflows that are defined in Service Manager.|
|Get-SCSMDeletedItem|Retrieves items that have been marked for deletion in Service Manager.|
|Get-SCSMDiscovery|Retrieves discovery information from Operations Manager and from Service Manager.|
|Get-SCSMEmailTemplate|Retrieves Email templates that are defined in Service Manager.|
|Get-SCSMEmailTemplateContent|Retrieves the content of Service Manager Email templates.|
|Get-SCSMGroup|Retrieves groups from Operations Manager and from Service Manager.|
|Get-SCSMManagementGroupConnection|Retrieves all management group connections, including the IsActive state of these connections. Only one connection will have its IsActive state set to True, because only one connection can be active at any time.|
|Get-SCSMManagementPack|Retrieves objects that represent management packs that have been imported.|
|Get-SCSMObjectTemplate|Retrieves an object template.|
|Get-SCSMPortalCMConfiguration|Retrieves the settings for the Configuration Manager that is used for software deployments on the Service ManagerSelf-Service Portal.|
|Get-SCSMPortalContactConfiguration|Retrieves the IT Contact setting that the  Service Manager Self-Service Portal is configured with.|
|Get-SCSMPortalDeploymentProcess|Retrieves information about software deployment processes for the Service Manager Self-Service Portal.|
|Get-SCSMPortalSoftwarePackage|Retrieves all the software packages that are configured for deployment in the Service Manager Self-Service Portal.|
|Get-SCSMQueue|Retrieves queues that are defined in Service Manager.|
|Get-SCSMRelationship|Retrieves information about relationship objects from Operations Manager and from Service Manager.|
|Get-SCSMRelationshipInstance|Retrieves the instances of relationships from Operations Manager and from Service Manager.|
|Get-SCSMRunAsAccount|Retrieves Run As accounts.|
|Get-SCSMSetting|Retrieves configuration settings of System Center Service Manager.|
|Get-SCSMSubscription|Retrieves subscriptions that are configured in Service Manager.|
|Get-SCSMTask|Retrieves tasks that are defined in Service Manager.|
|Get-SCSMUser|Retrieves users that are defined in Service Manager.|
|Get-SCSMUserRole|Retrieves user roles that are defined in Service Manager.|
|Get-SCSMView|Retrieves views that are defined in Service Manager.|
|Get-SCSMWorkflow|Retrieves configuration information for Service Manager workflows.|
|Get-SCSMWorkflowStatus|Retrieves the status of workflows in Service Manager.|
|Import-SCSMInstance|Imports objects and relationships from a comma-separated value (.csv) file into Service Manager.|
|Import-SCSMManagementPack|Imports management packs.|
|New-SCOrchestratorConnector||
|New-SCRelationshipInstance||
|New-SCSMADConnector|Creates a new Active Directory connector.|
|New-SCSMAlertRule|Creates an alert rule to be used with an Operations Manager alert connector in Service Manager.|
|New-SCSMAnnouncement|Creates a new announcement in Service Manager.|
|New-SCSMClassInstance|Adds a class instance to the database.|
|New-SCSMCMConnector|Creates a new Configuration Manager connector in Service Manager.|
|New-SCSMDCMWorkflow|Creates a new desired configuration management workflow in Service Manager.|
|New-SCSMEmailTemplate|Creates a new Email template for Service Manager.|
|New-SCSMManagementGroupConnection|Creates a new connection for the specified management group. The most recent management group connection that was created is the active connection that  **Get-** cmdlets use by default, in which you did not specify the **ComputerName** and **Credential**, or the **SCSession** parameters.|
|New-SCSMManagementPack|Creates a new management pack.|
|New-SCSMManagementPackBundle|Bundles individual management packs and their resources, creating a new management pack bundle.|
|New-SCSMOMAlertConnector|Creates a new Operations Manager alert connector in Service Manager.|
|New-SCSMOMConfigurationItemConnector|Creates a new Operations Manager CI connector in Service Manager.|
|New-SCSMPortalDeploymentProcess|Creates a software deployment process for deploying software by using the Service Manager Self-Service Portal.|
|New-SCSMRunAsAccount|Creates a new Run As account.|
|New-SCSMSubscription|Creates a new subscription in Service Manager.|
|New-SCSMUserRole|Creates a new user role in Service Manager.|
|New-SCSMWorkflow|Creates a new workflow in Service Manager.|
|New-SCVMMConnector||
|Protect-SCSMManagementPack|Seals a management pack, preventing it from being modified.|
|Remove-SCSMAllowListClass|Removes the specified classes from the Allow list of classes that are used by the Operations Manager CI Connector during synchronization in Service Manager.|
|Remove-SCSMAnnouncement|Removes an announcement from Service Manager.|
|Remove-SCSMClassInstance|Removes an instance of a configuration item object.|
|Remove-SCSMConnector|Removes a connector from Service Manager.|
|Remove-SCSMDCMWorkflow|Removes a desired configuration management workflow from Service Manager.|
|Remove-SCSMEmailTemplate|Removes an Email template from Service Manager.|
|Remove-SCSMManagementGroupConnection|Removes a management group connection.|
|Remove-SCSMManagementPack|Removes management packs.|
|Remove-SCSMPortalDeploymentProcess|Removes a software deployment process from the Service Manager Self-Service Portal.|
|Remove-SCSMRunAsAccount|Removes a Run As accounts.|
|Remove-SCSMSubscription|Removes a subscription from Service Manager.|
|Remove-SCSMUserRole|Removes a user role from Service Manager.|
|Remove-SCSMWorkflow|Removes a workflow from Service Manager.|
|Reset-SCSMAllowList|Resets the Allow list of classes that is used by the Operations Manager CI Connector in Service Manager to the default Allow list.|
|Restore-SCSMDeletedItem|Restores items that were previously deleted in Service Manager.|
|Set-SCSMChannel|Sets the properties of the email notification channel in Service Manager.|
|Set-SCSMManagementGroupConnection|Sets the specified connection as the active connection. The active connection is the connection that is implicitly used when you run a **Get-** cmdlet without specifying **–ComputerName** and **–Credential** or **–SCSession** parameters. Only one connection can be active at any time, and by default the active connection is the last connection that was created by using the **New-SCManagementGroupConnection** cmdlet.|
|Set-SCSMPortalCMConfiguration|Sets the configuration information for the Service Manager Self-Service Portal.|
|Set-SCSMPortalContactConfiguration|Configures the settings of information technology (IT) contacts for the end-user of the Service Manager Self-Service Portal.|
|Start-SCSMConnector|Starts a Service Manager connector.|
|Test-SCSMManagementPack|Tests the validity of a management pack.|
|Update-SCSMAnnouncement|Updates the properties of an announcement for Service Manager.|
|Update-SCSMClassInstance|Updates property values of a configuration item class instance.|
|Update-SCSMConnector|Updates properties of a Service Manager connector.|
|Update-SCSMDCMWorkflow|Updates properties of a desired configuration management workflow.|
|Update-SCSMEmailTemplate|Updates properties of an Email template.|
|Update-SCSMPortalDeploymentProcess|Updates the properties of software deployment processes for the Self-Service Portal.|
|Update-SCSMPortalSoftwarePackage|Updates the properties of software packages that are configured for deployment in the Service Manager Self-Service Portal.|
|Update-SCSMRunAsAccount|Updates the credentials that are associated with a Run As account.|
|Update-SCSMSetting|Updates the configuration settings for Service Manager.|
|Update-SCSMSubscription|Updates subscription properties in Service Manager.|
|Update-SCSMUserRole|Sets the UserRole property for a Service Manager user.|
|Update-SCSMWorkflow|Updates workflow properties.|

## Data Warehouse Cmdlets in the Microsoft.EnterpriseManagement.Warehouse.Cmdlets Module

|Cmdlet|Description|
|----------|---------------|
|Disable-SCDWJob|Disables a data warehouse job to prevent it from running.|
|Disable-SCDWJobSchedule|The **Disable-SCDWJobSchedule** cmdlet disables a Data Warehouse job schedule, which causes the job schedule to stop initiating jobs. If the job schedule was previously enabled, disabling the job schedule retains the job schedule settings. To modify the job schedule settings, run the **Set-SCDWJobSchedule** cmdlet.|
|Disable-SCDWSource||
|Enable-SCDWJob|Enables a Data Warehouse job so that it can run according to its schedule.|
|Enable-SCDWJobSchedule|The **Enable-SCDWJobSchedule** cmdlet allows Data Warehouse administrators to enable job schedules so that jobs run according to their specified schedule. To disable the job schedule, use the **Disable-SCDWJobSchedule** cmdlet.|
|Enable-SCDWSource||
|Get-SCDWEntity||
|Get-SCDWJob|Gets the job status of all recurring jobs, including extraction, transformation, and load (ETL) jobs.|
|Get-SCDWJobModule|Returns detailed information for the specified job. This information includes job modules that are executed as part of the job.|
|Get-SCDWJobSchedule|The **Get-SCDWJobSchedule** cmdlet displays scheduling information for Data Warehouse jobs. You can use the **JobName** parameter to specify a job for which to display scheduling information. Otherwise, the **Get-SCDWJobSchedule** cmdlet displays scheduling information for all Data Warehouse jobs.|
|Get-SCDWModule||
|Get-SCDWRetentionPeriod|The Data Warehouse grooms out rows after a predefined retention period. This cmdlet gives the retention period for a particular entity in minutes. If no entity is provided, it gives back the default retention period for all entities.|
|Get-SCDWSource||
|Get-SCDWSourceType||
|Get-SCDWWatermark||
|New-SCDWSourceType|To register a source with the Data Warehouse, the Datasource Type first has to be registered with the Data Warehouse. This cmdlet helps to register a new Datasource Type by importing the suitable management pack and doing the appropriate configuration changes.|
|Register-SCDWSource||
|Set-SCDWJobSchedule|Sets the schedule for a Data Warehouse job.|
|Set-SCDWRetentionPeriod||
|Set-SCDWSource||
|Set-SCDWWatermark||
|Start-SCDWJob|Starts a Data Warehouse job.|
|Unregister-SCDWManagememtPack||
|Unregister-SCDWSource||


