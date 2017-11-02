---
title: Service Manager performance
description: Describes how performance for Service Manager server roles and features is affected by different factors.
manager: carmonm
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
ms.assetid: 82f61204-f9f3-492c-9108-ef3edb5ac622
---

# System Center 2016 - Service Manager performance

>Applies To: System Center 2016 - Service Manager

Performance for System Center 2016 - Service Manager server roles and features is affected by different factors. Generally, there are three areas where positive and negative performance is most noticeable in Service Manager:  

-   Service Manager console responsiveness. This is the length of time it takes from the moment you take some sort of action in the console until it completes.  

-   Data insertion time for connectors. This is how long it takes for Service Manager to import data when a connector synchronizes.  

-   Workflow completion time. This is the length of time it takes for workflows to automatically apply some kind of action.  

## Connector performance

Connector initial synchronization can take a significant amount of time, for example, 8 to 12 hours for a large initial synchronization with System Center Configuration Manager. As a connector synchronizes initially, you can expect performance to suffer for all Service Manager server roles and processes during this time. This occurs because of the way that data is inserted sequentially into the Service Manager database, which is a Microsoft SQL Server database. Although you cannot hasten the connector's initial synchronization process, you can plan for the initial synchronization and ensure that the synchronization process completes well before Service Manager is put into production.  

When the initial synchronization is complete, Service Manager continues synchronizing the differences, which does not have a measurable impact on performance.  

## Workflow performance

Workflows are automatic processes that occur. They include sending email notifications, the next step of a change request activating, and automatically applying a template.  

Workflow performance considerations include the following:  

-   Normally, workflows start and finish within one minute. When Service Manager server roles are under a heavy workload, workflows do not complete as quickly as normal.  

-   In addition, when you create new workflows, such as a new notification subscription, additional load is placed on the system. As the number of new workflows that you create increases, the time it takes for each workflow to run also increases.  

When the system is under a heavy load - if, for example, a large number of new incidents are being created and each incident generates many workflows-performance might be negatively affected.  

## Group, queue, and user role impact on performance

You should plan for groups and user roles early. You should create groups sparingly and create them for the smallest scope possible. Then, you should initially populate your database with data from Active Directory Domain Services \(AD DS\), System Center Configuration Manager, and System Center Operations Manager before you create your groups.  

Often, administrators create groups to make sure that users have access to specified groups only. For example, in one scenario you might want to create a subset of incidents, such as incidents that affect computers that are used by human resource personnel. In this scenario, you might want only specific personnel to be able to view or modify the group of Sensitive Servers. Then, to enable this type for access, you would need to create a group for all users and a group for sensitive computers and then ensure that a security role has access to both the All Users and the Sensitive Servers groups. Inevitably, creating a group containing all users results in performance impact because Service Manager frequently checks to determine if there are changes to the group. This check occurs once every 30 seconds, by default. For a very large group, checking for the changes creates a heavy load on the system, and it may slow down response time considerably.  

Solution 1: You can manually specify how often Service Manager checks for group changes by modifying a registry key. For example, if you change the group check frequency from 30 seconds to 10 minutes, you significantly increase performance. However, queues and service level objectives are special kinds of groups that use the same group calculation polling interval. So, increasing the value of the polling interval will result in longer times for queue and service level objective calculations.  

> [!CAUTION]  
>  Incorrectly editing the registry may severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.  

#### To manually specify the group change check interval  

1.  Run Regedit, and navigate to HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\.  

2.  Create a new DWORD value named **GroupCalcPollingIntervalMilliseconds**.  

3.  For its value, specify the interval in milliseconds. The result is multiplied by 6. For example, to set the interval to 10 minutes, type **600000**.  

4.  Restart the System Center Management service.  

Solution 2: You can use a Windows PowerShell script to add objects of a type, such as "Users", to a user role. Essentially, an analyst who is logged on in this role can access all objects that have a type equal to "User". If you use this method, you eliminate the need for a very large group \("All Users"\) and the expensive check that Service Manager performs to determine this group membership. On the Service Manager management server, you can run the following Windows PowerShell script to add the "user" type to a role "RoleName". You will have to modify this example script for your environment.  

#### To run a Windows PowerShell script to add objects to a user role  

