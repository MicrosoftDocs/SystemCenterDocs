---
title: Query Database 
description: This article describes the Query Database activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/14/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 65d32c6e-5ac0-4672-9c8b-57d8b12af8f4
caps.latest.revision: 19
author: Jeronika-MS
ms.author: v-gajeronika
---
# Query Database

The Query Database activity queries a database and returns the resulting rows as published data. This activity supports the following database types:  

- Access  

- ODBC  

- Oracle  

- SQL Server  

The Query Database activity can be used to query a database for the detailed description of an error code that has appeared on one of the systems in the data center and then that description is sent to an administrator in an email message.  

## Configure the Query Database Activity

 Before you configure the Query Database activity you'll need to determine the following:  

- The database that you're connecting to  

- The SQL query that you're running  

Use the following information to configure the Query Database activity.  

### Details  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Query**|Enter the SQL query in the **Query** field|  

> [!WARNING]
> The Query Database activity does not support queries that return data as XML, such as queries that use the **FOR XML** clause in SQL Server.  

### Connection

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Database type**|Select the **Database type** from the drop-down list. The options include the following:<br /><br /> -   Access<br />-   ODBC<br />-   Oracle<br />-   SQL Server|  

> [!IMPORTANT]
> When Orchestrator is installed on a non-English operating system, and you set the **Connection** for **Database type** to **SQL Server**, the Server input value cannot be **localhost**. You must use the actual computer name.  

 Configuration instructions for each **Connection** tab **Database type** are listed in the following tables.  

### [Access Connections](#tab/access-connections)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the name of the **Access** database file that you want to access.|  
|**Workgroup file**|Enter the name of the **Access** workgroup file that is associated with this database.|  
|**User name**|Enter the user name for the workgroup file.|  
|**Password**|Enter the password for the workgroup file.|  
|**DB password**|Enter the password for the Access database.|  

### [ODBC Connections](#tab/odbc-connections)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**DSN**|Enter the data source name.|  
|**User name**|Enter the user name for this database.|  
|**Password**|Enter the password for this database.|  

### [Oracle Connections](#tab/oracle-connections)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Service Name**|Enter the service name.|  
|**User name**|Enter the user name for this database.|  
|**Password**|Enter the password for this database.|  

### [SQL Server Connections](#tab/sql-server-connections)

::: moniker range="sc-orch-2025"

>[!NOTE]
>MSOLEDB19 Driver is used to establish encrypted connections to the SQL Server (by default). If the SQL server certificate isn't **Trusted** on the Orchestrator machine,  enter *Server=\<serverName\>;Trust Server Certificate=True* for every configuration. [Learn more](/SystemCenterDocs/orchestrator/install.md#secure-connection-to-sql-server) to install a SQL Server certificate.

::: moniker-end

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Authentication**|Select either **Windows Authentication** or **SQL Server Authentication**.|  
|**Server**|Enter the name of the SQL Server that you want to access.|  
|**Initial catalog**|Enter the name of the initial catalog.<br /><br /> If you selected the **SQL Server Authentication** option, enter the user name and password used to access the SQL Server in the **User name** and **Password** boxes.|  

---

### Timeout

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Timeout**|Enter the amount of time that the Query Database activity will wait for the database operation to complete.<br /><br /> Set this value to `0` to wait indefinitely.|  

### Security Credentials

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Use the security of the account assigned to the service**|Select this option if you want to run the Query Database activity using the same account that the runbook server uses.|  
|**This account**|Use this option to specify a different account. Enter the **User name** and **Password**. **Note:**  If you specify an invalid user name or password, the account assigned to the runbook server will be used to run the activity.|  

### Published Data

The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Numeric return value of the query|When a query that returns a numeric value is used, this will be the value. For example, "Select COUNT(*) where FirstName=John"|  
|Database query|The database query that was sent to the database.|  
|Initial Catalog|The initial catalog that was used when connecting to the database. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|  
|Database server|The name of the database server. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|  
|Database user|The name of the user used to connect to the database server.|  
|ODBC DSN|The name of the ODBC DSN. This published data will only be available when **ODBC** is selected on the **Connection** tab.|  
|Oracle Service Name|The service name. This published data will only be available when **Oracle** is selected on the **Connection** tab.|  
|Access file|The Access database file that was queried. This published data will only be available when **Access** is selected on the **Connection** tab.|  
|Access workgroup information file|The Access workgroup file that is associated with the Access database file. This published data will only be available when **Access** is selected on the **Connection** tab.|  
|For each row published|
|Full line as a string with fields separated by `;`|The entire row that was published with each field in the row separated by a semi-colon (;). Use the **Field** data manipulation function to obtain the values of a field within the row.|
