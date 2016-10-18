---
title: Upgrade Planning for System Center 2016 - Service Manager
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cad46180-3c12-4eb2-a4bc-99fd88d2f3e7
---

# Upgrade Planning for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This guide outlines the procedures necessary to upgrade to System Center 2016.  

 An in\-place upgrade from Service Manager 2012 R2 to Service Manager 2016 is supported. An in\-place upgrade is an upgrade of all Service Manager parts on the same hardware. Other approaches, such as side\-by\-side upgrades or rolling upgrades, are not supported.  

 Upgrading to Service Manager 2016 requires preparation. We recommend that you install Service Manager in a lab environment and then replicate your production databases into the lab. You then perform an upgrade of the new installation in the lab, and once that has proven successful, perform the same upgrade to Service Manager SP1 in the production environment.  

## Evaluation and Select Versions  

 The release of System Center 2016 - Service Manager was available in two different versions:  

-   Evaluation version \(180\-day time\-out\)  

-   Select license version  

The following upgrade paths are supported to Service Manager 2016.  

|Current Version|Upgraded Version|Status|  
|---------------------|----------------------|------------|  
|System Center 2012 R2 - Service Manager Eval|System Center 2016 - Service Manager Eval|Evaluation period remains unchanged|  
|System Center 2012 R2 - Service Manager Select|System Center 2016 - Service Manager Select|Licensed|  

> [!NOTE]  
>  Upgrading from an evaluation version of Service Manager 2012 R2 to an evaluation version of Service Manager 2016 *does not* extend the 180\-day evaluation period.  

## Installation Location  

The default folder for installing Service Manager is \\Program Files\\Microsoft System Center\\Service&nbsp;Manager. However, when you perform the upgrade to Service Manager, the software is installed in the folder that Service Manager previously used. If Service Manager 2010 or Service Manager 2012 was previously upgraded, then the following folders could be used:  

\\Program Files\\Microsoft System Center\\Service&nbsp;Manager&nbsp;2010  
\\Program Files\\Microsoft System Center\\Service&nbsp;Manager&nbsp;2012


## Hardware Requirements for System Center 2016 - Service Manager  

 All hardware requirements for System Center 2016 - Service Manager are fully documented in [Hardware Requirements for System Center 2016 - Service Manager](../../system-requirements/Minimum-Hardware-Recommendations.md).  

## Software Requirements for System Center 2016 - Service Manager 

 To upgrade to System Center 2016, you must first apply the Update Rollup 9 or later for System Center 2012 R2 - Service Manager.  


 All software requirements for System Center 2016 - Service Manager are fully documented in [Software Requirements for System Center 2016 - Service Manager](../../system-requirements/system-requirements.md).  

 ## Impact on custom development

 With the System Center 2016 - Service Manager release, the product has moved to support .Net 4.5.1. The tool set to support this movement to .Net 4.5.1 required to break a few dependencies and has led to the movement of classes across the assemblies. Hence, the upgrade to Service Manager 2016 may break the custom solutions made in house or by 3rd party (non-Microsoft). Please refer the [steps to upgrade your custom solutions](https://blogs.technet.microsoft.com/servicemanager/2016/08/03/scsm-2016-upgrade-steps-for-custom-development/), to avoid getting into this problem.

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

 We recommend that you test the upgrade to System Center 2016 - Service Manager in a lab environment.  

## Upgrade Order and Timing  

 The order of your upgrades is important. Perform the upgrade steps in the following order:  

1.  Backup your databases and your management packs. See the topics "Backing Up Service Manager Databases" and "Backing Up Unsealed Management Packs" in the [Disaster Recovery Guide for System Center 2016 - Service Manager](../manage/disaster-disaster-recovery-guide-for-system-center-2016-service-manager.md).  

2.  Start with the data warehouse management server. You will be stopping the data warehouse jobs, and you will not be able to start them again until after you have completed the upgrade.  

3.  After the upgrade to the data warehouse management server is complete, upgrade the initial Service Manager management server. If you created more than one Service Manager management server, the initial Service Manager management server is the first one that you created.  

4.  Upgrade the Service Manager consoles and any additional Service Manager management servers.  

5.  Restart the data warehouse jobs.  

6.  Deploy the new Self-Service Portal.  

 The timing of your upgrades is also important. After you upgrade your data warehouse management server, you must both update the Service Manager management server and deploy the new Self-Service Portal. After you upgrade your initial Service Manager management server, you must be prepared to upgrade your Service Manager console or Service Manager consoles, additional Service Manager management servers, and Self-Service Portal at the same time.  


## Database Impacts  

 With System Center 2016 - Service Manager, you have the option to install Operations Manager and Configuration Manager data marts. Selecting this option will result in additional space requirements on the hard disk drive for the two databases, as well as associated file groups and log files.  

## Backing Up Service Manager Before Upgrading  

 Before you start any upgrade, we recommend that you back up your Service Manager and data warehouse databases and the encryption key. If you have already backed up your databases and encryption key, you can continue to run the upgrade. Otherwise, review the backup procedures in the [Disaster Recovery Guide for System Center - Service Manager](../manage/disaster-disaster-recovery-guide-for-system-center-2016-service-manager.md) before you continue the upgrade.  

## Registering with the Service Manager Data Warehouse  

 If you have installed a data warehouse management server in your environment, as part of the upgrade process, you must be able to view the status of the data warehouse jobs. You cannot perform this task if you have not registered with the Service Manager data warehouse. If the **Data Warehouse** button is not visible in the Service Manager console, complete the procedure in "Registering with the Service Manager Data Warehouse to Enable Reporting" in the [Deployment Guide for System Center 2016 - Service Manager](deploy-deploying-system-center-2016-service-manager.md).  

## Encryption Keys  

 When you have finished running Setup to either install or upgrade to System Center 2016 - Service Manager, you are prompted to open the Encryption Backup or Restore Wizard. If you have previously backed up the encryption keys, no additional action is required. If you never backed up the encryption keys, use the Encryption Key Backup or Restore Wizard to back up the encryption keys on the Service Manager management servers.  
