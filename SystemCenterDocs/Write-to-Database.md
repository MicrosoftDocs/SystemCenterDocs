---
title: Write to Database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e47a137-5f4b-41a2-a13a-59bcaae8e750
---
# Write to Database
The Write to Database activity writes a row into a database table. This activity interacts with the following databases:

-   Access

-   ODBC

-   Oracle

-   SQL Server

The Write to Database activity can be used to replicate important Windows Event Log Events to a database table that is able to be queried and maintained.

## Configuring the Write to Database Activity
Before you configure the Write to Database activity, you need to determine the following:

-   The database you are connecting to.

-   The table and fields you are updating.

Use the following information to configure the Write to Database activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Table name**|Type the name of the database table that you are adding the row to.|
|**Data**|The list displays all the fields in the table that will be set. To add a field, click **Add** and enter the **Field name** and **Value**. To remove a field, select it and click **Remove**. To edit a field, double\-click the field name.|

### Connection Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Database type**|Select the **Database type** from the drop\-down list. The options include the following:<br /><br />-   Access<br />-   ODBC<br />-   Oracle<br />-   SQL Server<br /><br />Configuration instructions for each **Connection** tab **Database type** are listed in the following tables.|

### Access Connections Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the name of the **Access** database file that you want to access.|
|**Workgroup file**|Type the name of the **Access** workgroup file that is associated with this database.|
|**User name**|Type the user name for the workgroup file.|
|**Password**|Type the password for the workgroup file.|
|**DB password**|Type the password for the Access database.|

### ODBC Connections Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**DSN**|Enter the data source name.|
|**User name**|Enter the user name for this database.|
|**Password**|Enter the password for this database.|

### Oracle Connections Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Service Name**|Enter the service name.|
|**User name**|Enter the user name for this database.|
|**Password**|Enter the password for this database.|

### SQL Server Connections Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Authentication**|Select either **Windows Authentication** or **SQL Server Authentication**.|
|**Server**|Enter the name of the SQL Server that you want to access.|
|**Initial catalog**|Enter the name of the initial catalog.<br /><br />If you selected the **SQL Server Authentication** option, type the user name and password used to access the SQL Server in the **User name** and **Password** boxes.|

### Timeout Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Timeout**|Enter the amount of time that the Query Database activity will wait for the database operation to complete.<br /><br />Set this value to **0** to wait indefinitely.|

### Security Credentials Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Use the security of the account assigned to the service**|Select this option if you want to run the Query Database activity using the same account that the runbook server uses.|
|**This account**|Use this option to specify a different account. Enter the **User name** and **Password**. **Note:** If you specify an invalid user name or password, the account assigned to the runbook server will be used to run the activity.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Initial Catalog|The initial catalog that was used when connecting to the database. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|
|Database server|The name of the database server. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|
|Table name|The name of the table that was written to.|
|Database user|The name of the user used to connect to the database server.|
|ODBC DSN|The name of the ODBC DSN. This published data will only be available when **ODBC** is selected on the **Connection** tab.|
|Oracle Service Name|The service name. This published data will only be available when **Oracle** is selected on the **Connection** tab.|
|Access file|The Access database file that was modified. This published data will only be available when **Access** is selected on the **Connection** tab.|
|Access workgroup information file|The Access workgroup file that is associated with the Access database file. This published data will only be available when **Access** is selected on the **Connection** tab.|

