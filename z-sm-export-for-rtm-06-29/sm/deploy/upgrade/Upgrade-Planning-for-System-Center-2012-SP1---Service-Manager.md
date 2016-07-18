---
title: Upgrade Planning for System Center 2012 SP1 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cad46180-3c12-4eb2-a4bc-99fd88d2f3e7
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
# Upgrade Planning for System Center 2012 SP1 - Service Manager
This guide outlines the procedures necessary to upgrade to [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)].  
  
 An in\-place upgrade from [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 is supported. An in\-place upgrade is an upgrade of all [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] parts on the same hardware. Other approaches, such as side\-by\-side upgrades or rolling upgrades, are not supported.  
  
 Upgrading to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 requires preparation. We recommend that you install [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in a lab environment and then replicate your production databases into the lab. You then perform an upgrade of the new installation in the lab, and once that has proven successful, perform the same upgrade to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 in the production environment.  
  
## Evaluation and Select Versions  
 The release of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] was available in two different versions:  
  
-   Evaluation version \(180\-day time\-out\)  
  
-   Select license version  
  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 is available as an Evaluation version \(180\-day time\-out\) or Select License edition. The following upgrade paths are supported to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1.  
  
|Current Version|Upgraded Version|Status|  
|---------------------|----------------------|------------|  
|[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] Eval|[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 Eval|Evaluation period remains unchanged|  
|[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] Select|[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 Select|Licensed|  
  
> [!NOTE]  
>  Upgrading from an evaluation version of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] to an evaluation version of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 *does not* extend the 180\-day evaluation period.  
  
## Installation Location  
 The default folder for installing [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 is \\Program Files\\Microsoft System Center\\Service Manager 2012. However, when you perform the upgrade to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1, the software is installed in the folder that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] previously used. If Service Manager 2010 was previously upgraded to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], then the following folder might be used:  
  
 \\Program Files\\Microsoft System Center\\Service Manager 2010.  
  
## Language Support  
 This release of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 represents an ongoing progression of support for various languages. In [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)], you used the Latin1\_General\_100\_CI\_AS collation for the Turkish language. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SP1 supports the Turkish\_100\_CI\_AS collation. However, if you upgraded from [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the collation that was used for the Turkish language \(Latin1\_General\_100\_CI\_AS\) would have been carried forward to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], and will be when you upgrade to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1.  
  
## Hardware Requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1  
 [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 will function on the same hardware that you used for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
 All hardware requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 are fully documented in [Hardware Requirements for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=253556).  
  
## Software Requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1  
 To upgrade to [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)] SP1, you must first apply Cumulative Update 2 for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
 [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 has the same software requirements for the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] that [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] does, except for the new requirement of Microsoft SQL Server 2012 Analysis Management Objects \(AMO\). Microsoft SQL Server 2012 AMO is supported on SQL Server 2008 and SQL Server 2012. In addition, the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] can now be installed on computers running [!INCLUDE[win8_client_2](../../../sm/deploy/upgrade/includes/win8_client_2_md.md)] and [!INCLUDE[win8_server_2](../../../sm/deploy/upgrade/includes/win8_server_2_md.md)].  
  
 The Service Manager and data warehouse management servers, along with the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], is supported with [!INCLUDE[win8_server_2](../../../sm/deploy/upgrade/includes/win8_server_2_md.md)].  
  
 All software requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 are fully documented in [Software Requirements for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=252844).  
  
## Preventing MPSync Jobs From Failing  
 **Before Upgrade**  
  
 **Description:** A problem with the upgrade process causes MPSync job to fail after the upgrade is complete. To prevent this problem from occurring before you upgrade, you must run the SQL script below on the DWRepository database to get the actual SQL scripts that drop and add a constraint on the primary key in fact tables in the DWRepository database to correct the problem. Additionally, transform and load jobs might also fail. This error can occur because of erroneous database grooming.  
  
