---
title:  Import data from Configuration Manager
description: Describes how to import data from Configuration Manager into Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: abaf3337-f620-4220-bbbb-13007dc72754
---

# Import data from Configuration Manager into Service Manager

>Applies To: System Center 2016 - Service Manager

This article describes how to create, configure, disable, and enable a Configuration Manager connector, and how to customize the Configuration Manager extended SMS_def.mof file for collecting hardware information. You use the connector to import data from System Center Configuration Manager into Service Manager.

The connector for Configuration Manager recognizes User-device Affinity and Mobile Devices and synchronizes them in the Service Manager database.

You can import data from the System Center Configuration Manager site database into the Service Manager database. This automatically creates and populates configuration items for the hardware and software that you want to manage in Service Manager. After you import data from System Center Configuration Manager, you can attach the respective configuration items to relevant incidents, and the information in the configuration items will be available to analysts working on the incident.

By using a Configuration Manager connector, you can import configuration baselines from System Center Configuration Manager and then use these configuration baselines to automatically generate incidents for noncompliant configuration items.

For information about Microsoft Operations Framework (MOF) implementation of change and configuration, see [Position of the Change and Configuration SMF Within the MOF IT Service Lifecycle](https://go.microsoft.com/fwlink/p/?LinkID=115631).

## Complete the data warehouse registration process
Before you create the Configuration Manager connector, you must make sure that the Data Warehouse Registration process is complete.

## Additional data in Configuration Manager
Additional data in Configuration Manager includes User-Device Affinity (UDA), Mobile Device Data, and Software Request Data. UDA data from Configuration Manager more accurately determines who the primary user of a computer or device is. The UDA data collected by the Service Manager Configuration Manager connector is used to populate the UsesComputer and PrimaryUser information in the Service Manager database.

Mobile device data for Windows Phones, Windows Mobile Phones, and Nokia devices will be collected by the Service Manager Configuration Manager connector. Data from other mobile devices such as iPhone, BlackBerry, and Android-based phones will be collected when you are using the Configuration Manager Exchange Server connector. Mobile device data will be imported into the Service Manager database as configuration items, and it can be associated with work items, incident management, and change management.

Software request data will be used in support of self-service software request integration with Configuration Manager. The administrative category data from Configuration Manager will be used to select which Service Request templates to apply when creating a request from the Self-Service Portal.

## Schedule
You can configure the Configuration Manager connector to update the Service Manager database on a recurring schedule. You can also temporarily suspend the importation of data from Configuration Manager by disabling the connector. For example, you can disable the connector when maintenance is performed on the Configuration Manager site database because you know that the maintenance process temporarily creates inaccurate data. When appropriate, you can re-enable the connector and resume importing data.

## Extended hardware inventory with Configuration Manager
In Configuration Manager, you can extend the hardware inventory by collecting an inventory of additional Windows Management Instrumentation (WMI) classes, additional WMI class attributes, registry keys, and other customizations to accommodate your organization's requirements. For more information about extending the hardware inventory in Configuration Manager, see [How to Extend Hardware Inventory](https://go.microsoft.com/fwlink/p/?LinkID=160640).

If you have extended the hardware inventory in Configuration Manager, you must create a new Configuration Manager Connector management pack in Service Manager to collect the extended hardware inventory. This new management pack can contain only the information required to collect the extended hardware inventory from Configuration Manager, or it can consist of everything from the original Configuration Manager Connector management pack plus the new extended hardware inventory. For information about creating a new connector management pack, see [How to Configure a Configuration Manager Connector for an Extended SMS_def.mof File](admin-how-to-configure-a-configuration-manager-connector-for-an-extended-sms-def.mof-file.md).

## Importing software configuration items
You can import software configuration items with the Configuration Manager Connector by importing  the following asset intelligence reporting classes in System Center Configuration Manager. These classes should be enabled in Configuration Manager before you configure the Configuration Manager connector in Service Manager. For more information about enabling Asset  Intelligence in Configuration Manager, see [How to Enable Asset Intelligence](https://go.microsoft.com/fwlink/p/?LinkId=262404).

-   SMS_InstalledSoftware

-   SMS_SystemConsoleUsage

-   SMS_SystemConsoleUser

-   SoftwareLicensingService

-   SoftwareLicensingProduct

If software for a particular computer does not appear in the **All Software** view in the Configuration Items workspace, you should review the Operations Manager event log on the Service Manager primary management server. You should look for events with sources of OpsMgr Connector and Lfx Service to determine if there are any errors.

## Create a Configuration Manager connector

You can use the following procedures to create a connector to import data from Configuration Manager into System Center 2016 - Service Manager and confirm the status of the connector.

> [!IMPORTANT]
> Before you can create the Configuration Manager connector, you have to verify that System Center Configuration Manager is installed in your environment, and you have to turn on Windows User Account Control (UAC). For more information about UAC, see [User Account Control](https://go.microsoft.com/fwlink/p/?LinkID=177523).

### To create a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.
3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Configuration Manager Connector**. The System Center Configuration Manager Connector Wizard starts.
4.  On the **Before You Begin** page, click **Next**.
5.  On the **General** page, do the following:
    1.  In the **Name** box, type a name for the new connector. For example, type **Configuration Manager Connector to Seattle**.
    2.  In the **Description** box, type a description for the new connector. For example, type **A Configuration Manager connector to site Seattle**.
    3.  Make sure that the **Enabled** check box is selected, and then click **Next**.
6.  On the **Select Management Pack** page, in the **Management Pack** list, select either **System Center Configuration Manager Connector Configuration** or **System Center Configuration Manager 2012 Connector Configuration**, and then click **Next**.
7.  On the **Connect to System Center Configuration Manager Database** page, do the following:
    1.  In the **Database Server Name** box, type the server name of the server that is hosting the System Center Configuration Manager site database and the database named instance, if applicable. For example, at the hypothetical Woodgrove Bank, you might type **woodgrove\instance1** if the System Center Configuration Manager database is on a named instance of Microsoft SQL Server, or type **woodgrove** if the database is on a default instance of SQL Server.
    2.  In the **Database Name** box, type the name of the System Center Configuration Manager site database. For example, type **SMS_CM1**.
    3.  In the **Credentials** area, select a Run As account, or create a new Run As account. The user account that you specify as the Run As account must be a member of the smsdbrole_extract and the db_datareader groups for the Configuration Manager site database.
    4.  In the **Credentials** area, click **Test Connection**.
    5.  In the **Credentials** dialog box, in the **Password** box, type the password for the account, and then click **OK**.
    6.  In the **Test Connection** dialog box, if you receive the following confirmation message, click **OK**:
        **The connection to the server was successful**.
    7.  Click **Next**.
8.  On the **Collections** page, select the appropriate collection, and then click **Next**.
9. On the **Schedule** page, in the **Synchronize** list, set the frequency and time of synchronization, and then click **Next**.
10. On the **Summary** page, confirm the connector settings you made, and then click **Create**.
11. On the **Confirmation** page, make sure that you receive the following confirmation message:
    *You have successfully completed the System Center Configuration Manager Connector Wizard.*
    Then, click **Close**.

    > [!NOTE]
    > The System Center Configuration Manager Connector Wizard may take several hours to import data from System Center Configuration Manager.

### To validate the creation of a Configuration Manager connector

1.  Confirm that the Configuration Manager connector that you created is displayed in the **Connectors** pane.
2.  In the Service Manager console, click **Configuration Items**. In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**. Verify that the intended computers from  appear in the **All Windows Computers** pane.
3.  In the middle pane, double-click a newly imported computer. Verify that the appropriate computer details appear in the computer form.

### To confirm the status of a Configuration Manager connector

-   View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of completion.

![PowerShell symbol](./media/import-data-cm/pssymbol.png)You can use a Windows PowerShell command to create a new Configuration Manager connector. For information about how to use Windows PowerShell to create a new Configuration Manager connector in Service Manager, see [New-SCCMConnector](https://go.microsoft.com/fwlink/p/?LinkId=225350).

## Disable and enable a Configuration Manager connector

You can use the following procedures to disable or enable a System Center Configuration Manager connector and validate the status of the change.

### To disable a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.
3.  In the **Connectors** pane, select the Configuration Manager connector that you want to disable. For example, click **Configuration Manager connector to SEA**.
4.  In the **Tasks** pane, under the connector name, click **Disable**.

    > [!NOTE]
    > If you disable a connector while it is synchronizing data, the synchronization process may not stop. However, a disabled connector will not import any new data from a Configuration Manager database from that point forward.

### To enable a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.
3.  In the **Connectors** pane, select the Configuration Manager connector that you want to enable. For example, click **Configuration Manager connector to SEA**.
4.  In the **Tasks** pane, under the connector name, click **Enable**.

### To validate the status change of a Configuration Manager connector

1.  After you disable or enable the connector, wait 30 seconds. Then, in the Service Manager console, click **Administration**, and then click **Connectors**.
2.  In the **Connectors** pane, locate the connector for which you have changed status, and verify the value in the **Enabled** column.
3.  If you enabled the connector, verify that the connector resumes synchronization according to the schedule. If you disabled the connector, verify that the connector no longer synchronizes according to the schedule.

![PowerShell symbol](./media/import-data-cm/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

-   For information about how to use Windows PowerShell to start a Service Manager connector, see [Start-SCSMConnector](https://go.microsoft.com/fwlink/?LinkId=203113).
-   For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkId=225320).
-   For information about how to use Windows PowerShell to update the properties of a Service Manager connector, see [Update-SCSMConnector](https://go.microsoft.com/fwlink/p/?LinkID=225382).

## Synchronize a Configuration Manager connector

To ensure that the Service Manager database is up to date, the System Center Configuration Manager connector synchronizes with Configuration Manager every day after the initial synchronization. However, you can use the following procedures to synchronize the connector manually and validate that the connector synchronized.

### To manually synchronize a Configuration Manager connector

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.
3.  In the **Connectors** pane, select the Configuration Manager connector that you want to synchronize.
4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

    > [!NOTE]
    > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### To validate that a Configuration Manager connector synchronized

1.  In the Service Manager console, click **Configuration Items**.
2.  In the **Configuration Items** pane, expand **Computers**, and then click **All Windows Computers**. Verify that any new computers in Configuration Manager appear in the middle pane.

## Configure a Configuration Manager connector for an extended SMS_def.mof file

Service Manager hardware inventory collects and then provides system information, such as available disk space, processor type, and operating system, about each computer in the Configuration Manager hierarchy. In Configuration Manager, users can customize the default Configuration Manager SMS_def.mof file to extend the hardware inventory information that is collected.

When you create a Configuration Manager connector in Service Manager, you can select the default System Center Configuration Manager Connector Configuration management pack that must be used for that connector. By using the default management pack, the connector imports hardware, software, and desired configuration management information for the computers that are in the system.

If the Configuration Manager SMS_def.mof file has been extended to collect additional hardware inventory data, which you also want to import into Service Manager, you must create a new custom management pack that defines that additional data. Then, you have to create a new Configuration Manager connector and configure it to use the new custom management pack.

### Import extended hardware inventory data from Configuration Manager
To import extended hardware inventory data from Configuration Manager, you must author a custom Configuration Manager connector management pack. There are two approaches to implementing a custom Configuration Manager connector:

-   Create a custom Configuration Manager connector management pack that defines the extended data that you want to import and then create two connectors. Configure one connector to use the default System Center Configuration Manager Connector Configuration management pack to import the data that is defined by default. Configure the second connector to use the custom management pack to import the additional extended data.

-   Customize the default System Center Configuration Manager Connector Configuration management pack to also include the additional extended data. Create a single connector that is configured to use the custom management pack to import all the information that you must have.

This topic provides the information that you must have to implement the first approach that is described earlier. It provides the details that you must have so that you can develop a custom Configuration Manager connector management pack that imports the extended hardware inventory from Configuration Manager.

The high-level steps to importing extended hardware inventory data are as follows:

1.  Create a custom Configuration Manager Connector Configuration management pack with the definitions for the extended data.
2.  Import the custom management pack into Service Manager. After you import the management pack, Service Manager processes the directives in the management pack to create staging tables and to run any install Structured Query Language (SQL) scripts, as defined in the management pack.
3.  Create a Configuration Manager connector and configure it to use the custom management pack.
4.  The Configuration Manager connector imports the data.

### Work with a custom Configuration Manager Connector management pack
Consider the following tips when you are working with a custom Configurations Manager Connector management pack:

-   Semantic errors in the connector configuration templates in the management pack do not prevent the management pack from being imported, and they are logged to the event log. In this case, you must delete the management pack, correct the errors, and reimport the management pack.

-   After creating a Configuration Manager connector, you cannot modify its management pack selection. Instead, you must delete that connector and then create a new one with the desired management pack selection.

-   To ensure a successful deletion of a management pack, you must delete any connectors that are configured to use the management pack that you want to delete and then delete the management pack.

    When you delete a custom Configurations Manager Connector management pack, Service Managerr tries to delete all related staging tables that were created during the management pack import. Then, Service Manager runs any scripts that are defined in the **Uninstall** section of the management pack.

-   Unlike other management packs, the custom Configuration Manager Connector management pack cannot be versioned. Importing a later version of the management pack will succeed. However, the connector configuration in the management pack will be ignored, or it might cause validation errors that are logged to the event log.

### Create custom Configuration Manager Connector Configuration management pack
A custom Configuration Manager Connector Configuration management pack is similar in structure to the default Configuration Manager Connector management pack. It must contain the two object templates **DataProvider** and **DataConsumer** that specify how the data should be imported and applied.

#### DataProvider section
The **DataProvider** section provides information, such as which data to import, that you must have when you are importing data from Configuration Manager into the staging tables of **LinkingFramework**. The **DataProvider** section includes the queries that run on the Configuration Manager site database; directives for staging table creation; custom SQL scripts; and information that is relevant for incremental synchronization, such as watermarking and batching.

#### DataConsumer section

The **DataConsumer** section provides information about reading the data from staging tables and writing it to the **ServiceManager** database's instances space, such as **Entities** or **Relationships**. The **DataConsumer** section includes queries that run on the staging tables; mapping to the Service Manager type system; custom SQL scripts; and information that is relevant for incremental synchronization, such as watermarking and batching.

#### Structure of the DataProvider and DataConsumer object templates sections
Basically, the **DataProvider** and the **DataConsumer** are object templates that are targeted to a projection type. The following code shows the general structure of the **DataProvider** and the **DataConsumer** sections:

```
<TypeProjection ID="System.LinkingFramework.DataConnector.Projection" Accessibility="Public" Type="System.LinkingFramework.DataConnector">
          <Component Alias="DataTable" Path="$Context/Path[Relationship='System.LinkingFramework.ConnectorEmbedsTables' TypeConstraint='System.LinkingFramework.DataTable']$">
            <Component Alias="Field" Path="$Context/Path[Relationship='System.LinkingFramework.TableEmbedsFields']$" />
          </Component>
          <Component Alias="DataCollection" Path="$Context/Path[Relationship='System.LinkingFramework.ConnectorEmbedsCollections' TypeConstraint='System.LinkingFramework.DataCollection']$" />
 </TypeProjection>

```

In this code, **DataTable**, **Field**, and **DataCollection** are defined as follows:

-   **DataTable**. The smallest data unit that is defined for data transfer. It is a declaration of what data to retrieve from the external data source. It also defines dependencies between different data tables and when data batching, watermarking, and grooming have finished.

-   **Field**. A single column in a data table.

-   **DataCollection**. A set of data tables to be transferred in one data transfer job or session. It defines which data tables are included in this data collection.

### Properties in the custom management pack
The following table provides the details about each property in the custom Configuration Manager Connector Configuration management pack. Use these guidelines when you create the custom management pack.

|Property|Expected value|Validation after import|
|------------|------------------|---------------------------|
|ID|For both **DataProvider** and **DataConsumer** templates as indicated in the sample|Yes|
|**DataConnector Properties**|||
|DataConnectorName|For both **DataProvider** and **DataConsumer** templates - identical to the values in the sample|Yes|
|IsProvider|In **DataProvider** template - True<br /><br />In **DataConsumer** template - False|Yes|
|SolutionName|A comment. For example, it can indicate the type of the imported data.|An attempt to import a management pack in which the solution name is already being used; it causes an error that is logged to the event log.|
|Entrypoint, EntryAssembly & WinformUIAssembly|Identical to the value in the sample||
|InstallSQLScripts section|SQL scripts that must run after the staging tables are set up. They are usually used in the **DataConsumer** template to configure views that display data from the staging tables.<br /><br />Everything that is enclosed between the <Script\><\/Script> tags is expected to be valid SQL script. Therefore, for comments, you must use the `/*` and the `*/` multi-line comment delimiters instead of the standard XML comment tags.|Not validated. Use custom table names to ensure that this does not cause overwriting or changing any tables except the ones that are declared in the management pack.|
|UnInstallSQLScripts section|SQL scripts that must run after you delete the Configuration Manager Connector management pack in the Service Manager console.<br /><br />Everything that is enclosed between the <Script\><\/Script> tags is expected to be valid SQL script. Therefore, for comments, you must use the `/*` and the `*/` multi-line comment delimiters instead of the standard XML comment tags.|Not validated. Use custom table names to ensure that this does not cause overwriting or changing any tables except the tables that are declared in the management pack.|
|DisableParallelProcessing|True||
|**DataTable Properties**|||
|DataName|The table from which to import data. It is used in the user interface (UI) and not used in queries.||
|StageTableName|The name of the staging table. It must be unique.|An attempt to import a management pack, in which the table name is already being used, causes an error to be logged to the event log.|
|WatermarkField|The name of the **rowversion** column||
|WatermarkType|Possible values are:<br /><br />-   0-Indicates **DateTime** type<br />-   1-Indicates the **Timestamp** type<br />-   (-1)-Indicates no watermarking, in which case **WatermarkField** becomes optional|Other types of watermarking are not supported.|
|BatchIdField|The name of the column that has good selectivity; used to separate incremental data into batches when importing to staging tables||
|BatchIdType|Possible values are:<br /><br />-   0-Int<br />-   (-1)-No batching, in which case **BatchIdField** becomes optional|Integer column|
|BatchIdSize|The size of the batch, if batching is used. A high number indicates that much data is being read or written at the same time. The recommended value is 500.|Integer column|
|UseCache|True||
|GroomType|Possible values are:<br /><br />-   1-The data in staging tables can be groomed after it is transferred to the Service Manager database.<br />-   2-The data in staging tables is groomed only after it is marked as deleted in the Configuration Manager database and has also been deleted in the Service Manager database because of the Service Manager connector synchronization.||
|QueryString|The actual query that Configuration Manager 2007 uses to retrieve the requested data. The query must be of the form:<br /><br />`SELECT ...`<br /><br />`FROM ...`<br /><br />`WHERE ...`<br /><br />`ORDER BY ...`<br /><br />The WHERE clause can contain the `$COLLECTIONLIST` token. During synchronization, this token is replaced by the collections that are specified in the System Center Configuration Manager Connector Wizard.<br /><br />The data that is exposed by Configuration Manager SCCM_Ext.* views is supported for import. This data can be extended by using standard sms_def.mof extensions or by using noidmifs. Other tables are not supported.<br /><br />Notably, subqueries are not supported, but joins to other tables are supported.|Not validated. All queries have an Lfx_Status column with value `U` or `D`, indicating whether the row represents an Update or a Delete operation.|
|CollectionName|A name for a group of data tables; this name must be unique. Tables in the same collection cannot depend on each other.|An attempt to import a management pack, in which the collection name is already being used, causes an error to be logged to the event log.|
|PrimaryKeyName|A section that declares the unique primary key name for the staging table.|An attempt to import a management pack, in which the key name is already being used, causes an error to be logged to the event log.|
|DependOnDataTable|The name or names of **DataTable** that must be synchronized first before this one. Typically, this is used to synchronize the staging table before the system reads it in the Consumer view.<br /><br />If you are using multiple collections, dependency should be expressed only between tables in different collections.|Not validated|
|**DataField Properties**|||
|Name, Type, AllowNull|These are required fields for any column type. Supported types are **int**, **nvarchar**, **datetime** and **xml**.|Not validated|
|PrimaryKeyACs, PrimaryKeyPosition|If part of primary key, indicates the position from the left in the primary key. Lfx adds two internal use columns (Lfx_Status, Lfx_SourceId) to the PK at the end.||
|Collation|DATABASE_DEFAULT|Not validated|
|**DataCollection Properties**|||
|DataCollectionName|Must be identical to what is referenced by a **DataTable** property|An attempt to import a management pack, in which the collection name is already being used, causes an error to be logged to the event log.|
|StagingName|In DataProvider template-DefaultCache<br /><br />In DataConsumer template-Not present|Not validated|
|DataTables|Comma-separated value (CSV) list of tables referencing this collection||
|Settings|In **DataProvider** template-Not present<br /><br />In **DataConsumer** template-Indicates type mapping|Escaped XML with following syntax:<br /><br />`<TypeName>Microsoft.Windows.Computer</TypeName>`<br /><br />`<MPName>Microsoft.Windows.Library</MPName>`<br /><br />`<MPVersion>version of MP</MPVersion>`<br /><br />`<MPToken>token for MP</MPToken>`|

### Custom Configuration Manager Connector Configuration management packs samples
The following are schema definitions and Configuration Manager Connector management pack samples that import data from the Configuration Manager SCCM_Ext.vex_GS_PC_BIOS view.

Refer to the table earlier in this topic for more information about the properties of these management packs. Use an XML editor, such as the editor in Microsoft Visual Studio, to modify these samples to fit your import scenarios.

#### Import data from a hosted class
When you are specifying a class that is hosted, the view in the **DataConsumer** template should include columns for the key property of the parent class. In this sample, the class that contains the BIOS information is hosted under a computer.

In this example, the Configuration Manager Connector Configuration management pack has two collections in the **DataProvider** and in the **DataConsumer** sections, one for importing the computers data and the second to import the BIOS data.

**Class Definition**

```

<ManagementPack xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" ContentReadable="true" SchemaVersion="1.1" OriginalSchemaVersion="1.1">
  <Manifest>
    <Identity>
      <ID>SampleBIOSMP</ID>
      <Version>1.0.0.0</Version>
    </Identity>
    <Name>BIOS Class MP</Name>
    <References>
      <Reference Alias="System">
        <ID>System.Library</ID>
        <Version>7.0.5229.0</Version>
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
      </Reference>
      <Reference Alias="Windows">
        <ID>Microsoft.Windows.Library</ID>
        <Version>7.0.5229.0</Version>
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
      </Reference>
    </References>
  </Manifest>
  <TypeDefinitions>
    <EntityTypes>
      <ClassTypes>
        <ClassType ID="HostedCustomClass" Accessibility="Public" Base="System!System.ConfigItem" Hosted="true" Abstract="false">
            <Property ID="SerialNumber" Type="string" Key="true"/>
        </ClassType>
      </ClassTypes>
      <RelationshipTypes>
        <RelationshipType ID="Microsoft.Windows.ComputerHostsBIOS" Accessibility="Public" Base="System!System.Hosting">
          <Source ID="Computer" Type="Windows!Microsoft.Windows.Computer" />
          <Target ID="BIOSClass" Type="HostedCustomClass" />
        </RelationshipType>      
      </RelationshipTypes>
    </EntityTypes>
  </TypeDefinitions>
</ManagementPack>
```

**Configuration Manager Connector Configuration management pack**

```
<ManagementPack xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" ContentReadable="true" SchemaVersion="1.1" OriginalSchemaVersion="1.1">
  <Manifest>
    <Identity>
      <ID>CnfgMgrBiosSample</ID>
      <Version>7.0.5229.0</Version>
    </Identity>
    <Name>CnfgMgrBiosSample</Name>
    <References>
      <Reference Alias="System">
        <ID>System.Library</ID>
        <Version>7.0.5229.0</Version>
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
      </Reference>
      <Reference Alias="LFX">
        <ID>ServiceManager.LinkingFramework.Library</ID>
        <Version>7.0.5229.0</Version>
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
      </Reference>
    </References>
  </Manifest>
  <Templates>
    <ObjectTemplate ID="DataProvider.Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms" TypeID="LFX!System.LinkingFramework.DataConnector.Projection">
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/DataConnectorName$">
          Microsoft_EnterpriseManagement_ServiceManager_Connector_Sms
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/IsProvider$">
          True
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/SolutionName$">SampleBIOS</Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/EntryPoint$">
          Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms.SmsConnector
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/EntryAssembly$">
          Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms,
          Version="7.0.5000.0",
          Culture=neutral,
          PublicKeyToken="31bf3856ad364e35"
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/WinFormUIAssembly$">
          Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms.SmsConnector,   
          Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms, Version="7.0.5000.0", Culture=neutral,
          PublicKeyToken="31bf3856ad364e35"
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/InstallSQLScripts$"></Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/DisableParallelProcess$">
          True
      </Property>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsTables' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataTable']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DataName$">SCCM_Ext.Sample_vex_R_System</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/StageTableName$">Sample_SMS_vex_R_System</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkField$">S.[rowversion]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkType$">1</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdField$">S.[ResourceID]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdSize$">2000</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/UseCache$">true</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/GroomType$">2</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/QueryString$"><![CDATA[
                            SELECT S.ResourceID,
                                S.ChangeAction as Lfx_Status,
                                S.Netbios_Name0,
                                S.Resource_Domain_OR_Workgr0
                            FROM SCCM_Ext.vex_R_System S
                            INNER JOIN SCCM_Ext.vex_FullCollectionMembership CM
                                ON S.ResourceID = CM.ResourceID
                            INNER JOIN SCCM_Ext.vex_Collection C
                                ON C.CollectionID = CM.CollectionID
                            WHERE ((S.ChangeAction = 'U' AND S.Client_Type0 != 3 AND S.Hardware_ID0 IS NOT NULL)
                                  OR S.ChangeAction = 'D')
                                  AND $COLLECTIONLIST
                            ORDER BY S.rowversion
                   ]]>
</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/CollectionName$">BIOSComputers</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/PrimaryKeyName$">[Sample_SMS_PK_v_R_SYSTEM]</Property>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[ResourceID]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">false</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyPosition$">0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyAcs$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">Netbios_Name0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">NVarChar</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Size$">64</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Collation$">DATABASE_DEFAULT</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">Resource_Domain_OR_Workgr0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">NVarChar</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Size$">255</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Collation$">DATABASE_DEFAULT</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsTables' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataTable']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DataName$">SCCM_Ext.Sample_vex_GS_COMPUTER_SYSTEM</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/StageTableName$">Sample_SMS_vex_GS_COMPUTER_SYSTEM</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkField$">CS.[rowversion]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkType$">1</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdField$">CS.[ResourceID]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdSize$">2000</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/UseCache$">true</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/GroomType$">2</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/QueryString$"><![CDATA[
                            SELECT CS.ResourceID,
                                    CS.GroupKey,
                                    CS.ChangeAction as Lfx_Status,
                                    CS.Name0,
                                    CS.Domain0
                            FROM SCCM_Ext.vex_GS_COMPUTER_SYSTEM CS
                            INNER JOIN SCCM_Ext.vex_FullCollectionMembership CM
                                ON CS.ResourceID = CM.ResourceID
                            INNER JOIN SCCM_Ext.vex_Collection C
                                ON C.CollectionID = CM.CollectionID  
                            WHERE $COLLECTIONLIST
                            ORDER BY CS.rowversion
                   ]]>
</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/CollectionName$">BIOSComputers</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/PrimaryKeyName$">[Sample_SMS_PK_v_GS_COMPUTER_SYSTEM]</Property>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[ResourceID]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">false</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyPosition$">0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyAcs$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[GroupKey]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">false</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyPosition$">1</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyAcs$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[Name0]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">NVarChar</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Size$">64</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Collation$">DATABASE_DEFAULT</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[Domain0]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">NVarChar</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Size$">32</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Collation$">DATABASE_DEFAULT</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsTables' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataTable']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DataName$">SCCM_Ext.vex_GS_PC_BIOS</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/StageTableName$">Sample_SMS_vex_GS_PC_BIOS</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkField$">S.[rowversion]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkType$">1</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdField$">S.[ResourceID]</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdSize$">2000</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/UseCache$">true</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/GroomType$">2</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/QueryString$"><![CDATA[
                      SELECT S.ChangeAction as Lfx_Status,
                      S.ResourceID,
                      S.BatchingKey,
                      S.GroupKey,
                      S.SerialNumber0
                      FROM SCCM_Ext.vex_GS_PC_BIOS S
                      INNER JOIN SCCM_Ext.vex_FullCollectionMembership CM
                        ON S.ResourceID = CM.ResourceID
                      INNER JOIN SCCM_Ext.vex_Collection C
                        ON C.CollectionID = CM.CollectionID
                      WHERE C.ChangeAction = 'U' AND CM.ChangeAction = 'U' AND $COLLECTIONLIST
                      ORDER BY S.rowversion
                   ]]>
        </Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/CollectionName$">Sample_SMS_PROVIDER_BIOS_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/PrimaryKeyName$">[Sample_SMS_PK_v_GS_BIOS1]</Property>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">[ResourceID]</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">false</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyPosition$">0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/PrimaryKeyAcs$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">BatchingKey</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">false</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">GroupKey</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">Int</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
        <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.TableEmbedsFields' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.Field']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Name$">SerialNumber0</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Type$">NVarChar</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Size$">34</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/Collation$">DATABASE_DEFAULT</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.Field']/AllowNull$">true</Property>
        </Object>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsCollections' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataCollection']$">
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataCollectionName$">BIOSComputers</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/StagingName$">DefaultCache</Property>
          <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataTables$">SCCM_Ext.Sample_vex_R_System,SCCM_Ext.Sample_vex_GS_COMPUTER_SYSTEM</Property>
      </Object>
      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsCollections' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataCollection']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataCollectionName$">Sample_SMS_PROVIDER_BIOS_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/StagingName$">DefaultCache</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataTables$">SCCM_Ext.vex_GS_PC_BIOS</Property>
      </Object>
    </ObjectTemplate>

    <ObjectTemplate ID="DataConsumer.Microsoft.EnterpriseManagement.ServiceManager.Connector.Sms" TypeID="LFX!System.LinkingFramework.DataConnector.Projection">
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/DataConnectorName$">
          MomStore
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/IsProvider$">
          False
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/SolutionName$">SampleBIOS</Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/EntryPoint$">
  Microsoft.EnterpriseManagement.ServiceManager.Linking.Consumer.OperationalStore.OperationalStoreConsumer
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/EntryAssembly$">
  Microsoft.EnterpriseManagement.ServiceManager.Linking.Consumer.OperationalStore,
  Version="7.0.5000.0",
  Culture=neutral,
  PublicKeyToken="31bf3856ad364e35"
      </Property>
      <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/InstallSQLScripts$"><![CDATA[
                        <Script>
                             if not object_id('[LFXSTG].[v_Sample_SMS_BIOSComputer]') is null
                                drop view [LFXSTG].[v_Sample_SMS_BIOSComputer];
                             exec ('
                                CREATE VIEW [LFXSTG].[v_Sample_SMS_BIOSComputer] AS
                                    SELECT S.Lfx_RowId,
                                           S.Lfx_SourceID,
                                           S.Lfx_Timestamp,
                                           S.Lfx_Status,
                                           CS.Name0 AS ''DisplayName'',
                                           COALESCE(CS.Name0, S.Netbios_Name0)
                                    + ''.'' + COALESCE(CS.Domain0, S.Resource_Domain_OR_Workgr0) AS ''PrincipalName''
                                    FROM LFXSTG.Sample_SMS_vex_R_System S
                                    INNER JOIN LFXSTG.Sample_SMS_vex_GS_COMPUTER_SYSTEM CS
                                         ON S.ResourceID = CS.ResourceID AND S.Lfx_SourceId = CS.Lfx_SourceId
                                    WHERE S.Netbios_Name0 IS NOT NULL
                                        AND S.Resource_Domain_OR_Workgr0 IS NOT NULL
                                ');
                        </Script>

                        <Script>
                            if not object_id('[LFXSTG].[v_Sample_BIOS]') is null
                                drop view [LFXSTG].[v_Sample_BIOS]
                            exec ('
                                CREATE VIEW [LFXSTG].[v_Sample_BIOS] AS
                                    SELECT P.Lfx_RowId AS Lfx_RowId,
                                        P.Lfx_SourceId,
                                        P.Lfx_Timestamp AS Lfx_Timestamp,
                                        P.Lfx_Status as Lfx_Status,
                                        P.SerialNumber0 AS ''SerialNumber'',
                                        COALESCE(CS.Name0, S.Netbios_Name0) + ''.'' + COALESCE(CS.Domain0, S.Resource_Domain_OR_Workgr0) AS ''PrincipalName''
                                    FROM [LFXSTG].Sample_SMS_vex_GS_PC_BIOS P
                                    INNER JOIN [LFXSTG]. Sample_SMS_vex_R_System S
                                        ON P.ResourceID=S.ResourceID AND P.Lfx_SourceId = S.Lfx_SourceId
                                    INNER JOIN [LFXSTG]. Sample_SMS_vex_GS_COMPUTER_SYSTEM CS
                                        ON S.ResourceID=CS.ResourceID
                                           AND S.Lfx_SourceId = CS.Lfx_SourceId
                                ')
                        </Script>
                   ]]>
        </Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataConnector']/UninstallSQLScripts$"><![CDATA[
                       <Script>
                            if not object_id('[LFXSTG].[v_Sample_SMS_BIOSComputer]') is null
                                drop view [LFXSTG].[v_Sample_SMS_BIOSComputer];
               </Script>

                       <Script>
                            if not object_id('[LFXSTG].[v_Sample_BIOS]') IS NULL
                                drop view [LFXSTG].[v_Sample_BIOS];
               </Script>
                   ]]>
        </Property>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsTables' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataTable']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DataName$">Sample_SMS_Computer</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkField$">E.Lfx_Timestamp</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdField$">E.Lfx_RowId</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdSize$">500</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/UseCache$">false</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/QueryString$"><![CDATA[
                            SELECT * FROM [LFXSTG].v_Sample_SMS_BIOSComputer E
                    ]]>
        </Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/CollectionName$">Sample_SMS_Computers_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DependOnDataTable$">SCCM_Ext.Sample_vex_GS_COMPUTER_SYSTEM,SCCM_Ext.Sample_vex_R_System</Property>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsTables' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataTable']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DataName$">Sample_SMS_BIOS_CONSUMER_VIEW</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkField$">C.Lfx_Timestamp</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/WatermarkType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdField$">C.Lfx_RowId</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdType$">0</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/BatchIdSize$">500</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/UseCache$">False</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/QueryString$"><![CDATA[
                        select C.* from [LFXSTG].v_Sample_BIOS C
                   ]]>
        </Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/CollectionName$">Sample_SMS_BIOS_CONSUMER_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataTable']/DependOnDataTable$">SCCM_Ext.vex_GS_PC_BIOS, Sample_SMS_Computer</Property>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsCollections' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataCollection']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataCollectionName$">Sample_SMS_Computers_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataTables$">Sample_SMS_Computer</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/Settings$"><![CDATA[
<TypeName xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">Microsoft.Windows.Computer</TypeName>
<MPName xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">Microsoft.Windows.Library</MPName>
<MPVersion xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">7.0.5229.0</MPVersion>
<MPToken xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">31bf3856ad364e35</MPToken>
]]>
</Property>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsCollections' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataCollection']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataCollectionName$">Sample_SMS_BIOS_CONSUMER_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataTables$">Sample_SMS_BIOS_CONSUMER_VIEW</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/Settings$"><![CDATA[
<TypeName xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">HostedCustomClass</TypeName>
<MPName xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">SampleBIOSMP</MPName>
<MPVersion xmlns="https://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">1.0.0.0</MPVersion>
        ]]>
        </Property>
      </Object>
    </ObjectTemplate>
  </Templates>
</ManagementPack>
```

## Next steps

- Learn about how to [Import runbooks from Orchestrator](import-data-orch.md).
