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
About Managing the Data Warehouse supports the following Windows PowerShell cmdlets, which are implemented in two modules: the administrator module and the data warehouse module.

## Administrator Cmdlets in the System.Center.Service.Manager Module

|Cmdlet|Description|
|----------|---------------|
|Add\-SCSMAllowListClass|Adds the specified classes to the Allow list of classes that is used by the [!INCLUDE[smshort](../../includes/smshort_md.md)] Operations Manager CI Connector during synchronization.|
|Export\-SCSMManagementPack|Exports a management pack as a valid XML\-formatted file that you can later import into [!INCLUDE[smshort](../../includes/smshort_md.md)] or [!INCLUDE[om12short](../../includes/om12short_md.md)].|
|Get\-SCSMAllowList|Retrieves the Allow list of classes that is used by the [!INCLUDE[smshort](../../includes/smshort_md.md)] Operations Manager CI Connector during synchronization.|
|Get\-SCSMAnnouncement|Retrieves announcements that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMChannel|Retrieves the Email Notification channels that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMClass|Retrieves a class.|
|Get\-SCSMClassInstance|Retrieves class instance objects.|
|Get\-SCSMCommand||
|Get\-SCSMConnector|Retrieves connectors that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMDCMWorkflow|Retrieves the list of desired configuration management workflows that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMDeletedItem|Retrieves items that have been marked for deletion in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMDiscovery|Retrieves discovery information from [!INCLUDE[om12short](../../includes/om12short_md.md)] and from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMEmailTemplate|Retrieves Email templates that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMEmailTemplateContent|Retrieves the content of [!INCLUDE[smshort](../../includes/smshort_md.md)] Email templates.|
|Get\-SCSMGroup|Retrieves groups from [!INCLUDE[om12short](../../includes/om12short_md.md)] and from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMManagementGroupConnection|Retrieves all management group connections, including the IsActive state of these connections. Only one connection will have its IsActive state set to True, because only one connection can be active at any time.|
|Get\-SCSMManagementPack|Retrieves objects that represent management packs that have been imported.|
|Get\-SCSMObjectTemplate|Retrieves an object template.|
|Get\-SCSMPortalCMConfiguration|Retrieves the settings for the Configuration Manager that is used for software deployments on the [!INCLUDE[smshort](../../includes/smshort_md.md)][!INCLUDE[smssp](../../includes/smssp_md.md)].|
|Get\-SCSMPortalContactConfiguration|Retrieves the IT Contact setting that the  [!INCLUDE[smssplong](../../includes/smssplong_md.md)] is configured with.|
|Get\-SCSMPortalDeploymentProcess|Retrieves information about software deployment processes for the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Get\-SCSMPortalSoftwarePackage|Retrieves all the software packages that are configured for deployment in the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Get\-SCSMQueue|Retrieves queues that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMRelationship|Retrieves information about relationship objects from [!INCLUDE[om12short](../../includes/om12short_md.md)] and from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMRelationshipInstance|Retrieves the instances of relationships from [!INCLUDE[om12short](../../includes/om12short_md.md)] and from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMRunAsAccount|Retrieves Run As accounts.|
|Get\-SCSMSetting|Retrieves configuration settings of System Center [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMSubscription|Retrieves subscriptions that are configured in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMTask|Retrieves tasks that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMUser|Retrieves users that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMUserRole|Retrieves user roles that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMView|Retrieves views that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Get\-SCSMWorkflow|Retrieves configuration information for [!INCLUDE[smshort](../../includes/smshort_md.md)] workflows.|
|Get\-SCSMWorkflowStatus|Retrieves the status of workflows in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Import\-SCSMInstance|Imports objects and relationships from a comma\-separated value \(.csv\) file into [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Import\-SCSMManagementPack|Imports management packs.|
|New\-SCOrchestratorConnector||
|New\-SCRelationshipInstance||
|New\-SCSMADConnector|Creates a new Active Directory connector.|
|New\-SCSMAlertRule|Creates an alert rule to be used with an Operations Manager alert connector in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMAnnouncement|Creates a new announcement in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMClassInstance|Adds a class instance to the database.|
|New\-SCSMCMConnector|Creates a new Configuration Manager connector in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMDCMWorkflow|Creates a new desired configuration management workflow in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMEmailTemplate|Creates a new Email template for [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMManagementGroupConnection|Creates a new connection for the specified management group. The most recent management group connection that was created is the active connection that  **Get\-** cmdlets use by default, in which you did not specify the **ComputerName** and **Credential**, or the **SCSession** parameters.|
|New\-SCSMManagementPack|Creates a new management pack.|
|New\-SCSMManagementPackBundle|Bundles individual management packs and their resources, creating a new management pack bundle.|
|New\-SCSMOMAlertConnector|Creates a new [!INCLUDE[om12short](../../includes/om12short_md.md)] alert connector in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMOMConfigurationItemConnector|Creates a new Operations Manager CI connector in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMPortalDeploymentProcess|Creates a software deployment process for deploying software by using the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|New\-SCSMRunAsAccount|Creates a new Run As account.|
|New\-SCSMSubscription|Creates a new subscription in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMUserRole|Creates a new user role in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCSMWorkflow|Creates a new workflow in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|New\-SCVMMConnector||
|Protect\-SCSMManagementPack|Seals a management pack, preventing it from being modified.|
|Remove\-SCSMAllowListClass|Removes the specified classes from the Allow list of classes that are used by the Operations Manager CI Connector during synchronization in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMAnnouncement|Removes an announcement from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMClassInstance|Removes an instance of a configuration item object.|
|Remove\-SCSMConnector|Removes a connector from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMDCMWorkflow|Removes a desired configuration management workflow from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMEmailTemplate|Removes an Email template from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMManagementGroupConnection|Removes a management group connection.|
|Remove\-SCSMManagementPack|Removes management packs.|
|Remove\-SCSMPortalDeploymentProcess|Removes a software deployment process from the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Remove\-SCSMRunAsAccount|Removes a Run As accounts.|
|Remove\-SCSMSubscription|Removes a subscription from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMUserRole|Removes a user role from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Remove\-SCSMWorkflow|Removes a workflow from [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Reset\-SCSMAllowList|Resets the Allow list of classes that is used by the Operations Manager CI Connector in [!INCLUDE[smshort](../../includes/smshort_md.md)] to the default Allow list.|
|Restore\-SCSMDeletedItem|Restores items that were previously deleted in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Set\-SCSMChannel|Sets the properties of the email notification channel in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Set\-SCSMManagementGroupConnection|Sets the specified connection as the active connection. The active connection is the connection that is implicitly used when you run a **Get\-** cmdlet without specifying **–ComputerName** and **–Credential** or **–SCSession** parameters. Only one connection can be active at any time, and by default the active connection is the last connection that was created by using the **New\-SCManagementGroupConnection** cmdlet.|
|Set\-SCSMPortalCMConfiguration|Sets the configuration information for the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Set\-SCSMPortalContactConfiguration|Configures the settings of information technology \(IT\) contacts for the end\-user of the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Start\-SCSMConnector|Starts a [!INCLUDE[smshort](../../includes/smshort_md.md)] connector.|
|Test\-SCSMManagementPack|Tests the validity of a management pack.|
|Update\-SCSMAnnouncement|Updates the properties of an announcement for [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Update\-SCSMClassInstance|Updates property values of a configuration item class instance.|
|Update\-SCSMConnector|Updates properties of a [!INCLUDE[smshort](../../includes/smshort_md.md)] connector.|
|Update\-SCSMDCMWorkflow|Updates properties of a desired configuration management workflow.|
|Update\-SCSMEmailTemplate|Updates properties of an Email template.|
|Update\-SCSMPortalDeploymentProcess|Updates the properties of software deployment processes for the [!INCLUDE[smssp](../../includes/smssp_md.md)].|
|Update\-SCSMPortalSoftwarePackage|Updates the properties of software packages that are configured for deployment in the [!INCLUDE[smssplong](../../includes/smssplong_md.md)].|
|Update\-SCSMRunAsAccount|Updates the credentials that are associated with a Run As account.|
|Update\-SCSMSetting|Updates the configuration settings for [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Update\-SCSMSubscription|Updates subscription properties in [!INCLUDE[smshort](../../includes/smshort_md.md)].|
|Update\-SCSMUserRole|Sets the UserRole property for a [!INCLUDE[smshort](../../includes/smshort_md.md)] user.|
|Update\-SCSMWorkflow|Updates workflow properties.|

## Data Warehouse Cmdlets in the Microsoft.EnterpriseManagement.Warehouse.Cmdlets Module

|Cmdlet|Description|
|----------|---------------|
|Disable\-SCDWJob|Disables a data warehouse job to prevent it from running.|
|Disable\-SCDWJobSchedule|The **Disable\-SCDWJobSchedule** cmdlet disables a Data Warehouse job schedule, which causes the job schedule to stop initiating jobs. If the job schedule was previously enabled, disabling the job schedule retains the job schedule settings. To modify the job schedule settings, run the **Set\-SCDWJobSchedule** cmdlet.|
|Disable\-SCDWSource||
|Enable\-SCDWJob|Enables a Data Warehouse job so that it can run according to its schedule.|
|Enable\-SCDWJobSchedule|The **Enable\-SCDWJobSchedule** cmdlet allows Data Warehouse administrators to enable job schedules so that jobs run according to their specified schedule. To disable the job schedule, use the **Disable\-SCDWJobSchedule** cmdlet.|
|Enable\-SCDWSource||
|Get\-SCDWEntity||
|Get\-SCDWJob|Gets the job status of all recurring jobs, including extraction, transformation, and load \(ETL\) jobs.|
|Get\-SCDWJobModule|Returns detailed information for the specified job. This information includes job modules that are executed as part of the job.|
|Get\-SCDWJobSchedule|The **Get\-SCDWJobSchedule** cmdlet displays scheduling information for Data Warehouse jobs. You can use the **JobName** parameter to specify a job for which to display scheduling information. Otherwise, the **Get\-SCDWJobSchedule** cmdlet displays scheduling information for all Data Warehouse jobs.|
|Get\-SCDWModule||
|Get\-SCDWRetentionPeriod|The Data Warehouse grooms out rows after a predefined retention period. This cmdlet gives the retention period for a particular entity in minutes. If no entity is provided, it gives back the default retention period for all entities.|
|Get\-SCDWSource||
|Get\-SCDWSourceType||
|Get\-SCDWWatermark||
|New\-SCDWSourceType|To register a source with the Data Warehouse, the Datasource Type first has to be registered with the Data Warehouse. This cmdlet helps to register a new Datasource Type by importing the suitable management pack and doing the appropriate configuration changes.|
|Register\-SCDWSource||
|Set\-SCDWJobSchedule|Sets the schedule for a Data Warehouse job.|
|Set\-SCDWRetentionPeriod||
|Set\-SCDWSource||
|Set\-SCDWWatermark||
|Start\-SCDWJob|Starts a Data Warehouse job.|
|Unregister\-SCDWManagememtPack||
|Unregister\-SCDWSource||