```  
;WITH FactName  
AS (  
       select w.WarehouseEntityName from etl.WarehouseEntity w  
       join etl.WarehouseEntityType t on w.WarehouseEntityTypeId = t.WarehouseEntityTypeId  
       where t.WarehouseEntityTypeName = 'Fact'  
),FactList  
AS (  
    SELECT  PartitionName, p.WarehouseEntityName,  
            RANK() OVER ( PARTITION BY p.WarehouseEntityName ORDER BY PartitionName ASC ) AS RK  
    FROM    etl.TablePartition p  
       join FactName f on p.WarehouseEntityName = f.WarehouseEntityName  
)  
, FactPKList  
AS (  
    SELECT  f.WarehouseEntityName, a.TABLE_NAME, a.COLUMN_NAME, b.CONSTRAINT_NAME, f.RK,  
            CASE WHEN b.CONSTRAINT_NAME = 'PK_' + f.WarehouseEntityName THEN 1 ELSE 0 END AS DefaultConstraints  
    FROM    FactList f  
    JOIN    INFORMATION_SCHEMA.KEY_COLUMN_USAGE a ON f.PartitionName = a.TABLE_NAME  
    JOIN    INFORMATION_SCHEMA.TABLE_CONSTRAINTS b ON a.CONSTRAINT_NAME = b.CONSTRAINT_NAME AND b.CONSTRAINT_TYPE = 'Primary key'  
)  
, FactWithoutDefaultConstraints  
AS (  
    SELECT  a.*  
    FROM    FactPKList a  
    LEFT JOIN FactPKList b ON b.WarehouseEntityName = a.WarehouseEntityName AND b.DefaultConstraints = 1  
    WHERE   b.WarehouseEntityName IS NULL AND a.RK = 1  
)  
, FactPKListStr  
AS (  
    SELECT  DISTINCT f1.WarehouseEntityName, f1.TABLE_NAME, f1.CONSTRAINT_NAME, F.COLUMN_NAME AS PKList  
    FROM    FactWithoutDefaultConstraints f1  
    CROSS APPLY (  
                    SELECT  '[' + COLUMN_NAME + '],'  
                    FROM    FactWithoutDefaultConstraints f2  
                    WHERE   f2.TABLE_NAME = f1.TABLE_NAME  
                    ORDER BY COLUMN_NAME  
                FOR  
                   XML PATH('')  
                ) AS F (COLUMN_NAME)  
)  
SELECT  'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] DROP CONSTRAINT [' + f.CONSTRAINT_NAME + ']' + CHAR(13) + CHAR(10) +  
        'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] ADD CONSTRAINT [PK_' + f.WarehouseEntityName + '] PRIMARY KEY NONCLUSTERED (' + SUBSTRING(f.PKList, 1, LEN(f.PKList) -1) + ')' + CHAR(13) + CHAR(10)  
FROM    FactPKListStr f  
  
```  
  
 **Workaround 1:** If you have already upgraded and you do not have problems with transform or load job failures but do have a management pack deployment failure, then follow the steps in the Before Upgrade section. In addition, after the default primary keys have been restored, restart the failed management pack deployment in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] by navigating to the Data Warehouse workspace and then select Management Pack.  
  
 **Workaround 2:** If you have upgraded and you have problems with transform or load job failures, then determine if the SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base management pack exists in the DWStagingAndConfig database by running the following query.  
  
```  
select * from ManagementPack where mpname like '%SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base%'  
```  
  
 If the management pack does not exist, you need to restore your database to a state prior to upgrade. To restore your database, perform the following steps.  
  
1.  Perform disaster recovery steps for the database backups.  
  
2.  Disable the MPSyncJob schedule.  
  
3.  Restore all the missing primary keys in the DWRepository manually. You can drop and recreate the primary key using the SQL script from the Before Upgrade section.  
  
4.  Restart the failed base management pack deployment using the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
## Testing the Upgrade in a Lab Environment  
 We recommend that you test the upgrade to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 in a lab environment.  
  
## Upgrade Order and Timing  
 The order of your upgrades is important. Perform the upgrade steps in the following order:  
  
1.  Backup your databases and your management packs. See the topics "Backing Up Service Manager Databases" and "Backing Up Unsealed Management Packs" in the [Disaster Recovery Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209671).  
  
2.  Start with the data warehouse management server. You will be stopping the data warehouse jobs, and you will not be able to start them again until after you have completed the upgrade.  
  
3.  After the upgrade to the data warehouse management server is complete, upgrade the initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. If you created more than one [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, the initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server is the first one that you created.  
  
4.  Upgrade the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]s and any additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers.  
  
5.  Restart the data warehouse jobs.  
  
