---
description: This article provides an introduction to the Service Manager cmdlets for the Windows PowerShell command-line interface and describes how to get started using them.
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Configuring and Using the Service Manager Cmdlets for Windows PowerShell
ms.technology:  service-manager
ms.assetid:  f032839d-a148-4dd9-9309-a51a047f197a
---

# Configuring and Using the Service Manager Cmdlets for Windows PowerShell

>Applies To: System Center 2016 - Service Manager

This article provides an introduction to the Service Manager cmdlets for the Windows PowerShell command-line interface.

Before you can run any command in the Windows PowerShell command-line interface in Service Manager, you must set execution policy to RemoteSigned. Before you can run data warehouse cmdlets, you must manually import the data warehouse cmdlets module.

The Service Manager cmdlets are implemented in the following two modules:

-   **System.Center.Service.Manager**. This module is imported automatically every time a Service Manager Windows PowerShell session is opened.

-   **Microsoft.EnterpriseManagement.Warehouse.Cmdlets**. This module must be imported manually.

## Getting Started with Service Manager Cmdlets for Windows PowerShell

Windows PowerShell is a Windows command-line shell that includes an interactive prompt and a scripting environment. Windows PowerShell uses cmdlets to manipulate the Windows PowerShell objects. Service Manager includes many cmdlets that you can use to perform various Service Manager-related tasks without using the Service Manager console. For example, you can use the **Import-SCSMManagementPack** cmdlet to import a management pack.

The Service Manager cmdlets are delivered in two modules that are listed below. In Service Manager, these cmdlet modules are not installed in the typical path that is listed in the $env:PSModulePath variable. Therefore, if you run the `Get-Module -List` cmdlet, the Service Manager modules are not listed.

-   Administrator cmdlets: The System.Center.Service.Manager module which contains the cmdlets that are needed for common administrative tasks.

-   Data warehouse cmdlets: The Microsoft.EnterpriseManagement.Warehouse.Cmdlets module which contains the cmdlets that are needed for operating on the Service Manager data warehouse.

The data warehouse cmdlets operate on the data warehouse database, and you can run them on both the  Service Manager management server or the data warehouse management server.

Data returned from Windows PowerShell command might contain more information than can be displayed in a default Windows PowerShell command window. We recommend increasing the width of the command window: Right-click the title bar, click **Properties**, and in the **Layout** tab, set the **Screen Buffer Size** width to 120.

The following procedures help you to get started with Service Manager cmdlets.

### To open a Service Manager Windows PowerShell session from the Service Manager console

1.  In the Service Manager console, click **Administration**.

2.  On the **Tasks** pane, click **Start PowerShell Session**.

The administrator cmdlet module is automatically pre-imported in this session.

### To open a Service Manager Windows PowerShell session from Windows

1.  On the computer that hosts the Service Manager management server, on the taskbar, click **Start**, point to **All Programs**, and then click **Microsoft System Center**.

2.  Click **Service Manager 2016**, and then click **Service Manager Shell**.

The administrator cmdlet module is automatically pre-imported in this session.

### To list all Service Manager cmdlets

1.  Open a Service Manager Windows PowerShell session.

2.  To list the cmdlets that are included in the administrator module, in the Service Manager Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command -module System.Center.Service.Manager
    ```

3.  To list the cmdlets that are included in the data warehouse module, in the Service Manager Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command -module Microsoft.EnterpriseManagement.Warehouse.Cmdlets
    ```

### To get Help for a cmdlet

1.  Open a Service Manager Windows PowerShell session.

2.  You can now access the on-the-box Help, or you can use the `-online` parameter to access the most up-to-date online Help:
    -   On-the-box Help: Type the following command. Replace *cmdlet-name* with the name of the cmdlet that you want to get help for, for example, **Import-SCSMManagementPack**:

        ```
        Get-help <cmdlet-name> -detailed
        ```

    -   Online, up-to-date Help: Type the following command, and then press ENTER:

        ```
        Get-help <cmdlet-name> -online
        ```

        This command uses the `-online` parameter to access the latest online Help for a cmdlet. It opens a web browser and displays the online Help that is available for *cmdlet-name*.

## List of the Service Manager Cmdlets

Service Manager supports the following Windows PowerShell cmdlets, which are implemented in two modules: the administrator module and the data warehouse module.

