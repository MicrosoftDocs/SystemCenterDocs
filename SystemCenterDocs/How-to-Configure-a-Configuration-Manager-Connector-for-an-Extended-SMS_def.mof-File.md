---
title: How to Configure a Configuration Manager Connector for an Extended SMS_def.mof File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26a8586b-a5f5-47a9-9bf8-626ef75d48eb
---
# How to Configure a Configuration Manager Connector for an Extended SMS_def.mof File
Service Manager hardware inventory collects and then provides system information, such as available disk space, processor type, and operating system, about each computer in the Configuration Manager hierarchy. In Configuration Manager, users can customize the default Configuration Manager SMS\_def.mof file to extend the hardware inventory information that is collected.

When you create a Configuration Manager connector in Service Manager, you can select the default System Center Configuration Manager Connector Configuration management pack that must be used for that connector. By using the default management pack, the connector imports hardware, software, and desired configuration management information for the computers that are in the system.

If the Configuration Manager SMS\_def.mof file has been extended to collect additional hardware inventory data, which you also want to import into Service Manager, you must create a new custom management pack that defines that additional data. Then, you have to create a new Configuration Manager connector and configure it to use the new custom management pack.

## Importing Extended Hardware Inventory Data from Configuration Manager
To import extended hardware inventory data from Configuration Manager, you must author a custom Configuration Manager connector management pack. There are two approaches to implementing a custom Configuration Manager connector:

-   Create a custom Configuration Manager connector management pack that defines the extended data that you want to import and then create two connectors. Configure one connector to use the default System Center Configuration Manager Connector Configuration management pack to import the data that is defined by default. Configure the second connector to use the custom management pack to import the additional extended data.

-   Customize the default System Center Configuration Manager Connector Configuration management pack to also include the additional extended data. Create a single connector that is configured to use the custom management pack to import all the information that you must have.

This topic provides the information that you must have to implement the first approach that is described earlier. It provides the details that you must have so that you can develop a custom Configuration Manager connector management pack that imports the extended hardware inventory from Configuration Manager.

The high\-level steps to importing extended hardware inventory data are as follows:

1.  Create a custom Configuration Manager Connector Configuration management pack with the definitions for the extended data.

2.  Import the custom management pack into Service Manager. After you import the management pack, Service Manager processes the directives in the management pack to create staging tables and to run any install Structured Query Language \(SQL\) scripts, as defined in the management pack.

3.  Create a Configuration Manager connector and configure it to use the custom management pack.

4.  The Configuration Manager connector imports the data.

### Working with a Custom Configurations Manager Connector Management Pack
Consider the following tips when you are working with a custom Configurations Manager Connector management pack:

-   Semantic errors in the connector configuration templates in the management pack do not prevent the management pack from being imported, and they are logged to the event log. In this case, you must delete the management pack, correct the errors, and reimport the management pack.

-   After creating a Configuration Manager connector, you cannot modify its management pack selection. Instead, you must delete that connector and then create a new one with the desired management pack selection.

-   To ensure a successful deletion of a management pack, you must delete any connectors that are configured to use the management pack that you want to delete and then delete the management pack.

    When you delete a custom Configurations Manager Connector management pack, Service Managerr tries to delete all related staging tables that were created during the management pack import. Then, Service Manager runs any scripts that are defined in the **Uninstall** section of the management pack.

-   Unlike other management packs, the custom Configuration Manager Connector management pack cannot be versioned. Importing a later version of the management pack will succeed. However, the connector configuration in the management pack will be ignored, or it might cause validation errors that are logged to the event log.

## Creating a Custom Configuration Manager Connector Configuration Management Pack
A custom Configuration Manager Connector Configuration management pack is similar in structure to the default Configuration Manager Connector management pack. It must contain the two object templates **DataProvider** and **DataConsumer** that specify how the data should be imported and applied.

### DataProvider Section
The **DataProvider** section provides information, such as which data to import, that you must have when you are importing data from Configuration Manager into the staging tables of **LinkingFramework**. The **DataProvider** section includes the queries that run on the Configuration Manager site database; directives for staging table creation; custom SQL scripts; and information that is relevant for incremental synchronization, such as watermarking and batching.

