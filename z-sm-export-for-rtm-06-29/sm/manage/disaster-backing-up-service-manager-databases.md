---
title: Backing Up Service Manager Databases
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68f6b035-4085-4348-8247-3b31ae85f125
 

















---
# Backing Up Service Manager Databases
There are up to eight databases in a System Center 2012 - Service Manager environment:  
  
-   ServiceManager  
  
-   DWDataMart  
  
-   DWRepository  
  
-   DWStagingAndConfig  
  
-   ReportServer  
  
-   Analyst  
  
-   OMDWDataMart  
  
-   CMDWDataMart  
  
 The first four databases in this list need to connect and exchange data with the Service Manager and data warehouse management servers. Data is encrypted during these exchanges. On the management servers, the encryption keys are backed up and restored as necessary, as explained in this guide. For more information about the encryption keys on the management servers, see [Backing Up Service Manager Management Servers](../../../sm/manage/disaster/Backing-Up-Service-Manager-Management-Servers.md). For the servers that host databases, the encryption keys are stored in the databases themselves.  
  
 If a computer that hosts a database fails, all you need for recovery is the ability to restore the databases, which include the encryption keys, to a computer with the same name as the original computer. Your disaster recovery strategy for the Service Manager databases should be based on procedures for general SQL&nbsp;Server&nbsp;2008 disaster recovery. For more information, see [SQL Server 2008 R2 Books Online: Planning for Disaster Recovery](http://go.microsoft.com/fwlink/p/?LinkID=131016).  
  
 As part of your disaster recovery preparation, you run a script to capture the Security log to preserve user role information for each database. After you deploy Service Manager and, if necessary, run the Data Warehouse Registration Wizard, you use the SQL&nbsp;Server Script Wizard to create a script that captures SQL&nbsp;Server logon permissions and object\-level permissions. Then, if you need to restore a new server for the Service Manager databases, you can use this script to recreate the necessary logon permissions and object\-level permissions. The wizard that is used to generate scripts in SQL&nbsp;Server&nbsp;2008 differs from the wizard in SQL&nbsp;Server&nbsp;2008&nbsp;R2. Instructions for both the SQL&nbsp;Server&nbsp;2008 wizard and the SQL&nbsp;Server&nbsp;2008&nbsp;R2 wizard are presented in this guide.  
  
## Enable Common Language Runtime on SQL&nbsp;Server  
 During installation of the Service Manager database, Service Manager Setup enables common language runtime \(CLR\) on the computer that is running SQL&nbsp;Server. If you restore a Service Manager database to another computer running SQL&nbsp;Server, you must enable CLR manually. For more information, see [Enabling CLR Integration](http://go.microsoft.com/fwlink/p/?LinkId=217932).  
  
## In This Section  
 [How to Start the SQL Server 2008 Script Wizard](../../../sm/manage/disaster/How-to-Start-the-SQL-Server-2008-Script-Wizard.md)  
 Describes how to generate a script to capture SQL&nbsp;Server&nbsp;2008 logon permissions and object\-level permissions.  
  
 [How to Start the SQL Server 2008 R2 Script Wizard](../../../sm/manage/disaster/How-to-Start-the-SQL-Server-2008-R2-Script-Wizard.md)  
 Describes how to generate a script to capture SQL&nbsp;Server&nbsp;2008&nbsp;R2 logon permissions and object\-level permissions.
