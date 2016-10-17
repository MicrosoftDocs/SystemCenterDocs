---
title: Deploying Service Manager from a Command Line
manager:  cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27c60668-1baf-4521-98ad-cf87389c8310
---

# Deploying Service Manager from a Command Line

>Applies To: System Center 2016 - Service Manager


This section describes how to deploy System Center - Service Manager using command\-line parameters. For easier reading, the command\-line examples in this guide list each command\-line parameter on its own line. If you copy these examples, you must remove the carriage returns\/line\-feeds \(CRs\/LFs\) from each line before you can run the commands.  

> [!NOTE]  
>  The **/silent** parameter must be the last parameter used in a command\-line install.  

 In this guide, the command\-line arguments that you provide are delineated by brackets: \[\]. For example, you provide the Registered Owner's name **\[owners name\]** and Registered Organization's name **\[company name\]** as shown in the following example:  

```  
Setup.exe  
/Install:Datawarehouse  
/RegisteredOwner:[owners name]  
/RegisteredOrganization:[company name]   
/Silent  

```  

 If your command\-line argument contains a space-for example, **\[owners name\]**-enclose the argument in double quotation marks. For example, if you use **Garret Young** as the argument for the **RegisteredOwner** command\-line parameter, type the name as shown in the following example:  

```  
/RegisteredOwner:"Garret Young"  
```  

 Some of the command\-line parameters that are used for the Operations Manager and Configuration Manager data marts define Structured Query Language \(SQL\) path statements as command\-line arguments. You must define the drive name and make sure that the path that is listed in this guide is the correct path for your version of Microsoft SQL&nbsp;Server. The examples in this guide are correct for SQL&nbsp;Server&nbsp;2016, as shown in the following example:  

```  
/OMDataMartDatabaseLogFilePath:[drive name]\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA  
```  



 For additional information about command\-line parameters, type **setup.exe /?**. The parameters in the following table are optional.  

|command|notes|  
|---|---|  
|**/ProductKey**|If this parameter is omitted, Service Manager is installed as an evaluation edition with an evaluation period of 180 days.|  
|**/Installpath**|If this parameter is omitted, Service Manager is installed in the default folder and path:<br /><br /> \[drive name\]:\\Program Files\\Microsoft System Center\\Service Manager 2016.|  
|**/ServiceRunUnderAccount**|If this parameter is omitted, the local system account is used.|  
|**/WorkflowAccount**|If this parameter is omitted, the local system account is used.|  

### Before you run the command line  
 To help prevent an installation failure, perform the following steps on the computer where you will be installing Service Manager:  

1.  Run the UI\-based Setup up to the point where you run the prerequisite checker. Make sure that the prerequisite checker passes, or at least passes with a warning.  

2.  On the computer where you will be installing the reporting server, make sure that the SQL&nbsp;Server Reporting Services \(SSRS\) service has started.  

3.  If you are going to deploy the Reporting Server on a computer other than the computer hosting the data warehouse management server, make sure that you have completed the procedure in [Manual Steps to Configure the Remote SQL Server Reporting Services](deploy-manual-steps-to-configure-the-remote-sql-server-reporting-services.md).  

### Determining When Installation Is Complete  
 When installation of either the Service Manager management server or the data warehouse management server is complete, an event with Event&nbsp;ID&nbsp;1033 is written into the Application Event log, as shown in the following illustration.  

 ![Command Line Install Event Log](../media/deploy-commandlineinstalleventlog.png)  


 If you use the **start \/w** command when you are using setup.exe, the command window will remain open when Setup completes, giving you the opportunity to examine any return codes.  

### Checking Error Codes  
 When the command\-line Setup is complete, the command prompt appears. You can view the error code that was returned by typing **echo %errorlevel%**. An error code of 0 means that the installation was successful. The error codes that could be returned by the command\-line installation are listed in [Appendix A \- Command\-Line Option Error Codes](deploy-appendix-a-command-line-option-error-codes.md) in this guide.  

 The command\-line installation will not check the database name that you supply to see if it already exists. If you supply a database name that already exists, the command\-line installation will fail and a \-1 will be returned as an error code.  

## Deploy a Service Manager Management Server Using the Command Line

You can use the following command\-line procedures to deploy the Service Manager management server and the Service Manager database.  

### To deploy the Service Manager management server and database on one computer  

1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  

2.  Open the command window.  

3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  

    ```  
    Start /Wait   
    Setup.exe   
    /Install:Server   
    /AcceptEula:[YES/NO]   
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /CreateNewDatabase   
    /ManagementGroupName:[management group name]   
    /AdminRoleGroup:[domain\account name]   
    /ServiceRunUnderAccount:[domain\account name\password]   
    /WorkflowAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]   

    /Silent  

    ```  

## Deploy a Data Warehouse Management Server Using the Command Line

Use the following procedures to deploy a Service Manager data warehouse and databases, including the Operations Manager and Configuration Manager data mart databases, in System Center - Service Manager.  

## Deploying the Data Warehouse  
 Use the following procedures to deploy the data warehouse with the Operations Manager and Configuration Manager data mart databases. If you want to install the data warehouse management server and data warehouse databases on the same computer, use the same computer name that you are running Setup on for all instances of **\[computer name\]**. If you want to deploy the databases on a separate computer, adjust the **\[computer name\]** entries accordingly.  

 The **/AnalysisServerDatabaseDataFilePath** is optional, and if it is not used, the default path will be used.  

 The DWStagingAndConfig database and the DWRepository database must reside on the same instance. Make sure that you specify the same computer and instance for the **/StgConfigSqlServerInstance** and **/RepositorySqlServerInstance** command\-line options.  

#### To deploy the data warehouse management server, data warehouse databases, and optional data marts  

1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  

2.  Open a command window.  

    > [!NOTE]  
    >  You must run the command prompt with administrative credentials.  

3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  

    ```  
    Start /Wait   
    Setup.exe   
    /Install:Datawarehouse   
    /AcceptEula:[YES/NO]   
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /CreateNewDatabase   
    /AdminRoleGroup:[domain\account name]   
    /StgConfigSqlServerInstance:[computer name]   
    /RepositorySqlServerInstance:[computer name]   
    /DataMartSqlServerInstance:[computer name]   
    /ReportingServer:[computer name]   
    /ReportingWebServiceURL:"http://[computer name]:80/ReportServer"   
    /ServiceRunUnderAccount:[domain\account name\password]   
    /DatasourceAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]   
    /ManagementGroupName:DW_improvement   
    /OMDataMartSqlServerInstance:[computer name]   
    /CMDataMartSqlServerInstance:[computer name]   
    /AnalysisServerInstance:[computer name]   
    /AnalysisServerDatabaseDataFilePath:[path to analysis database]   
    /ASRunUnderAccount:[domain\account name\password]   
    /Silent  
    ```  

## Deploy a Service Manager Console Using the Command Line

Use the following command\-line procedure to deploy the Service Manager console in System Center - Service Manager.  

### To deploy the Service Manager console  

1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  

2.  Open a command window.  

3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  

    ```  
    Start /Wait   
    Setup.exe   
    /Install:Console   
    /AcceptEula:[YES/NO]  
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /Installpath:[drive name]\Program Files\Microsoft System Center\Service Manager 2016   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]  

    /Silent  
    ```  