### DataConsumer Section
The **DataConsumer** section provides information about reading the data from staging tables and writing it to the **ServiceManager** database’s instances space, such as **Entities** or **Relationships**. The **DataConsumer** section includes queries that run on the staging tables; mapping to the Service Manager type system; custom SQL scripts; and information that is relevant for incremental synchronization, such as watermarking and batching.

### Structure of the DataProvider and DataConsumer Object Templates Sections
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

## Properties in the Custom Management Pack
The following table provides the details about each property in the custom Configuration Manager Connector Configuration management pack. Use these guidelines when you create the custom management pack.

|Property|Expected value|Validation after import|
|------------|------------------|---------------------------|
|ID|For both **DataProvider** and **DataConsumer** templates—as indicated in the sample|Yes|
|**DataConnector Properties**|||
|DataConnectorName|For both **DataProvider** and **DataConsumer** templates—identical to the values in the sample|Yes|
|IsProvider|In **DataProvider** template—True<br /><br />In **DataConsumer** template—False|Yes|
|SolutionName|A comment. For example, it can indicate the type of the imported data.|An attempt to import a management pack in which the solution name is already being used; it causes an error that is logged to the event log.|
|Entrypoint, EntryAssembly & WinformUIAssembly|Identical to the value in the sample||
|InstallSQLScripts section|SQL scripts that must run after the staging tables are set up. They are usually used in the **DataConsumer** template to configure views that display data from the staging tables.<br /><br />Everything that is enclosed between the \<Script\><\/Script> tags is expected to be valid SQL script. Therefore, for comments, you must use the ‘\/\*’ and the ‘\*\/’ multi\-line comment delimiters instead of the standard XML comment tags.|Not validated. Use custom table names to ensure that this does not cause overwriting or changing any tables except the ones that are declared in the management pack.|
|UnInstallSQLScripts section|SQL scripts that must run after you delete the Configuration Manager Connector management pack in the [!INCLUDE[smcons](../Token/smcons_md.md)].<br /><br />Everything that is enclosed between the \<Script\><\/Script> tags is expected to be valid SQL script. Therefore, for comments, you must use the ‘\/\*’ and the ‘\*\/’ multi\-line comment delimiters instead of the standard XML comment tags.|Not validated. Use custom table names to ensure that this does not cause overwriting or changing any tables except the tables that are declared in the management pack.|
|DisableParallelProcessing|True||
|**DataTable Properties**|||
|DataName|The table from which to import data. It is used in the user interface \(UI\) and not used in queries.||
|StageTableName|The name of the staging table. It must be unique.|An attempt to import a management pack, in which the table name is already being used, causes an error to be logged to the event log.|
|WatermarkField|The name of the **rowversion** column||
|WatermarkType|Possible values are:<br /><br />-   0—Indicates **DateTime** type<br />-   1—Indicates the **Timestamp** type<br />-   \(\-1\)—Indicates no watermarking, in which case **WatermarkField** becomes optional|Other types of watermarking are not supported.|
|BatchIdField|The name of the column that has good selectivity; used to separate incremental data into batches when importing to staging tables||
|BatchIdType|Possible values are:<br /><br />-   0—Int<br />-   \(\-1\)—No batching, in which case **BatchIdField** becomes optional|Integer column|
|BatchIdSize|The size of the batch, if batching is used. A high number indicates that much data is being read or written at the same time. The recommended value is 500.|Integer column|
|UseCache|True||
|GroomType|Possible values are:<br /><br />-   1—The data in staging tables can be groomed after it is transferred to the Service Manager database.<br />-   2—The data in staging tables is groomed only after it is marked as deleted in the Configuration Manager database and has also been deleted in the [!INCLUDE[smshort](../Token/smshort_md.md)] database because of the [!INCLUDE[smshort](../Token/smshort_md.md)] connector synchronization.||
|QueryString|The actual query that [!INCLUDE[sccmshortname](../Token/sccmshortname_md.md)] uses to retrieve the requested data. The query must be of the form:<br /><br />`SELECT …`<br /><br />`FROM …`<br /><br />`WHERE …`<br /><br />`ORDER BY …`<br /><br />The WHERE clause can contain the “$COLLECTIONLIST” token. During synchronization, this token is replaced by the collections that are specified in the System Center Configuration Manager Connector Wizard.<br /><br />The data that is exposed by Configuration Manager SCCM\_Ext.\* views is supported for import. This data can be extended by using standard sms\_def.mof extensions or by using noidmifs. Other tables are not supported.<br /><br />Notably, subqueries are not supported, but joins to other tables are supported.|Not validated. All queries have an Lfx\_Status column with value “U” or “D,” indicating whether the row represents an Update or a Delete operation.|
|CollectionName|A name for a group of data tables; this name must be unique. Tables in the same collection cannot depend on each other.|An attempt to import a management pack, in which the collection name is already being used, causes an error to be logged to the event log.|
|PrimaryKeyName|A section that declares the unique primary key name for the staging table.|An attempt to import a management pack, in which the key name is already being used, causes an error to be logged to the event log.|
|DependOnDataTable|The name or names of **DataTable** that must be synchronized first before this one. Typically, this is used to synchronize the staging table before the system reads it in the Consumer view.<br /><br />If you are using multiple collections, dependency should be expressed only between tables in different collections.|Not validated|
|**DataField Properties**|||
|Name, Type, AllowNull|These are required fields for any column type. Supported types are **int**, **nvarchar**, **datetime** and **xml**.|Not validated|
|PrimaryKeyACs, PrimaryKeyPosition|If part of primary key, indicates the position from the left in the primary key. Lfx adds two internal use columns \(Lfx\_Status, Lfx\_SourceId\) to the PK at the end.||
|Collation|DATABASE\_DEFAULT|Not validated|
|**DataCollection Properties**|||
|DataCollectionName|Must be identical to what is referenced by a **DataTable** property|An attempt to import a management pack, in which the collection name is already being used, causes an error to be logged to the event log.|
|StagingName|In DataProvider template—DefaultCache<br /><br />In DataConsumer template—Not present|Not validated|
|DataTables|Comma\-separated value \(CSV\) list of tables referencing this collection||
|Settings|In **DataProvider** template—Not present<br /><br />In **DataConsumer** template—Indicates type mapping|Escaped XML with following syntax:<br /><br />`<TypeName>Microsoft.Windows.Computer</TypeName>`<br /><br />`<MPName>Microsoft.Windows.Library</MPName>`<br /><br />`<MPVersion>version of MP</MPVersion>`<br /><br />`<MPToken>token for MP</MPToken>`|

