---
title: include file
description: include file that outlines planning considerations and the order to upgrade to System Center 2019 - Service Manager.  
ms.custom: na
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 03/14/2019
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: include
ms.assetid: 21baa50d-4f34-489e-b3ce-f44e1b3a83aa
---

## Upgrade to System Center 2019 - Service Manager
The following sections provide information about how to upgrade to System Center 2019 - Service Manager (SM).  

> [!WARNING]  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:  
>   
> 1.  Orchestrator  
> 2.  Service Manager  
> 3.  Data Protection Manager  
> 4.  Operations Manager  
> 5.  Configuration Manager  
> 6.  Virtual Machine Manager  
> 7.  App Controller  

 You can only upgrade to System Center 2019 from System Center 2016 or 1801 or 1807.

> [!IMPORTANT]  
>  It's assumed in this guide that you're performing an *upgrade* to an existing System Center version. For information about installing System Center 2019 - Service Manager on a computer where no previous version of Service Manager exists, see [deploying System Center - Service Manager](../scsm/deploy-sm.md).  

## Plan the upgrade to System Center 2019 - Service Manager

This section outlines the procedures necessary to upgrade to System Center 2019.  

An in-place upgrade from Service Manager 2016, 1801, 1807 is supported. An in-place upgrade is an upgrade of all the Service Manager parts on the same hardware. Other approaches, such as side-by-side upgrades or rolling upgrades, aren't supported.  

Upgrading to Service Manager 2019 requires preparation. We recommend that you install Service Manager in a lab environment and then replicate your production databases into the lab. After that, perform an upgrade of the new installation in the lab.

### Evaluation and Select versions  

The release of System Center 2016 and 1801 - Service Manager was available in two different versions:  

-   Evaluation version \(180\-day time\-out\)
-   Select license version  

The following upgrade paths are supported to Service Manager 2019.  

|Current Version|Upgraded Version|Status|  
|---------------------|----------------------|------------|  
|System Center 2016/1801 - Service Manager Eval|System Center 2019 - Service Manager Eval|Evaluation period remains unchanged|  
|System Center 2016/1801/1807 - Service Manager Select|System Center 2019 - Service Manager Select|Licensed|  

> [!NOTE]  
>  Upgrading from an evaluation version of Service Manager to an evaluation version of Service Manager 2019 *does not* extend the 180 days evaluation period.  

### Installation location  

The default folder for installing Service Manager is \\Program Files\\Microsoft System Center\\Service&nbsp;Manager. However, when you perform the upgrade to Service Manager, the software is installed in the folder that Service Manager previously used. If Service Manager 2016/1801 was previously upgraded, then the following folder could be used:  

\\Program Files\\Microsoft System Center\\Service&nbsp;Manager&nbsp;  


### Hardware requirements for System Center 2019 - Service Manager  

All hardware requirements for System Center 2019 - Service Manager are fully documented in [Hardware Requirements](../scsm/system-requirements.md).  

### Software requirements for System Center 2019 - Service Manager

All software requirements for System Center 2019- Service Manager are fully documented in [Software Requirements](../scsm/system-requirements.md).  

### Impact on custom development

With the System Center 2016 - Service Manager release, the product has moved to support .NET 4.5.1. The tool set to support this movement to .NET 4.5.1 required to break a few dependencies and has led to the movement of classes across the assemblies.

### Preventing MPSync jobs from failing  

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
    SELECT  PartitionName, p.WarehouseEntityName,  
            RANK() OVER ( PARTITION BY p.WarehouseEntityName ORDER BY PartitionName ASC ) AS RK  
    FROM    etl.TablePartition p  
       join FactName f on p.WarehouseEntityName = f.WarehouseEntityName  
)  
, FactPKList  
AS (  
    SELECT  f.WarehouseEntityName, a.TABLE_NAME, a.COLUMN_NAME, b.CONSTRAINT_NAME, f.RK,  
            CASE WHEN b.CONSTRAINT_NAME = 'PK_' + f.WarehouseEntityName THEN 1 ELSE 0 END AS DefaultConstraints  
    FROM    FactList f  
    JOIN    INFORMATION_SCHEMA.KEY_COLUMN_USAGE a ON f.PartitionName = a.TABLE_NAME  
    JOIN    INFORMATION_SCHEMA.TABLE_CONSTRAINTS b ON a.CONSTRAINT_NAME = b.CONSTRAINT_NAME AND b.CONSTRAINT_TYPE = 'Primary key'  
)  
, FactWithoutDefaultConstraints  
AS (  
    SELECT  a.*  
    FROM    FactPKList a  
    LEFT JOIN FactPKList b ON b.WarehouseEntityName = a.WarehouseEntityName AND b.DefaultConstraints = 1  
    WHERE   b.WarehouseEntityName IS NULL AND a.RK = 1  
)  
, FactPKListStr  
AS (  
    SELECT  DISTINCT f1.WarehouseEntityName, f1.TABLE_NAME, f1.CONSTRAINT_NAME, F.COLUMN_NAME AS PKList  
    FROM    FactWithoutDefaultConstraints f1  
    CROSS APPLY (  
                    SELECT  '[' + COLUMN_NAME + '],'  
                    FROM    FactWithoutDefaultConstraints f2  
                    WHERE   f2.TABLE_NAME = f1.TABLE_NAME  
                    ORDER BY COLUMN_NAME  
                FOR  
                   XML PATH('')  
                ) AS F (COLUMN_NAME)  
)  
SELECT  'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] DROP CONSTRAINT [' + f.CONSTRAINT_NAME + ']' + CHAR(13) + CHAR(10) +  
        'ALTER TABLE [dbo].[' + f.TABLE_NAME + '] ADD CONSTRAINT [PK_' + f.WarehouseEntityName + '] PRIMARY KEY NONCLUSTERED (' + SUBSTRING(f.PKList, 1, LEN(f.PKList) -1) + ')' + CHAR(13) + CHAR(10)  
