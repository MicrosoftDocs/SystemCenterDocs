---
ms.assetid: 84899e64-8395-4d33-aecb-19b07be15b9a  
title: Service level changes for gMSA in System Center Operations Manager
description: This article details the service level changes that are required to use group managed service accounts (gMSA), a new feature supported in Operations Manager 2019 UR1.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---


# Service level changes
This article details the service level changes that are required to use group Managed Service Accounts (gMSA).

>[!NOTE]
>This article is applicable for System Center 2019 UR1 - Operations Manager.


## Change service account for System Center Data Access Service to gMSA

To enable the System Center Data Access Service to use gMSA, do following:

1.	Add gMSA to the local Administrators group on the computer on which, the management server is installed, as shown in the image below.

    ![Data access service](media/gmsa/data-access-service.png)

2.	Change the existing service account for System Center Data Access Service to gMSA from the Windows Services Console as shown below:

    ![Logon service right](media/gmsa/logon-service-right.png)


## Change the credentials for System Center configuration service

Change the log on credentials for this service account from *Windows Services Console* as shown below:

![Configuration service](media/gmsa/configuration-service.png)

![Configuration properties](media/gmsa/configuration-properties.png)

Validate that both the services are running with gMSA.

![Data access service](media/gmsa/system-center-data-access-service.png)

## Change service account for SQL Server Reporting Services to gMSA
You can change the data reader account in the following two ways:

### From Windows Services Console

Change the existing service account for SQL Server Reporting Services to gMSA from the Windows Services Console as shown below:

![change service account for SQL Server](media/gmsa/change-service-account-SQL.png)

Validate that the SSRS is running with gMSA.

![SQL server reporting](media/gmsa/sql-server-reporting-service.png)

### From Reporting Services Configuration Manager

![Reporting service configuration manager](media/gmsa/reporting-service-configuration-manager.png)

Select **Authentication Type** as **Service Credentials**, which is already specified as a gMSA earlier in the Reporting Services Configuration Manager.

![Report server configuration manager](media/gmsa/configuration-manager-change-credentials.png)

![Report server database](media/gmsa/configuration-manager-report-server-database.png)

>[!NOTE]
>SQL Server doesn’t support gMSA for SSRS Execution account. Continue to use non-gMSA account for this account.


## Change the Data Warehouse Write account to use gMSA
Operations Manager stores the credentials for the Data Warehouse Write account within a Run as account, called Data Warehouse Action account.

Change the credentials of this action account to gMSA that you intend to use as Data Warehouse Write Account.

![Datawarehouse Monitoring host](media/gmsa/change-data-warehouse-write-account.png)

Validate that the *monitoringhost.exe* uses the gMSA credentials for DW Write account.

## Update the Data Warehouse database

1.	Run the following SQL Query against your Data Warehouse database. Replace *DataWarehouseName* with the name of your data Warehouse database.

    ```
    SELECT [ManagementGroupDefaultName],[WriterLoginName] FROM [DataWarehouseName].[dbo].[ManagementGroup]

    ```
2.	If the above query does not return the gMSA that you had created for the DW Write account, then execute the following query to update it:

    ```
    UPDATE [DataWarehouseName].[dbo].[ManagementGroup] SET [WriterLoginName] = 'DOMAIN\USERNAME' WHERE [ManagementGroupDefaultName] = 'SCOM MANAGEMENT GROUP NAME'
    ```



## Next steps
[Console level changes](console-level-changes.md)
