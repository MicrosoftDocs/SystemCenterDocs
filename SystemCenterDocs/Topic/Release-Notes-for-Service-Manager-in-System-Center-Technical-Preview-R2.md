---
title: Release Notes for Service Manager in System Center Technical Preview R2
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f131fe4-d13a-4139-850d-de53b602c491
robots: noindex,nofollow
---
# Release Notes for Service Manager in System Center Technical Preview R2
Before you install and use [!INCLUDE[smshort12](../Token/smshort12_md.md)] in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], read these release notes.

## Known Issues

## [!INCLUDE[smcons](../Token/smcons_md.md)] Installed on a VMM Server Causes VMM Connector Failure
**Description:** If the [!INCLUDE[smcons](../Token/smcons_md.md)] is installed on the same server as VMM, then you cannot use that [!INCLUDE[smcons](../Token/smcons_md.md)] to create a VMM connector to that VMM server.

**Workaround:** None, however you can use a different [!INCLUDE[smcons](../Token/smcons_md.md)] to create the VMM connector.

## Data Warehouse stops working after upgrading Service Manager
**Description:** The Data Warehouse stops working after upgrading Service Manager in System Center 2012 SP1 to System Center 2012 R2 due to a Data Warehouse fact entity upgrade.

**Workaround:** To prevent this issue from occurring again, run the following SQL script for each of the following data warehouse databases: DW Repository, DW DataMart, CM DataMart, and OM DataMart. If this workaround is applied after data warehouse upgrade, resume the failed management pack upgrade process deploy captured in the list of Data Warehouse Management Packs from the Service Manager console.

```
IF OBJECT_ID('tempdb..#PKFixQueries') IS NOT NULL
    DROP TABLE #PKFixQueries

;WITH FactName
AS (
        SELECT  w.WarehouseEntityName
        FROM    etl.WarehouseEntity w
        JOIN    etl.WarehouseEntityType t ON w.WarehouseEntityTypeId = t.WarehouseEntityTypeId
        WHERE   t.WarehouseEntityTypeName = 'Fact'
),FactList
AS (
    SELECT  PartitionName, p.WarehouseEntityName
    FROM    etl.TablePartition p
    JOIN    FactName f ON p.WarehouseEntityName = f.WarehouseEntityName
)
, FactWithPK
AS (
    SELECT  f.WarehouseEntityName, f.PartitionName, b.CONSTRAINT_NAME, a.COLUMN_NAME
    FROM    FactList f
    JOIN    INFORMATION_SCHEMA.KEY_COLUMN_USAGE a ON f.PartitionName = a.TABLE_NAME
    JOIN    INFORMATION_SCHEMA.TABLE_CONSTRAINTS b ON a.CONSTRAINT_NAME = b.CONSTRAINT_NAME AND b.CONSTRAINT_TYPE = 'Primary key'
)
, FactWithDefaultOrNoPK
AS (
    SELECT  DISTINCT f.WarehouseEntityName, f.PartitionName
            , 'PK_' + f.WarehouseEntityName AS DefaultPKConstraint
            , 'PK_' + f.PartitionName AS NewPKConstraint
    FROM    FactList f
    LEFT JOIN    FactWithPK pkf ON pkf.WarehouseEntityName = f.WarehouseEntityName AND pkf.PartitionName = f.PartitionName
    WHERE   pkf.WarehouseEntityName IS NULL OR pkf.CONSTRAINT_NAME = 'PK_' + f.WarehouseEntityName
)
, FactPKList
AS (
    SELECT  DISTINCT f.WarehouseEntityName, f.COLUMN_NAME
    FROM    FactWithPK f
)
, FactPKListStr
AS (
    SELECT  DISTINCT f1.WarehouseEntityName, F.COLUMN_NAME AS PKList
    FROM    FactPKList f1
    CROSS APPLY (
                    SELECT  '[' + COLUMN_NAME + '],'
                    FROM    FactPKList f2
                    WHERE   f2.WarehouseEntityName = f1.WarehouseEntityName
                    ORDER BY COLUMN_NAME
                    FOR XML PATH('')
                ) AS F (COLUMN_NAME)
)
SELECT  f.PartitionName,
        '----------------------------- [' + f.PartitionName + '] -----------------------------' + CHAR(13) +
        'IF OBJECT_ID(''[' + f.DefaultPKConstraint + ']'') IS NOT NULL' + CHAR(13) +
        'BEGIN' + CHAR(13) +
        '  ALTER TABLE [dbo].[' + f.PartitionName + '] DROP CONSTRAINT [' + f.DefaultPKConstraint + ']' + CHAR(13) +
        'END' + CHAR(13) + CHAR(13) +
        'IF OBJECT_ID(''[' + f.NewPKConstraint + ']'') IS NULL' + CHAR(13) +
        'BEGIN' + CHAR(13) +
        '  ALTER TABLE [dbo].[' + f.PartitionName + '] ADD CONSTRAINT [' + f.NewPKConstraint + '] PRIMARY KEY NONCLUSTERED (' + SUBSTRING(pk.PKList, 1, LEN(pk.PKList) -1) + ')' + CHAR(13) +
        'END' AS Query
INTO    #PKFixQueries
FROM    FactWithDefaultOrNoPK f
JOIN    FactPKListStr pk ON pk.WarehouseEntityName = f.WarehouseEntityName

DECLARE @PartitionName NVARCHAR(MAX), @Query NVARCHAR(MAX)
WHILE EXISTS (SELECT 1 FROM #PKFixQueries)
BEGIN
    SELECT  TOP 1
            @PartitionName = PartitionName,
            @Query = Query
    FROM    #PKFixQueries

    PRINT   @Query
    EXEC(@Query)

    DELETE  #PKFixQueries
    WHERE   PartitionName = @PartitionName
END
```

