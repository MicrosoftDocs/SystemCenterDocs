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
 

















---
# Upgrade Planning for System Center 2012 SP1 - Service Manager
This guide outlines the procedures necessary to upgrade to System Center 2012 Service Pack 1.  
  
 An in\-place upgrade from Service Manager to Service Manager SP1 is supported. An in\-place upgrade is an upgrade of all Service Manager parts on the same hardware. Other approaches, such as side\-by\-side upgrades or rolling upgrades, are not supported.  
  
 Upgrading to Service Manager SP1 requires preparation. We recommend that you install Service Manager in a lab environment and then replicate your production databases into the lab. You then perform an upgrade of the new installation in the lab, and once that has proven successful, perform the same upgrade to Service Manager SP1 in the production environment.  
  
## Evaluation and Select Versions  
 The release of System Center 2012 - Service Manager was available in two different versions:  
  
-   Evaluation version \(180\-day time\-out\)  
  
-   Select license version  
  
 Service Manager SP1 is available as an Evaluation version \(180\-day time\-out\) or Select License edition. The following upgrade paths are supported to Service Manager SP1.  
  
|Current Version|Upgraded Version|Status|  
|---------------------|----------------------|------------|  
|System Center 2012 - Service Manager Eval|System Center 2012 - Service Manager SP1 Eval|Evaluation period remains unchanged|  
|System Center 2012 - Service Manager Select|System Center 2012 - Service Manager SP1 Select|Licensed|  
  
> [!NOTE]  
>  Upgrading from an evaluation version of Service Manager to an evaluation version of Service Manager SP1 *does not* extend the 180\-day evaluation period.  
  
## Installation Location  
 The default folder for installing Service Manager and Service Manager SP1 is \\Program Files\\Microsoft System Center\\Service&nbsp;Manager&nbsp;2012. However, when you perform the upgrade to Service Manager SP1, the software is installed in the folder that Service Manager previously used. If Service Manager 2010 was previously upgraded to System Center 2012 - Service Manager, then the following folder might be used:  
  
 \\Program Files\\Microsoft System Center\\Service&nbsp;Manager&nbsp;2010.  
  
## Language Support  
 This release of Service Manager SP1 represents an ongoing progression of support for various languages. In System Center Service ManagerÂ&nbsp;2010, you used the Latin1\_General\_100\_CI\_AS collation for the Turkish language. Service Manager and Service Manager SP1 supports the Turkish\_100\_CI\_AS collation. However, if you upgraded from System Center Service ManagerÂ&nbsp;2010 to System Center 2012 - Service Manager, the collation that was used for the Turkish language \(Latin1\_General\_100\_CI\_AS\) would have been carried forward to System Center 2012 - Service Manager, and will be when you upgrade to System Center 2012 - Service Manager SP1.  
  
## Hardware Requirements for System Center 2012 - Service Manager SP1  
 System Center 2012 - Service Manager SP1 will function on the same hardware that you used for System Center 2012 - Service Manager.  
  
 All hardware requirements for System Center 2012 - Service Manager SP1 are fully documented in [Hardware Requirements for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=253556).  
  
## Software Requirements for System Center 2012 - Service Manager SP1  
 To upgrade to System Center 2012 Service Pack 1 SP1, you must first apply Cumulative Update 2 for System Center 2012 - Service Manager.  
  
 System Center 2012 - Service Manager SP1 has the same software requirements for the Service Manager console that System Center Service ManagerÂ&nbsp;2010 does, except for the new requirement of Microsoft SQL Server 2012 Analysis Management Objects \(AMO\). Microsoft SQL Server 2012 AMO is supported on SQL Server 2008 and SQL Server 2012. In addition, the Service Manager console can now be installed on computers running Windows 8 and Windows Server 2012.  
  
 The Service Manager and data warehouse management servers, along with the Self-Service Portal, is supported with Windows Server 2012.  
  
 All software requirements for System Center 2012 - Service Manager SP1 are fully documented in [Software Requirements for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=252844).  
  
## Preventing MPSync Jobs From Failing  
 **Before Upgrade**  
  
 **Description:** A problem with the upgrade process causes MPSync job to fail after the upgrade is complete. To prevent this problem from occurring before you upgrade, you must run the SQL script below on the DWRepository database to get the actual SQL scripts that drop and add a constraint on the primary key in fact tables in the DWRepository database to correct the problem. Additionally, transform and load jobs might also fail. This error can occur because of erroneous database grooming.  
  