## Sample of Custom Configuration Manager Connector Configuration Management Packs
The following are schema definitions and Configuration Manager Connector management pack samples that import data from the Configuration Manager SCCM\_Ext.vex\_GS\_PC\_BIOS view.

Refer to the table earlier in this topic for more information about the properties of these management packs. Use an XML editor, such as the editor in Microsoft Visual Studio, to modify these samples to fit your import scenarios.

### Importing Data from a Hosted Class
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
<TypeName xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">Microsoft.Windows.Computer</TypeName>
<MPName xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">Microsoft.Windows.Library</MPName>
<MPVersion xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">7.0.5229.0</MPVersion>
<MPToken xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">31bf3856ad364e35</MPToken>
]]>
</Property>
      </Object>

      <Object Path="$Context/Path[Relationship='LFX!System.LinkingFramework.ConnectorEmbedsCollections' SeedRole='Source' TypeConstraint='LFX!System.LinkingFramework.DataCollection']$">
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataCollectionName$">Sample_SMS_BIOS_CONSUMER_COLLECTION</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/DataTables$">Sample_SMS_BIOS_CONSUMER_VIEW</Property>
        <Property Path="$Context/Property[Type='LFX!System.LinkingFramework.DataCollection']/Settings$"><![CDATA[
<TypeName xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">HostedCustomClass</TypeName>
<MPName xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">SampleBIOSMP</MPName>
<MPVersion xmlns="http://schemas.microsoft.com/sdm/servicedesk/linking/2005/09">1.0.0.0</MPVersion>
        ]]>
        </Property>
      </Object>
    </ObjectTemplate>
  </Templates>
</ManagementPack>
```