-   Modify the following script as necessary, and then run it:  

```  
#  
# Insert a "type" scope in a role  
# Syntax:  
#   AddTypeToRoleScope -server "put_server_name_here" -RoleName "put display name of the role here" -TypeToAdd "put display name of the type to add to scope here"  
#  
# Note:  This is a simple demonstration script without error checking.   
#   

# set script parameter defaults  
param ([String]$Server = "localhost", [String]$RoleName="My Analyst Role", [String]$TypeToAdd="User")  

$a = [reflection.assembly]::LoadWithPartialName("Microsoft.EnterpriseManagement.Core")  

$m = new-object Microsoft.EnterpriseManagement.EnterpriseManagementGroup $Server   

# Get Type object  
#   Note:  If you need to get a list of all available classes related to (for example) "User",   use this command:  
#               $m.EntityTypes.GetClasses() | ?{ $_.Name -like '*user*'} | %{ $_.Name}  
#  
$type = $m.EntityTypes.GetClasses() | ?{ $_.DisplayName -eq $TypeToAdd}  

# Get role object, and insert the type GUID into scope  
$role = $m.Security.GetUserRoles()  | ?{ $_.DisplayName -eq $RoleName}  
$role.Scope.Objects.Add($type.Id)     
$role.Update()  

#   
# Get the value from the database again and validate it is there  
if ( $role.scope.objects.Contains($type.Id) ) {  
    write-host *** Successfully set the scope for role `" $role.DisplayName`" and it now contains all instances of $type.DisplayName `( $type.Name `)  
} else {  
    write-host "There was an error trying to insert the scope into the role."  
}  