```  
;WITH FactName  
AS (  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; select w.WarehouseEntityName from etl.WarehouseEntity w  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; join etl.WarehouseEntityType t on w.WarehouseEntityTypeId = t.WarehouseEntityTypeId  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; where t.WarehouseEntityTypeName = 'Fact'  
),FactList  
AS (  
&nbsp;&nbsp;&nbsp; SELECT&nbsp; PartitionName, p.WarehouseEntityName,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RANK() OVER ( PARTITION BY p.WarehouseEntityName ORDER BY PartitionName ASC ) AS RK  
&nbsp;&nbsp;&nbsp; FROM&nbsp;&nbsp;&nbsp; etl.TablePartition p  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; join FactName f on p.WarehouseEntityName = f.WarehouseEntityName  
)  
, FactPKList  
AS (  
&nbsp;&nbsp;&nbsp; SELECT&nbsp; f.WarehouseEntityName, a.TABLE_NAME, a.COLUMN_NAME, b.CONSTRAINT_NAME, f.RK,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CASE WHEN b.CONSTRAINT_NAME = 'PK_' + f.WarehouseEntityName THEN 1 ELSE 0 END AS DefaultConstraints  
&nbsp;&nbsp;&nbsp; FROM&nbsp;&nbsp;&nbsp; FactList f  
&nbsp;&nbsp;&nbsp; JOIN&nbsp;&nbsp;&nbsp; INFORMATION_SCHEMA.KEY_COLUMN_USAGE a ON f.PartitionName = a.TABLE_NAME  
&nbsp;&nbsp;&nbsp; JOIN&nbsp;&nbsp;&nbsp; INFORMATION_SCHEMA.TABLE_CONSTRAINTS b ON a.CONSTRAINT_NAME = b.CONSTRAINT_NAME AND b.CONSTRAINT_TYPE = 'Primary key'  
)  
, FactWithoutDefaultConstraints  
AS (  
&nbsp;&nbsp;&nbsp; SELECT&nbsp; a.*  
&nbsp;&nbsp;&nbsp; FROM&nbsp;&nbsp;&nbsp; FactPKList a  
&nbsp;&nbsp;&nbsp; LEFT JOIN FactPKList b ON b.WarehouseEntityName = a.WarehouseEntityName AND b.DefaultConstraints = 1  
&nbsp;&nbsp;&nbsp; WHERE&nbsp;&nbsp; b.WarehouseEntityName IS NULL AND a.RK = 1  
)  
, FactPKListStr  
AS (  
&nbsp;&nbsp;&nbsp; SELECT&nbsp; DISTINCT f1.WarehouseEntityName, f1.TABLE_NAME, f1.CONSTRAINT_NAME, F.COLUMN_NAME AS PKList  
&nbsp;&nbsp;&nbsp; FROM&nbsp;&nbsp;&nbsp; FactWithoutDefaultConstraints f1  
&nbsp;&nbsp;&nbsp; CROSS APPLY (  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SELECT&nbsp; '[' + COLUMN_NAME + '],'  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FROM&nbsp;&nbsp;&nbsp; FactWithoutDefaultConstraints f2  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; WHERE&nbsp;&nbsp; f2.TABLE_NAME = f1.TABLE_NAME  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ORDER BY COLUMN_NAME  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FOR  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; XML PATH('')  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ) AS F (COLUMN_NAME)  
)  
SELECT&nbsp; 'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] DROP CONSTRAINT [' + f.CONSTRAINT_NAME + ']' + CHAR(13) + CHAR(10) +  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] ADD CONSTRAINT [PK_' + f.WarehouseEntityName + '] PRIMARY KEY NONCLUSTERED (' + SUBSTRING(f.PKList, 1, LEN(f.PKList) -1) + ')' + CHAR(13) + CHAR(10)  
FROM&nbsp;&nbsp;&nbsp; FactPKListStr f  
  
```  
  
 **Workaround 1:** If you have already upgraded and you do not have problems with transform or load job failures but do have a management pack deployment failure, then follow the steps in the Before Upgrade section. In addition, after the default primary keys have been restored, restart the failed management pack deployment in the Service Manager console by navigating to the Data Warehouse workspace and then select Management Pack.  
  
 **Workaround 2:** If you have upgraded and you have problems with transform or load job failures, then determine if the SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base management pack exists in the DWStagingAndConfig database by running the following query.  
  
```  
select * from ManagementPack where mpname like '%SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base%'  
```  
  
 If the management pack does not exist, you need to restore your database to a state prior to upgrade. To restore your database, perform the following steps.  
  
1.  Perform disaster recovery steps for the database backups.  
  
2.  Disable the MPSyncJob schedule.  
  
3.  Restore all the missing primary keys in the DWRepository manually. You can drop and recreate the primary key using the SQL script from the Before Upgrade section.  
  
4.  Restart the failed base management pack deployment using the Service Manager console.  
  
## Testing the Upgrade in a Lab Environment  
 We recommend that you test the upgrade to System Center 2012 - Service Manager SP1&nbsp;in a lab environment.  
  
## Upgrade Order and Timing  
 The order of your upgrades is important. Perform the upgrade steps in the following order:  
  
1.  Backup your databases and your management packs. See the topics "Backing Up Service Manager Databases" and "Backing Up Unsealed Management Packs" in the [Disaster Recovery Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209671).  
  
2.  Start with the data warehouse management server. You will be stopping the data warehouse jobs, and you will not be able to start them again until after you have completed the upgrade.  
  
