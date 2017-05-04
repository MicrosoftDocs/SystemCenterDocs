---
title: Resolve System Center 2016 - Service Manager upgrade problems
description: This article helps you resolve System Center 2016 - Service Manager upgrade problems and work around them.
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
ms.assetid: 41d83462-5e56-4eb3-8eb8-b67d34060c86
---

# Identify and resolve System Center 2016 - Service Manager upgrade problems

>Applies To: System Center 2016 - Service Manager

An upgrade to System Center 2016 – Service Manager might not complete successfully. There are five phases of the upgrade where a failure might occur. The steps that you take to recover from a failed upgrade depend on the phase in which the failure occurs:

- Failure occurs during the prerequisite check.
- Failure occurs during predicted checks.
- Failure occurs in an unpredictable manner before permanent changes are made to a management server.
- Failure occurs in an unpredictable manner after permanent changes are made to a management server.
- Failure occurs in an unpredictable manner after permanent changes are made to the database.
- The upgrade might also fail as a result of Configuration service Startup timing out.

You can also work around configuration service startup issues after a failed upgrade.

## Failure occurs during a prerequisite check

Before the installation of System Center 2016 – Service Manager begins, a prerequisite check is made for certain requirements. If a condition is found in which Service Manager will continue to function, you receive a warning. Warnings are identified with an explanation point (!) in a yellow triangle. Conditions that have been identified as a Warning will not prevent you from installing Service Manager.

If a condition is found that is an absolute requirement for Service Manager, a failure indication appears. Failure indications are identified with an X in a red circle.

If either a warning or a failure indication appears, you can either cancel the installation and make the necessary changes, or make the appropriate changes and then click **Check prerequisites again** and continue with the installation. All failure conditions must be corrected before the installation or upgrade can proceed.


## Failure occurs during predicted checks

After any failures that were identified during the prerequisite check are corrected, pressing **Next** on the **Prerequisites** page starts the upgrade or installation of Service Manager. The system checks for the following conditions during the installation or upgrade process:

- The data warehouse database that you specified exists.
- The computer running SQL Server that you specified is not running a supported SQL Server version.
- The hard disk drive that you specified for a database has at least 1 GB of free space.
- The System Center Data Access service can log on with the set of credentials that you supplied.
- The System Center Management Configuration service can log on with the set of credentials you supplied.
- There is enough free disk space to install the upgraded files.
- Setup can access the file location for the Service Manager installation.

If failures occur during these types of checks, you can make the appropriate changes. For example, specify a hard disk location with sufficient space, and then on the Warning page, click **Retry** to continue the installation.


## Failure occurs in an unpredictable manner before permanent changes are made to the Management Server

During an installation or upgrade of Service Manager, an error may occur. If the error occurs before any permanent changes are made to the Service Manager management server or data warehouse management server—for example, before changes are made to the Structured Query Language (SQL) database or before management packs are imported—the error message that appears includes a **Retry** button. In these situations, you can correct the issue and then retry the installation or upgrade.


## Failure occurs in an unpredictable manner after permanent changes are made to the Management Server

If an error occurs after permanent changes are made to the Service Manager management server or data warehouse management server—for example, after changes are made to the SQL database or after management packs are imported—the error message that appears does not include a Retry button. In this situation, you must reinstall the original version of the affected management server.

In any case, you need the backup of the encryption key. For the Service Manager management server, the encryption key is available only if you made a backup before you started the upgrade. For more information, see "Back Up the Encryption Key" in the Disaster Recovery Guide for Service Manager.

## Failure occurs in an unpredictable manner after permanent changes are made to a database

If an error occurs after permanent changes have been made—for example, after management packs are imported or any other time data is written into a database—the error message that appears does not include a Retry button.

At this point your only option is to click **Close** and begin a disaster recovery process to restore your databases. This recovery is possible only if you backed up your databases before you started the upgrade process. For more information, see "Backing Up Service Manager Databases" in the Disaster Recovery Guide for Service Manager.

## Upgrade fails as a result of the Configuration service startup timing-out

On some computers, Service Manager Setup fails and rolls back if it cannot start the System Center Management Configuration service in a timely fashion. If this problem occurs, you might see the following entries in the install log:

```
CAStartServices: Attempting to start service. OMCFG

CAStartServices: StartService failed. Error Code: 0x8007041D.

ConfigureSDKConfigService: CAStartServices failed. Error Code: 0x8007041D. OMCFG
```

Error 0x8007041D indicates that the service did not respond to the start or control request in a timely fashion. In addition, the following event may be logged in the System Event log:

```
Log Name:      System
Source:        Service Control Manager
Event ID:      7009
Task Category: None
Level:         Error
Keywords:      Classic
User:          N/A
Description:
A timeout was reached (30000 milliseconds) while waiting for the System Center Management Configuration service to connect.
```

This problem occurs because a .NET Framework 2.0 managed assembly that has an Authenticode signature takes longer than usual to load. The signature is always verified when the .NET Framework 2.0 managed assembly that has an Authenticode signature is loaded. In addition, the .NET Framework 2.0 managed assembly may take longer than usual to load because of various other settings. For example, the .NET Framework 2.0 managed assembly may take longer than usual to load because of the network configuration.

For additional information about the cause of this problem, see [Knowledgebase Article 936707](http://go.microsoft.com/fwlink/p/?LinkId=207190) in the Microsoft Knowledge Base.

## Work around configuration service startup issues after a failed upgrade

There are two workaround procedures that you can use to try to resolve the issue in which an upgrade to System Center 2016 - Service Manager fails as a result of Configuration service Startup timing out. You can:  

-   Disable signature verification on the computer that is running Setup.  

-   Increase the service time\-out setting on the computer that is running Setup.  

### To disable signature verification  

1.  On the computer that is running Setup, edit the Microsoft.Mom.ConfigServiceHost.exe.config file, which is located in the Program Files\\Microsoft System Center 2016\\Service Manager folder.  

2.  In the `<runtime> </runtime>` section, add `<generatePublisherEvidence enabled="false">`.  

3.  Save the changes to the file.  

4.  Attempt the upgrade again.  

### To increase the service time\-out setting  

1.  On the computer that is running Setup, create the following registry value to increase the service time\-out period:  

    ```  
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control   
    ServicesPipeTimeout  
    DWORD  
    200000  

    ```  

    > [!CAUTION]  
    >  Incorrectly editing the registry may severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.  

    > [!NOTE]  
    >  You may have to increase this value further if the service still fails to start. The value in this example is in milliseconds. For additional details about the registry key, see [article 922918](http://go.microsoft.com/fwlink/p/?LinkId=207191) in the Microsoft Knowledge Base.  

2.  Start the computer again.  

3.  Attempt the upgrade again.
