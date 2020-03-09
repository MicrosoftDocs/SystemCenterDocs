---
ms.assetid: 84899e64-8395-4d33-aecb-19b07be15b9a  
title: Service-level changes for gMSA in System Center Operations Manager
description: This article describes the service-level changes that are required to use group Managed Service Accounts (gMSA), a new feature supported in Operations Manager 2019 UR1.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---


# Service-level changes

This article describes the service-level changes that are required to use group Managed Service Accounts (gMSAs).

>[!NOTE]
>This article applies to System Center 2019 Update Rollup 1 (UR1) Operations Manager.


## Change the service account for System Center Data Access Service to gMSA

To enable System Center Data Access Service to use gMSA:

1. Add **gMSA** to the local Administrators group on the computer on which the management server is installed, as shown.

    ![Data access service](media/gmsa/data-access-service.png)

1. Change the existing service account for System Center Data Access Service to **gMSA** from Windows Services Console, as shown.

    ![Log On As A Service right](media/gmsa/logon-service-right.png)


## Change the credentials for the System Center configuration service

Change the sign-in credentials for this service account from Windows Services Console, as shown.

![Configuration service](media/gmsa/configuration-service.png)

![Configuration properties](media/gmsa/configuration-properties.png)

Validate that both the services are running with gMSA.

![System Center Data Access Service](media/gmsa/system-center-data-access-service.png)

## Change the service account for SQL Server Reporting Services to gMSA

You can change the data reader account in the following two ways.

### From Windows Services Console

Change the existing service account for SQL Server Reporting Services to **gMSA** from Windows Services Console, as shown.

![Change service account for SQL Server](media/gmsa/change-service-account-SQL.png)

Validate that SQL Server Reporting Services is running with gMSA.

![SQL Server Reporting Services](media/gmsa/sql-server-reporting-service.png)

### From Reporting Services Configuration Manager

![Reporting Services Configuration Manager](media/gmsa/reporting-service-configuration-manager.png)

Select **Service Credentials** as **Authentication Type**, which is already specified as a gMSA earlier in Reporting Services Configuration Manager.

![Report Server Database Configuration Wizard](media/gmsa/configuration-manager-change-credentials.png)

![Report Server Database](media/gmsa/configuration-manager-report-server-database.png)

>[!NOTE]
>SQL Server doesn't support gMSA for the SQL Server Reporting Services Execution account. Continue to use a non-gMSA account for this account.


## Change the Data Warehouse Write account to use gMSA

Operations Manager stores the credentials for the Data Warehouse Write account within a Run As account, called the Data Warehouse Action account.

Change the credentials of this Action account to gMSA that you intend to use as a Data Warehouse Write account.

![Data Warehouse Monitoring host](media/gmsa/change-data-warehouse-write-account.png)

Validate that the *MonitoringHost.exe* uses the gMSA credentials for the Data Warehouse Write account.

## Update the Data Warehouse database

1. Run the following SQL query against your Data Warehouse database. Replace *DataWarehouseName* with the name of your Data Warehouse database.

    ```
    SELECT [ManagementGroupDefaultName],[WriterLoginName] FROM [DataWarehouseName].[dbo].[ManagementGroup]

    ```
1. If the previous query doesn't return the gMSA that you created for the Data Warehouse Write account, then execute the following query to update it.

    ```
    UPDATE [DataWarehouseName].[dbo].[ManagementGroup] SET [WriterLoginName] = 'DOMAIN\USERNAME' WHERE [ManagementGroupDefaultName] = 'SCOM MANAGEMENT GROUP NAME'
    ```



## Next steps

[Console-level changes](console-level-changes.md)