6.  Deploy the new [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)].  
  
 The timing of your upgrades is also important. After you upgrade your data warehouse management server, you must both update the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and deploy the new [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]. After you upgrade your initial [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, you must be prepared to upgrade your [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] or [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]s, additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers, and [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] at the same time.  
  
## Operations Manager Compatibility  
 This section describes the compatibility between [!INCLUDE[om2007r2short](../../../sm/deploy/upgrade/includes/om2007r2short_md.md)], [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] and [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1.  
  
### [!INCLUDE[om2007r2long](../../../sm/deploy/upgrade/includes/om2007r2long_md.md)]  
 [!INCLUDE[om2007r2short](../../../sm/deploy/upgrade/includes/om2007r2short_md.md)] agents must be removed from the Service Manager and data warehouse management servers before you attempt an upgrade. [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 includes a [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1 agent and it is automatically installed when you upgrade. After [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
 You can upgrade Service Manager servers in the presence of an [!INCLUDE[om2007r2short](../../../sm/deploy/upgrade/includes/om2007r2short_md.md)] console.  
  
### [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)]  
 [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] agents were not supported with [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. However, the agent that is automatically installed by [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1 is compatible with [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] and [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] SP1.  After [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
 You can upgrade Service Manager servers in the presence of an [!INCLUDE[om12long](../../../sm/deploy/upgrade/includes/om12long_md.md)] console.  
  
## Database Impacts  
 With [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1, you have the option to install Operations Manager and Configuration Manager data marts. Selecting this option will result in additional space requirements on the hard disk drive for the two databases, as well as associated file groups and log files.  
  
## Backing Up [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Before Upgrading  
 Before you start any upgrade, we recommend that you back up your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and data warehouse databases and the encryption key. If you have already backed up your databases and encryption key, you can continue to run the upgrade. Otherwise, review the backup procedures in the [Disaster Recovery Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209671) before you continue the upgrade.  
  
## Registering with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Data Warehouse  
 If you have installed a data warehouse management server in your environment, as part of the upgrade process, you must be able to view the status of the data warehouse jobs. You cannot perform this task if you have not registered with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse. If the **Data Warehouse** button is not visible in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], complete the procedure in "Registering with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Data Warehouse to Enable Reporting" in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).  
  
## Encryption Keys  
 When you have finished running Setup to either install or upgrade to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] SP1, you are prompted to open the Encryption Backup or Restore Wizard. If you have previously backed up the encryption keys, no additional action is required. If you never backed up the encryption keys, use the Encryption Key Backup or Restore Wizard to back up the encryption keys on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers.  
  
## Authoring Tool Workflows  
 When you use the Service Manager SP1 version of the Authoring tool to create a workflow, then custom scripts using Windows PowerShell cmdlets called by the workflow fail. This is due to a problem in the Service Manager MonitoringHost.exe.config file.  
  
 To work around this problem, update the MonitoringHost.exe.config XML file using the following steps.  
  
1.  Navigate to %ProgramFiles%\\Microsoft System Center 2012\\Service Manager\\ or the location where you installed Service Manager.  
  
2.  Edit the MonitoringHost.exe.config file and add the section in italic type from the example below in the corresponding section of your file. You must insert the section before \<publisherPolicy apply\="yes" \/\>.  
  
3.  Save your changes to the file.  
  
4.  Restart the System Center Management service on the Service Manager management server.  
  
```  
<?xml version="1.0"?>  
<configuration>  
  <configSections>  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
  </configSections>  
  <uri>  
    <iriParsing enabled="true" />  
  </uri>    
  <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <dependentAssembly>  
        <assemblyIdentity name="Microsoft.Mom.Modules.DataTypes" publicKeyToken="31bf3856ad364e35" />  
        <publisherPolicy apply="no" />  
        <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
      </dependentAssembly>  
      <dependentAssembly>  
        <assemblyIdentity name="Microsoft.EnterpriseManagement.HealthService.Modules.WorkflowFoundation" publicKeyToken="31bf3856ad364e35" />  
        <publisherPolicy apply="no" />  
        <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
      </dependentAssembly>  
  <dependentAssembly>   
         <assemblyIdentity name="Microsoft.EnterpriseManagement.Modules.PowerShell" publicKeyToken="31bf3856ad364e35" />  
        <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
     </dependentAssembly>   
      <publisherPolicy apply="yes" />  
      <probing privatePath="" />  
    </assemblyBinding>  
    <gcConcurrent enabled="true" />  
  </runtime>  
</configuration>  
  
```