FROM    FactPKListStr f  

```  

**Workaround 1:** If you've already upgraded and you don't have problems with transform or load job failures but do have a management pack deployment failure, then follow the steps in the Before Upgrade section. In addition, after the default primary keys have been restored, restart the failed management pack deployment in the Service Manager console by navigating to the Data Warehouse workspace and then select Management Pack.  

**Workaround 2:** If you've upgraded and you've problems with transform or load job failures, then determine if the SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base management pack exists in the DWStagingAndConfig database by running the following query.  

```  
select * from ManagementPack where mpname like '%SystemDerivedMp.Microsoft.SystemCenter.Datawarehouse.Base%'  
```  

If the management pack doesn't exist, you need to restore your database to a state prior to upgrade. To restore your database, perform the following steps.  

1.  Perform disaster recovery steps for the database backups.  

2.  Disable the MPSyncJob schedule.  

3.  Restore all the missing primary keys in the DWRepository manually. You can drop and recreate the primary key using the SQL script from the Before Upgrade section.  

4.  Restart the failed base management pack deployment using the Service Manager console.  

### Testing the upgrade in a lab environment  

We recommend that you test the upgrade to System Center 2019 - Service Manager in a lab environment.  

### Upgrade order and timing  

The order of your upgrades is important. Perform the upgrade steps in the following order:  

1.  Back up your databases and your management packs. See the sections **Backing Up Service Manager Databases** and **Backing Up Unsealed Management Packs** in the [Disaster Recovery Guide for System Center - Service Manager](../scsm/disaster-recovery.md).  

2.  Start with the data warehouse management server. You will be stopping the data warehouse jobs, and you won't be able to start them again until after you've completed the upgrade.  

3.  After the upgrade to the data warehouse management server is complete, upgrade the initial Service Manager management server. If you created more than one Service Manager management server, the initial Service Manager management server is the first one that you created.  

4.  Upgrade the Service Manager consoles and any additional Service Manager management servers.  

5.  Restart the data warehouse jobs.  

6.  Deploy the new Self-Service Portal.  

The timing of your upgrades is also important. After you upgrade your data warehouse management server, you must update the Service Manager management server and also deploy the new Self-Service Portal. After you upgrade your initial Service Manager management server, you must be prepared to upgrade your Service Manager console or Service Manager consoles, additional Service Manager management servers, and Self-Service Portal at the same time.  


### Database impacts  

With System Center 2019 - Service Manager, you've the option to install Operations Manager and Configuration Manager data marts. Selecting this option will result in additional space requirements on the hard disk drive for the two databases, as well as associated file groups and log files.  

### Back up Service Manager before you upgrade  

Before you start any upgrade, we recommend that you back up your Service Manager and data warehouse databases and the encryption key. If you've already backed up your databases and encryption key, you can continue to run the upgrade. Otherwise, review the backup procedures in the [Disaster Recovery Guide for System Center - Service Manager](../scsm/disaster-recovery.md) before you continue the upgrade.  

### Register the Service Manager data warehouse  

If you've installed a data warehouse management server in your environment, as part of the upgrade process, you must be able to view the status of the data warehouse jobs. You can't perform this task if you haven't registered with the Service Manager data warehouse. If the **Data Warehouse** button isn't visible in the Service Manager console, complete the procedure in **Registering with the Service Manager Data Warehouse to Enable Reporting** in the [Deployment Guide for System Center - Service Manager](../scsm/deploy-sm.md).  

### Encryption keys  

When you've finished running Setup to either install or upgrade to System Center 2019 - Service Manager, you're prompted to open the Encryption Backup or Restore Wizard. If you've previously backed up the encryption keys, no additional action is required. If you never backed up the encryption keys, use the Encryption Key Backup or Restore Wizard to back up the encryption keys on the Service Manager management servers.  