### Administrator Cmdlets in the System.Center.Service.Manager Module

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
|New-SCOrchestratorConnector|Creates a new Service Manager Orchestrator connector.|
|New-SCRelationshipInstance|Creates an instance of a relationship.|
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
|New-SCSMRunAsAccount|Creates a new Run As account.|
|New-SCSMSubscription|Creates a new subscription in Service Manager.|
|New-SCSMUserRole|Creates a new user role in Service Manager.|
|New-SCSMWorkflow|Creates a new workflow in Service Manager.|
|New-SCVMMConnector|Creates a new Service Manager Virtual Machine Manager connector.|
|Protect-SCSMManagementPack|Seals a management pack, preventing it from being modified.|
|Remove-SCSMAllowListClass|Removes the specified classes from the Allow list of classes that are used by the Operations Manager CI Connector during synchronization in Service Manager.|
|Remove-SCSMAnnouncement|Removes an announcement from Service Manager.|
|Remove-SCSMClassInstance|Removes an instance of a configuration item object.|
|Remove-SCSMConnector|Removes a connector from Service Manager.|
|Remove-SCSMDCMWorkflow|Removes a desired configuration management workflow from Service Manager.|
|Remove-SCSMEmailTemplate|Removes an Email template from Service Manager.|
|Remove-SCSMManagementGroupConnection|Removes a management group connection.|
|Remove-SCSMManagementPack|Removes management packs.|
|Remove-SCSMRunAsAccount|Removes a Run As accounts.|
|Remove-SCSMSubscription|Removes a subscription from Service Manager.|
|Remove-SCSMUserRole|Removes a user role from Service Manager.|
|Remove-SCSMWorkflow|Removes a workflow from Service Manager.|
|Reset-SCSMAllowList|Resets the Allow list of classes that is used by the Operations Manager CI Connector in Service Manager to the default Allow list.|
|Restore-SCSMDeletedItem|Restores items that were previously deleted in Service Manager.|
|Set-SCSMChannel|Sets the properties of the email notification channel in Service Manager.|
|Set-SCSMManagementGroupConnection|Sets the specified connection as the active connection. The active connection is the connection that is implicitly used when you run a **Get-** cmdlet without specifying **-ComputerName** and **-Credential** or **-SCSession** parameters. Only one connection can be active at any time, and by default the active connection is the last connection that was created by using the **New-SCManagementGroupConnection** cmdlet.|
|Start-SCSMConnector|Starts a Service Manager connector.|
|Test-SCSMManagementPack|Tests the validity of a management pack.|
|Update-SCSMAnnouncement|Updates the properties of an announcement for Service Manager.|
|Update-SCSMClassInstance|Updates property values of a configuration item class instance.|
|Update-SCSMConnector|Updates properties of a Service Manager connector.|
|Update-SCSMDCMWorkflow|Updates properties of a desired configuration management workflow.|
|Update-SCSMEmailTemplate|Updates properties of an Email template.|
|Update-SCSMRunAsAccount|Updates the credentials that are associated with a Run As account.|
|Update-SCSMSetting|Updates the configuration settings for Service Manager.|
|Update-SCSMSubscription|Updates subscription properties in Service Manager.|
|Update-SCSMUserRole|Sets the UserRole property for a Service Manager user.|
|Update-SCSMWorkflow|Updates workflow properties.|

### Data Warehouse Cmdlets in the Microsoft.EnterpriseManagement.Warehouse.Cmdlets Module

|Cmdlet|Description|
|----------|---------------|
|Disable-SCDWJob|Disables a data warehouse job to prevent it from running.|
|Disable-SCDWJobSchedule|The **Disable-SCDWJobSchedule** cmdlet disables a Data Warehouse job schedule, which causes the job schedule to stop initiating jobs. If the job schedule was previously enabled, disabling the job schedule retains the job schedule settings. To modify the job schedule settings, run the **Set-SCDWJobSchedule** cmdlet.|
|Disable-SCDWSource|Enables all jobs that are affiliated with the specified data source.|
|Enable-SCDWJob|Enables a Data Warehouse job so that it can run according to its schedule.|
|Enable-SCDWJobSchedule|The **Enable-SCDWJobSchedule** cmdlet allows Data Warehouse administrators to enable job schedules so that jobs run according to their specified schedule. To disable the job schedule, use the **Disable-SCDWJobSchedule** cmdlet.|
|Enable-SCDWSource|Enables all jobs that are affiliated with the specified data source.|
|Get-SCDWEntity|Gets the list of fact tables, dimensions, tables, and outriggers that exist in a data warehouse.|
|Get-SCDWJob|Gets the job status of all recurring jobs, including extraction, transformation, and load (ETL) jobs.|
|Get-SCDWJobModule|Returns detailed information for the specified job. This information includes job modules that are executed as part of the job.|
|Get-SCDWJobSchedule|The **Get-SCDWJobSchedule** cmdlet displays scheduling information for Data Warehouse jobs. You can use the **JobName** parameter to specify a job for which to display scheduling information. Otherwise, the **Get-SCDWJobSchedule** cmdlet displays scheduling information for all Data Warehouse jobs.|
|Get-SCDWModule||
|Get-SCDWRetentionPeriod|The Data Warehouse grooms out rows after a predefined retention period. This cmdlet gives the retention period for a particular entity in minutes. If no entity is provided, it gives back the default retention period for all entities.|
|Get-SCDWSource|Enables all jobs that are affiliated with the specified data source.|
|Get-SCDWSourceType|Gets the types of data sources that can be registered to the data warehouse.|
|Get-SCDWWatermark|Gets the latest watermark for the specified job module.|
|New-SCDWSourceType|To register a source with the Data Warehouse, the Datasource Type first has to be registered with the Data Warehouse. This cmdlet helps to register a new Datasource Type by importing the suitable management pack and doing the appropriate configuration changes.|
|Register-SCDWSource|Registers instances of data source types, such as Service Manager, Operations Manager, and Configuration Manager, to the data warehouse.|
|Set-SCDWJobSchedule|Sets the schedule for a Data Warehouse job.|
|Set-SCDWRetentionPeriod|Sets the data retention period in minutes for either a specific fact table within a specific data warehouse database or sets the default for fact tables within the database.|
|Set-SCDWSource|Updates the definition of classes and relationships that can be populated for an instance of a data source.|
|Set-SCDWWatermark|- Sets the watermark from which subsequent data processing should continue.|
|Start-SCDWJob|Starts a Data Warehouse job.|
|Unregister-SCDWManagememtPack||
|Unregister-SCDWSource|Unregisters a data source from the data warehouse.|
