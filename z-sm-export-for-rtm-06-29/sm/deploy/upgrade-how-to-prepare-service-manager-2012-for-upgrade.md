---
title: How to Prepare Service Manager 2012 for Upgrade to SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5bf76997-344c-4bda-abb3-42c604cd56b2
 

















---
# How to Prepare Service Manager 2012 for Upgrade to SP1
This topic describes how to prepare your System Center 2012 - Service Manager environment for an upgrade. To do this, perform the following procedures for upgrading the data warehouse management server:  
  
1.  List the data warehouse jobs that are running.  
  
2.  Disable the data warehouse job schedules.  
  
3.  Confirm that the data warehouse jobs have stopped running.  
  
 When the data warehouse jobs have completed, start the upgrade of the data warehouse management server.  
  
 After the data warehouse has been upgraded, perform the following procedures on the first Service Manager management server:  
  
1.  Wait 10 minutes, and then start the upgrade of the Service Manager management server.  
  
### To list the data warehouse jobs by using Windows PowerShell cmdlets  
  
1.  On the computer that hosts the data warehouse management server, click **Start**, click **All Programs**, click **Microsoft System Center 2012**, and then click **Service Manager Shell**.  
  
2.  Type the following commands, and then press ENTER after each command:  
  
    ```  
    Set-ExecutionPolicy –force RemoteSigned  
    ```  
  
    ```  
    cd 'C:\Program Files\Microsoft System Center 2012\Service Manager'  
    Import-Module .\Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1  
  
    ```  
  
    ```  
    Get-SCDWJob  
    ```  
  
3.  A list of the data warehouse jobs appears. Use this list in the next procedure, "To disable data warehouse job schedules by using Windows PowerShell cmdlets.”  
  
### To disable data warehouse job schedules by using Windows PowerShell cmdlets  
  
1.  Type the following commands, and then press ENTER after each command:  
  
    ```  
    Disable-SCDWJobSchedule –JobName Extract_<data warehouse management group name>  
    ```  
  
    ```  
    Disable-SCDWJobSchedule –JobName Extract_<Service Manager management group name>  
    ```  
  
    ```  
    Disable-SCDWJobSchedule –JobName Transform.Common  
    ```  
  
    ```  
    Disable-SCDWJobSchedule –JobName Load.Common  
    ```  
  
    ```  
    Disable-SCDWJobSchedule –JobName DWMaintenance  
    ```  
  
    ```  
    Disable-SCDWJobSchedule –JobName MPSyncJob  
    ```  
  
    ```  
    Start-SCDWJob –JobName MPSyncJob  
    ```  
  
     The last command to start the **MPSyncJob** will enable the extraction, transformation, and load \(ETL\) jobs to run to completion. After that, because all the schedules have been disabled, the jobs will stop. To close the Windows PowerShell window, type **exit**.  
  
### To confirm that the data warehouse jobs have stopped running  
  
1.  In the Service Manager console, click **Data Warehouse**.  
  
2.  In the **Data Warehouse** pane, expand **Data Warehouse**, and then click **Data Warehouse Jobs**.  
  
3.  In the **Data Warehouse Jobs** pane, observe the **Status** column for each data warehouse job. When the status for each job is listed as **Not Started**, proceed to the next procedure to stop the Self-Service Portal. If no Self-Service Portal exists in your environment, you can start the upgrade process in [How to Upgrade to System Center 2012 SP1 \- Service Manager](../../../sm/deploy/upgrade/How-to-Upgrade-to-System-Center-2012-SP1---Service-Manager.md).  
  
### To prevent MPSync jobs from failing  
  
-   Run the SQL script below on the DWRepository database to get the SQL scripts that drop and add a constraint on the primary key in fact tables in the DWRepository database to correct the problem  
  
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