3.  After the upgrade to the data warehouse management server is complete, upgrade the initial Service Manager management server. If you created more than one Service Manager management server, the initial Service Manager management server is the first one that you created.  
  
4.  Upgrade the Service Manager consoles and any additional Service Manager management servers.  
  
5.  Restart the data warehouse jobs.  
  
6.  Deploy the new Self-Service Portal.  
  
 The timing of your upgrades is also important. After you upgrade your data warehouse management server, you must both update the Service Manager management server and deploy the new Self-Service Portal. After you upgrade your initial Service Manager management server, you must be prepared to upgrade your Service Manager console or Service Manager consoles, additional Service Manager management servers, and Self-Service Portal at the same time.  
  
## Operations Manager&nbsp;Compatibility  
 This section describes the compatibility between Operations Manager 2007 R2, System CenterÂ&nbsp;2012 - Operations Manager and System Center 2012 - Service Manager SP1.  
  
### System Center Operations Manager 2007 R2  
 Operations Manager 2007 R2 agents must be removed from the Service Manager and data warehouse management servers before you attempt an upgrade. System Center 2012 - Service Manager SP1 includes a System CenterÂ&nbsp;2012 - Operations Manager SP1 agent and it is automatically installed when you upgrade. After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
 You can upgrade Service Manager servers in the presence of an Operations Manager 2007 R2 console.  
  
### System CenterÂ&nbsp;2012 - Operations Manager  
 System CenterÂ&nbsp;2012 - Operations Manager agents were not supported with System Center 2012 - Service Manager. However, the agent that is automatically installed by System Center 2012 - Service Manager SP1 is compatible with System CenterÂ&nbsp;2012 - Operations Manager and System CenterÂ&nbsp;2012 - Operations Manager SP1.  After Service Manager Setup completes, you must manually configure the agent to communicate with the Operations Manager management server.  
  
 To validate that the Operations Manager Agent was installed, open Control Panel and verify that the Operations Manager Agent is present. To manually configure the Operations Manager agent, see [Configuring Agents](http://go.microsoft.com/fwlink/p/?LinkId=264988).  
  
 You can upgrade Service Manager servers in the presence of an System CenterÂ&nbsp;2012 - Operations Manager console.  
  
## Database Impacts  
 With System Center 2012 - Service Manager SP1, you have the option to install Operations Manager and Configuration Manager data marts. Selecting this option will result in additional space requirements on the hard disk drive for the two databases, as well as associated file groups and log files.  
  
## Backing Up Service Manager Before Upgrading  
 Before you start any upgrade, we recommend that you back up your Service Manager and data warehouse databases and the encryption key. If you have already backed up your databases and encryption key, you can continue to run the upgrade. Otherwise, review the backup procedures in the [Disaster Recovery Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209671) before you continue the upgrade.  
  
## Registering with the Service Manager Data Warehouse  
 If you have installed a data warehouse management server in your environment, as part of the upgrade process, you must be able to view the status of the data warehouse jobs. You cannot perform this task if you have not registered with the Service Manager data warehouse. If the **Data Warehouse** button is not visible in the Service Manager console, complete the procedure in "Registering with the Service Manager Data Warehouse to Enable Reporting" in the [Deployment Guide for System&nbsp;Center&nbsp;2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).  
  
## Encryption Keys  
 When you have finished running Setup to either install or upgrade to System Center 2012 - Service Manager SP1, you are prompted to open the Encryption Backup or Restore Wizard. If you have previously backed up the encryption keys, no additional action is required. If you never backed up the encryption keys, use the Encryption Key Backup or Restore Wizard to back up the encryption keys on the Service Manager management servers.  
  
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
&nbsp; <configSections>  
&nbsp;&nbsp;&nbsp; <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
&nbsp; </configSections>  
&nbsp; <uri>  
&nbsp;&nbsp;&nbsp; <iriParsing enabled="true" />  
&nbsp; </uri>&nbsp;   
&nbsp;&nbsp;<runtime>  
&nbsp;&nbsp;&nbsp; <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <dependentAssembly>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <assemblyIdentity name="Microsoft.Mom.Modules.DataTypes" publicKeyToken="31bf3856ad364e35" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="no" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </dependentAssembly>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <dependentAssembly>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <assemblyIdentity name="Microsoft.EnterpriseManagement.HealthService.Modules.WorkflowFoundation" publicKeyToken="31bf3856ad364e35" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="no" />  
&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </dependentAssembly>  
&nbsp;&nbsp;<dependentAssembly>   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<assemblyIdentity name="Microsoft.EnterpriseManagement.Modules.PowerShell" publicKeyToken="31bf3856ad364e35" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</dependentAssembly>   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <publisherPolicy apply="yes" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <probing privatePath="" />  
&nbsp;&nbsp;&nbsp; </assemblyBinding>  
&nbsp;&nbsp;&nbsp; <gcConcurrent enabled="true" />  
&nbsp; </runtime>  
</configuration>  
  
```
