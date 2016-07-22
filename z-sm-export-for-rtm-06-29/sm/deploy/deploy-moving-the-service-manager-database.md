---
title: Moving the Service Manager Database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04f4671d-2fd1-4638-a64f-4543e013e541
 

















---
# Moving the Service Manager Database
You must use the following high\-level steps to move the Service Manager database.  
  
> [!NOTE]  
>  These steps link to content in the Service Manager Upgrade Guide.  
  
1.  Open the inbound SQL Port on new Service Manager database server. The default port is 1433.  
  
2.  Stop the System Center services on all the management servers, as described in [How to Stop Service Manager Services on the Secondary Management Server](http://technet.microsoft.com/library/jj900194.aspx).  
  
3.  Back up the Service Manager database, as described in [How to Back Up the Production Service Manager Database](http://technet.microsoft.com/library/jj900185.aspx).  
  
4.  Restore the Service Manager database on the target computer that is running Microsoft SQL Server, as described in [How to Restore the Service Manager Database in the Lab Environment](http://technet.microsoft.com/library/jj900192.aspx).  
  
5.  Configure the Service Manager database, as described in [How to Prepare the Service Manager Database in the Lab Environment](http://technet.microsoft.com/library/jj900187.aspx).  
  
    > [!IMPORTANT]  
    >  Do not perform step 17 in the procedure for configuring tables.  
  
6.  After you move the ServiceManager database, ensure that you manually change all the Service Manager database and data warehouse registration information in the DWStagingAndConfig database. Old information about where the ServiceManager database is located remains in the DWStagingAndConfig database in the following tables:  
  
    -   MT\_Microsoft$Systemcenter$Datawarehouse$CMDBSource  
  
        -   In the corresponding entry with DataSourceName\_GUID \= \<Service Manager Data Source Name\>, change the field DatabaseServer\_GUID with the new name of the SQLServer\\Instance where the ServiceManager database has moved to.  
  
    -   MT\_Microsoft$Systemcenter$ResourceAccessLayer$SqlResourceStore  
  
        -   In the corresponding entry with DataService\_GUID \= ServiceManager, change the field Server\_GUID to the new name of the SQLServer\\Instance where the ServiceManager database has moved to.  
  
7.  Configure the registry on all the management servers that will access the new SQL Server instance, by using the following steps:  
  
    1.  Open Registry Editor.  
  
    2.  Browse to **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\System Center\\2010\\Common\\Database**.  
  
    3.  Configure two keys: one for the server name \(DatabaseServerName\) and one for the database name \(DatabaseName\). Set values to the new server name and database name, if they are different from the original values.  
  
8.  If you are also upgrading the SQL server while moving, then upgrade the following SQL Server prerequisites for the Service Manager Management server. There are 2 SQL Server prerequisites:  
  
    -   SQL Native Client  
  
    -   Analysis Management Objects \(AMO\)  
  
9. Start the System Center services on all the management servers, as described in [How to Start Service Manager Services on the Secondary Management Server](http://technet.microsoft.com/library/jj900196.aspx).  
  
10. Install another Service Manager database that has a different name on the same computer that is running SQL Server, by installing another Service Manager management server and choosing to create a new database. This step will populate the master database with error message text so that if an error occurs in the future, the error message can describe the specific problem instead of displaying generic text. After the database is installed, you can drop it from the computer that is running SQL Server and uninstall the additional, temporary management server.  
  
     \-Or\-  
  
     Run the following query on the source Service Manager database server and copy the output script and then run it on new Service Manager database server.  
  
    ```  
    DECLARE @crlf char(2);  
    DECLARE @tab char(1);  
    SET @crlf = CHAR(13) + CHAR(10);  
    SET @tab = CHAR(9);  
  
    SELECT   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 'EXEC sp_addmessage ' + @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@msgnum = ' + CAST(m.message_id AS varchar(30))  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + ', ' + @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@severity = ' + CAST(m.severity AS varchar(3))&nbsp;   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ ', ' + @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@msgtext = N''' + REPLACE(m.[text],'''','''''')&nbsp;   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ ''''&nbsp; + ', ' + @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@lang = ''' +   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (SELECT TOP 1 alias   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM master.sys.syslanguages l   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE l.lcid = m.language_id)   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ ''', ' + @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@with_log = ''' +   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CASE WHEN m.is_event_logged = 1   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;THEN 'TRUE' ELSE 'FALSE' END&nbsp;&nbsp; + ''', ' +&nbsp; @crlf + @tab  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; -- Uncomment ONLY if you want to replace:  
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + '@replace = ''replace'';'   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ @crlf + 'GO' + @crlf + @crlf   
    FROM   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;master.sys.messages m  
    WHERE   
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;m.message_id > 50000;  
  
    GO  
  
    ```  
  
## See Also  
 [Appendix B \- Guidance for Moving the Service Manager and Data Warehouse Databases](../../../sm/deploy/deploy-guide/Appendix-B---Guidance-for-Moving-the-Service-Manager-and-Data-Warehouse-Databases.md)