## Installing chargeback report files on the Service Manager management server might fail after upgrade
**Description:** When installing chargeback report files on the Service Manager management server after upgrading Service Manager in System Center 2012 SP1 to System Center 2012 R2, you may receive an error message. This occurs because files are not able to be imported from Operations Manager.

**Workaround:** If this issue affects you, complete the following procedure and try to use chargeback again:

#### To prepare for chargeback

1.  On the server running [!INCLUDE[scvm_threshold_1](../Token/scvm_threshold_1_md.md)], copy the following management packs from their installed location, by default *InstallationDrive*:\\Program Files\\Microsoft System Center 2012 R2\\Virtual Machine Manager\\ManagementPacks to a folder on the server running the [!INCLUDE[smshort12](../Token/smshort12_md.md)] management server.

    -   Microsoft.SystemCenter.VirtualMachineManager.PRO.Library

    -   Microsoft.SystemCenter.VirtualMachineManager.PRO.V2.Library

    -   Microsoft.SystemCenter.VirtualMachineManager.Pro.2008.Library

    -   Microsoft.SystemCenter.VirtualMachineManager.Library

    -   Microsoft.SystemCenter.VirtualMachineManager.2012.Discovery

2.  Start the [!INCLUDE[smcons](../Token/smcons_md.md)] and navigate to **Administration**, **Management Packs**.

3.  **Import** the management packs that you copied to the [!INCLUDE[smshort12](../Token/smshort12_md.md)] management server. Make sure to click **Yes** on the **Online Data Connection** dialog box.

## Service Manager Requires a Hotfix
**Description:** Service Manager might stop unexpectedly unless you apply a Hotfix which is available at Microsoft Support.

**Workaround:** Apply Hotfix [2600907](http://go.microsoft.com/fwlink/p/?LinkId=230954).

## [!INCLUDE[smssp](../Token/smssp_md.md)] Installation
**Description:** For [!INCLUDE[smshort12](../Token/smshort12_md.md)] in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], you must install the [!INCLUDE[smssp](../Token/smssp_md.md)] on a server that does not host a [!INCLUDE[smshort12](../Token/smshort12_md.md)] role.

**Workaround:** None.

## [!INCLUDE[smshort12](../Token/smshort12_md.md)] Requires SQL Server 2008 R2 SP1 or Later
**Description:** The [!INCLUDE[smshort12](../Token/smshort12_md.md)] prerequisite checker included in Setup does not check for SQL Server 2008 R2 SP1, however it is required. If you are running the RTM version of SQL Server 2008 R2, then you must upgrade it to SQL Server 2008 R2 SP1 or later before you can install [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)].

**Workaround:** None.

