---
title: Write to Database 
description: This article describes the Write to Database activity that writes a row into a database table.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 08/13/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 0e47a137-5f4b-41a2-a13a-59bcaae8e750
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Write to Database

The Write to Database activity writes a row into a database table. This activity interacts with the following databases:  

- Access  

- ODBC  

- Oracle  

- SQL Server  

The Write to Database activity can be used to replicate important Windows Event Log Events to a database table that is able to be queried and maintained.  

## Configure the Write to Database Activity

 Before you configure the Write to Database activity, you need to determine the following:  

- The database you're connecting to.  

- The table and fields you're updating.  

Use the following information to configure the Write to Database activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Table name**|Enter the name of the database table that you're adding the row to.|  
|**Data**|The list displays all the fields in the table that will be set. To add a field, select **Add** and enter the **Field name** and **Value**. To remove a field, select it, and select **Remove**. To edit a field, double-click the field name.|  

### Connection Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Database type**|Select the **Database type** from the dropdown list. The options include the following:<br /><br /> -   Access<br />-   ODBC<br />-   Oracle<br />-   SQL Server<br /><br /> Configuration instructions for each **Connection** tab **Database type** are listed in the following tables.|  

### Access Connections Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the name of the **Access** database file that you want to access.|  
|**Workgroup file**|Enter the name of the **Access** workgroup file that is associated with this database.|  
|**User name**|Enter the user name for the workgroup file.|  
|**Password**|Enter the password for the workgroup file.|  
|**DB password**|Enter the password for the Access database.|  

### ODBC Connections Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**DSN**|Enter the data source name.|  
|**User name**|Enter the user name for this database.|  
|**Password**|Enter the password for this database.|  

### Oracle Connections Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Service Name**|Enter the service name.|  
|**User name**|Enter the user name for this database.|  
|**Password**|Enter the password for this database.|  

### SQL Server Connections Tab

::: moniker range="sc-orch-2025"

>[!Note]
>MSOLEDB19 Driver is used to establish encrypted connections to the SQL Server (by default). If the SQL server certificate isn't **Trusted** on the Orchestrator RunbookWorker machine,  enter *Server=\<serverName\>;Trust Server Certificate=True* for every configuration. [Learn more](/system-center/orchestrator/install?view=sc-orch-2025#secure-connection-to-sql-server&preserve-view=true) to install a SQL Server certificate.

::: moniker-end

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Authentication**|Select either **Windows Authentication** or **SQL Server Authentication**.|  
|**Server**|Enter the name of the SQL Server that you want to access.|  
|**Initial catalog**|Enter the name of the initial catalog.<br /><br /> If you selected the **SQL Server Authentication** option, enter the user name and password used to access the SQL Server in the **User name** and **Password** boxes.|  

### Timeout Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Timeout**|Enter the amount of time that the Query Database activity will wait for the database operation to complete.<br /><br /> Set this value to `0` to wait indefinitely.|  

### Security Credentials Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Use the security of the account assigned to the service**|Select this option if you want to run the Query Database activity using the same account that the runbook server uses.|  
|**This account**|Use this option to specify a different account. Enter the **User name** and **Password**. **Note:**  If you specify an invalid user name or password, the account assigned to the runbook server will be used to run the activity.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Initial Catalog|The initial catalog that was used when connecting to the database. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|  
|Database server|The name of the database server. This published data will only be available when **SQL Server** is selected on the **Connection** tab.|  
|Table name|The name of the table that was written to.|  
|Database user|The name of the user used to connect to the database server.|  
|ODBC DSN|The name of the ODBC DSN. This published data will only be available when **ODBC** is selected on the **Connection** tab.|  
|Oracle Service Name|The service name. This published data will only be available when **Oracle** is selected on the **Connection** tab.|  
|Access file|The Access database file that was modified. This published data will only be available when **Access** is selected on the **Connection** tab.|  
|Access workgroup information file|The Access workgroup file that is associated with the Access database file. This published data will only be available when **Access** is selected on the **Connection** tab.|