```  

## View performance

When you create views, plan on using "typical" classes in the system whenever possible. Most object classes-for example, Incident Management-have two types: "typical" and "advanced". The typical object type contains simple references to a small subset of data that is related to an item. The advanced type contains many complex references to data that are related to an item. Typical types are simple projections; advanced types are complex projections. Most advanced object types are used to populate different fields in forms that you would not normally want to see displayed in a view. Whenever you create a view based on an advanced object type and when you open the view, Service Manager queries the database and a large amount of data is read. However, very little of the retrieved data is actually displayed or used.  

 If you encounter performance problems with the views that you have defined when you use advanced object types in views, switch to using typical types. Or alternatively, you can create your own projection types that contain only the data you need to base a view upon.

## Service Manager database performance

Performance of the Service Manager database is directly affected by various factors, including the number of concurrent Service Manager consoles that are reading or writing data, the group change check interval, and data that is inserted by connectors. More information is available in this document. Here are a few key points:  

-   You should have a minimum of 8 gigabytes \(GB\) of RAM for the management server that hosts the Service Manager database in so that you can have an acceptable response time in typical scenarios.  

-   You should have at least 8 CPU cores on the computer hosting the Service Manager database.  

-   You can achieve better database performance by segregating log files and data files to separate physical disks, if possible. You can achieve further benefits by moving your tempdb to a different physical RAID drive than that of the Service Manager database. Use a RAID 1\+0 disk system to host your Service Manager database, if possible.  

-   Performance can be negatively affected if the Service Manager database is created with a smaller size and it is set to autogrow, especially by small increments.  

 See the Service Manager Sizing Helper tool that is included in the [Service Manager job aids](https://go.microsoft.com/fwlink/p/?LinkID=232378) documentation set \(SM\_job\_aids.zip\) for help in assessing the size of the database, and create the database with a size that is closer to the final size. This will help performance by reducing the amount of times the database has to autogrow.  

 Similarly, all the other best practices for a high\-performing database are applicable, as well. For example, if you can take advantage of a superior disk subsystem, you can benefit from splitting up the groups of tables on respective filegroups and moving them to a different physical drives.  

## Service Manager management server performance

Performance of the Service Manager management server is primarily affected by the number of active concurrent Service Manager consoles. Because all Service Manager roles interact with the management server, consider adding additional management servers if you plan to have a large number of concurrent consoles. You should have 8 GB of RAM for the management server. You should have at least 4 CPU cores per management server, assuming that you have 10 to 12 active consoles per CPU core.  

## Service Manager console performance

Performance of the Service Manager console is primarily affected by the number of forms that your analysts typically have open and the amount of data that is retrieved by views. You should have 4 GB of RAM on the computer where the Service Manager console is installed. If you have views that retrieve a large amount of data, you will need additional RAM. You should have at least a 4\-core CPU for the computer where the Service Manager console is installed. Because the Service Manager console is an end user application, we recommend that you restart it if you see excessive resource consumption. The Service Manager console aggressively caches information in memory, which can contribute to overall memory usage.  

## Service Manager data warehouse database performance

Performance of the data warehouse is directly affected by various factors, including the number of concurrent Service Manager management servers sending data, volume of data stored or the data retention period, rate of data change, and the extraction, transformation, and load \(ETL\) frequency. The amount of data that is stored in the data warehouse increases over time. Ensuring that you archive unnecessary data is important. Another factor that affects data warehouse performance is the BatchSize setting of ETL processes.  

You can achieve better performance by segregating log files and data files to separate physical disks. However, you should avoid placing more than one log file per disk. Similarly, you can achieve better throughput by putting the tempdb on a different physical disk than the other databases. Lastly, you can benefit by placing the different databases on their respective physical disks, as well. Use a RAID 1\+0 disk system to host your data warehouse, if possible. You should generally have a minimum of 8 GB of RAM for the computer where the data warehouse databases are installed. If you have additional data warehouse data sources from Operations Manager or Configuration Manager you should increase the amount of RAM for the databases. You will benefit from more memory on the computer running SQL Server that hosts the data warehouse, and even more so if the Datamart and Repository databases are on the same server. However, if you have 4,000 or fewer computers in your deployment topology, 4 GB is sufficient. You should have at least 8 CPU cores in the computer where the data warehouse database is installed. Additional cores will help both ETL and report performance.  

Performance can be negatively affected if all the databases in the system are created with a smaller size and set to autogrow, especially by small increments. See the Service Manager Sizing Helper tool that is included in the [Service Manager job aids](https://go.microsoft.com/fwlink/p/?LinkID=232378) documentation set \(SM\_job\_aids.zip\) to assess the size of the database and create the database with a size that is closer to the final size, which will help performance by reducing the amount of times that the database has to autogrow.  

Service Manager includes built\-in support for filegroups. You can benefit from this by placing the filegroups on separate hard drives. For more information about filegroup best practices, see the SQL Server documentation.  

## Service Manager data warehouse server performance

Performance of the data warehouse server is affected by the number of Service Manager management servers that are registered to the data warehouse, the size of your deployment, and the number of data sources. You should generally have a minimum of 8 GB of RAM for the data warehouse server. However, performance will benefit by having additional memory for advanced deployment scenarios where more than one Service Manager management server inserts data into the data warehouse. If you must trade off performance, your highest priority should be for memory for the computer running SQL Server. You should have at least 8 CPU cores to prevent performance problems.  

## Self Service portal performance

The Self-Service Portal is designed for easy access to incident and service request filing. It is not designed to handle thousands of users simultaneously.  

Performance testing for the Self-Service Portal was focused on typical "Monday morning" scenarios-specifically, to ensure that on Monday morning hundreds of users can log in within a span of 5 to 10 minutes and open incidents with acceptable \(less than 4\-to\-5 second\) response times. This goal was achieved with the minimum hardware recommended in this document.  

## Service-level objective performance

There is no specific number of service\-level objectives that Service Manager supports. For example, if an organization typically has few incidents, it can support more service\-level objectives than it might otherwise be capable of. However, a larger incident volume might necessitate either fewer service\-level objectives or a scale\-out of additional hardware and software, as appropriate. We recommend that you create no more than five service\-level objectives for a typical 50,000\-computer Service Manager configuration. You could possibly create more service\-level objectives. However, because conditions vary greatly from organization to organization, Microsoft cannot provide a concrete recommendation for the number of service\-level objectives that you should not exceed. If your deployment configuration suffers from poor performance as a result of the number of service\-level objectives, we recommend that you scale out using the next\-larger deployment scenario, as described in the [Configurations for Deployment Scenarios](deploy-topo-scenarios.md) article of this guide.

## Next steps

- Review [Recommended deployment topology scenarios](deploy-topo-scenarios.md) to learn about hardware and software configurations for Service Manager deployment scenarios.