## Data Warehouse Setup Might Fail if the Database or Log Path Includes a Single Quotation Mark Character
**Description:** During Setup, if you specify a database or log path that includes a single quotation mark character \('\), Setup might fail.

**Workaround:** None. The path that you specify cannot include a single quotation mark character.

## Setup Might Fail if the Service Manager 2010 Authoring Tool Has Been Installed
**Description:** Setup might fail if you have previously installed any version of the Service Manager 2010 Authoring Tool.

**Workaround:** Remove the Service Manager 2010 Authoring Tool, and then retry Setup.

## Setup Does Not Install the Report Viewer Language Pack
**Description:** Setup includes a prerequisite checker that checks for and—if necessary, installs—the Microsoft Report Viewer. However, Setup does not install the Report Viewer Language Pack, which makes the Microsoft Report Viewer compatible with Windows operating systems that are configured to use languages other than English.

**Workaround:** If your system is configured to use a language other than English, you should manually install the Report Viewer Language Pack for that language. You can download the [Microsoft Report Viewer Redistributable 2008 SP1 Language Pack](http://go.microsoft.com/fwlink/p/?LinkID=191491) from the Microsoft Download Center.

## Service Manager Setup Fails if a SQL Server Instance Contains a $ Character
**Description:** If you attempt to install Service Manager using a named Structured Query Language \(SQL\) instance that contains a dollar sign \($\) character, Setup fails.

**Workaround:** Use a SQL instance that does not contain the $ character in its name.

## Orchestrator Connector Account Password Cannot Contain $ Characters
**Description:** If the Orchestrator connector account password contains a $ character, the sync job completes, however runbooks are not updated in the Service Manager database.

**Workaround:** If your Orchestrator connector account password contains a $ character, change the password to one that does not include the $ character.

## Registering an Operations Manager 2007 R2 Data Source Fails
**Description:** When you attempt to register an Operations Manager 2007 R2 data source in the Data Warehouse workspace, registration fails and an error appears stating that `The Data Access service is either not running or not yet initialized. Check the event log for more information`.

**Workaround:** None. This is a known problem when you try to register an Operations Manager 2007 R2 data source with [!INCLUDE[smshort12](../Token/smshort12_md.md)] in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)].

## Information Linked from Setup Might Not Display Localized Content
**Description:** Information that is linked from Setup to the Setup log and to technical documentation might not display localized content. Setup logs in [!INCLUDE[smshort12](../Token/smshort12_md.md)] are available in English only. Technical documentation is available in a variety of localized languages. Where available, localized technical documentation is displayed on TechNet; however, not all languages are available.

**Workaround:** None.

## Full Text Search Does Not Work for Some Turkish Language Characters
**Description:** Full text search in the [!INCLUDE[smssp](../Token/smssp_md.md)] works only if you have a licensed non\-Microsoft word breaker installed. However, full text search does not work for some characters of the Turkish language even if you have a licensed non\-Microsoft Turkish word breaker installed.

**Workaround:** Load a licensed non\-Microsoft word breaker that enables full\-text search to function. For more information, see the following links for the version of SQL Server that you are using:

-   [SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=205800) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=205800\)

-   [SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=205557) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=205557\).

## Unassigned Virtual Machines Appear in Reporting Information
**Description:** All virtual machines appear in Microsoft Online Analytical Processing \(OLAP\) cube data and the sample Microsoft Excel report, regardless of whether a virtual machine is assigned to a cloud. Reporting information is designed to show unassigned virtual machines as rows without price sheet data.

**Workaround:** None.

## Virtual Machine Component Aggregation Is Misleading
**Description:** The SystemCenterVmmCloudChargebackCube OLAP cube contains aggregated values for virtual machine components. However, values for the components should not be expressed in the cube using any manner other than a daily count.

**Workaround:** None. However, you should ignore any aggregated time values for virtual machine components other than daily values.

## Reassigned Virtual Machine Values Might Be Erroneously Calculated
**Description:** When you remove and then reassign a virtual machine from one cloud object to another, erroneous calculated values might appear for both clouds where the virtual machine was assigned. This condition might occur only for the same date when values for the virtual machine are not removed from the cloud that the virtual machine was initially assigned to. Data for the next day is accurate.

**Workaround:** None.

## Values in Price Sheets Are Effective Starting on the Next Day
**Description:** When you type a value in a price sheet, the value becomes effective on the following day. For example, if you modify a calculated price today, the updated price will not immediately appear in OLAP cube data or the sample chargeback Excel report. Instead, the old price continues to appear in OLAP cube data and the sample chargeback Excel report. This behavior is expected; you can use it to update prices throughout your business day without the prices going into effect until the next business day.

**Workaround:** None.

## After the Display Language Is Changed, the Wizard Text Might Display an Incorrect Language
**Description:** After you change the display language using the **Language** menu in the Service Manager console, wizard text might be displayed in your previously selected language.

**Workaround:** If this problem affects you, do the following:

1.  Close the Service Manager console.

2.  On the **Start** menu, click **Run**, type **%temp%**, and then click **OK**.

3.  Navigate up to the parent LOCAL folder.

4.  Open \\Microsoft\\System Center Service Manager 2010\\<ServerName>\\<VersionNumber>\\, and then delete the contents of the folder.

5.  Open the Service Manager console. The wizard text should appear in the language that you selected previously.

## Errors Might Occur When You Modify or Delete Service Request Template Items
**Description:** When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround:** When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.

## The Service Manager Console Stops When You Attempt to Open a Change Request if the SelectedDate Value Is Not Valid
**Description:** This problem can occur after upgrading from [!INCLUDE[scvm_threshold_1](../Token/scvm_threshold_1_md.md)] to Service Manager in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)] if a change request’s scheduled end is set before the scheduled start date. The error message might resemble `System.ArgumentOutOfRangeException: SelectedDate value is not valid`.

**Workaround:** To display the change request containing a ScheduledStartDate value that is greater than the ScheduledEndDate value, you can use the following sets of commands in a Service Manager module for Windows PowerShell window:

```
$class=get-scclass -Name System.WorkItem.ChangeRequest
```

```
$instances= get-scclassinstance $class | where {$_.ScheduledStartDate -gt
```

```
$_.ScheduledEndDate}
```

```
$instances | Select DisplayName, ScheduledStartDate, ScheduledEndDate
```

To correct the situation, run the following set of cmdlets. These cmdlets set the **ScheduledEndDate** value to the same value as **ScheduledStartDate**.

```
$class=get-scclass -Name System.WorkItem.ChangeRequest
```

```
$instances= get-scclassinstance $class | where {$_.ScheduledStartDate -gt
```

```
$_.ScheduledEndDate}
```

```
$instances | Select DisplayName, ScheduledStartDate, ScheduledEndDate
```

```
$instances | %{ $_.ScheduledEndDate = $_.ScheduledStartDate ; $_ } | update-scclassinstance
```

## Double\-Byte Characters Might Not Display Correctly if a Knowledge Article Is Created from a TXT File
**Description:** If you create a knowledge article using a TXT file that contains double\-byte characters, the characters might not display correctly.

**Workaround:** If this problem affects you, do not use TXT files to create knowledge articles. Instead, use RTF files.

## Shortcut Keys Have Limited Functionality
**Description:** Most shortcut keys do not work properly.

**Workaround:** If a particular shortcut key does not work, on the **Tasks** menu, click **Tasks**, and then try the shortcut key.

## Analyze Cube in Excel Does Not Work with Excel Viewer
**Description:** If you attempt to analyze an OLAP data cube in the Data Warehouse workspace using Microsoft Office Excel Viewer, a dialog box appears, stating erroneously that you can install Microsoft Excel viewer and try again.

**Workaround:** Close the [!INCLUDE[smcons](../Token/smcons_md.md)], install Microsoft Excel, and then try again.

## Configuring the Reporting Server Might Take a Long Time
**Description:** When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround:** None.

## Double\-Byte Characters Are Sent Incorrectly to Search Provider
**Description:** When you perform a knowledge search and you type double\-byte characters in the **Search Provider** box, they are not sent correctly to the search website. Instead, erroneous characters are sent.

**Workaround:** None.

## Data Binding Does Not Work for Class Extension Properties
**Description:** The value for an extended property is not saved when a form control is bound to an extended property on a class.

**Workaround:** Restart the [!INCLUDE[smcons](../Token/smcons_md.md)] after binding to a property.

## Sorting Knowledge Articles by Date Does Not Work
**Description:** When you try to sort knowledge articles by date, sorting does not work.

**Workaround:** None.

## The System Center Alert Management Cube Management Pack Is Not Imported During Operations Manager Registration
**Description:** When you register Operations Manager as a data source, the System Center Alert Management Cube management pack will not be imported.

**Workaround:** First, create a data source for Operations Manager. For more information, see [How to Register the System Center Data Warehouse to Operations Manager](http://technet.microsoft.com/library/hh542405.aspx) in the Service Manager Administrator's Guide.

Next, make sure that the System Center Data Warehouse Operations Manager management pack has been imported. In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Data Warehouse**, click **Management Packs**, and confirm that **System Center Datawarehouse Operations Manager Library** is listed.

Finally, on the Data Warehouse Management Server, type the following Windows PowerShell commands to manually import the management pack. \(This example assumes that Service Manager is on drive C and that you installed Service Manager using the default path\).

```
cd 'C:\Program Files\Microsoft System Center\Service Manager 2012 R2\PowerShell'
Import-Module .\System.Center.Service.Manager.psd1
Import-SCSMManagementPack ..\AlertCube.mpb
```

