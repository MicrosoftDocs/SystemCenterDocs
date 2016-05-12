---
title: Install with the Orchestrator Command Line Install Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 405babd5-7790-4bc8-84d2-3d2127f3e8a6
---
# Install with the Orchestrator Command Line Install Tool
To install [!INCLUDE[orchshort](Token/orchshort_md.md)] at a command prompt, use Setup.exe with the command\-line options in the following table.

|Option|Description|
|----------|---------------|
|\/Silent|Installation is performed without displaying a dialog box.|
|\/Uninstall|Product is uninstalled. This option is performed silently.|
|\/Key:\[Product Key\]|Specifies the product key. If no product key is specified, [!INCLUDE[orchshort](Token/orchshort_md.md)] is installed as an evaluation edition.|
|\/ServiceUserName:\[User Name\]|Specifies the user account for the [!INCLUDE[orchshort](Token/orchshort_md.md)] Management Service. This value is required if you are installing Management Server, Runbook Server, or web services.|
|\/ServicePassword:\[Password\]|Specifies the password for the user account for the [!INCLUDE[orchshort](Token/orchshort_md.md)] Management Service. This value is required if you are installing Management Server, Runbook Server, or web services.|
|\/Components:\[Feature 1, Feature 2,…\]|Specifies the features to install. Possible values are ManagementServer, RunbookServer, RunbookDesigner, WebComponents, and All.|
|\/InstallDir:\[Path\]|Specifies the path to install [!INCLUDE[orchshort](Token/orchshort_md.md)]. If no path is specified, C:\\Program Files \(x86\)\\Microsoft System Center 2012\\Orchestrator is used.|
|\/DbServer:\[Computer\[\\Instance\]\]|Specifies the computer name and instance of the database server. This value is required if you are installing Management Server, Runbook Server, or web services.|
|\/DbUser:\[User Name\]|Specifies the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, no value should be specified.|
|\/DbPassword:\[Password\]|Specifies the password for the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, then no value should be specified.|
|\/DbNameNew:\[Database Name\]|Specifies the database name if a new database is being created. Cannot be used with DbNameExisting.|
|\/DbNameExisting:\[Database Name\]|Specifies the database name if an existing database is being used. Cannot be used with DbNameNew.|
|\/WebServicePort:\[Port\]|Specifies the port to use for the web service. Required if web services are installed.|
|\/WebConsolePort:\[Port\]|Specifies the port to use for the [!INCLUDE[orchshort](Token/orchshort_md.md)] console. Required if web services are installed.|
|\/OrchestratorUsersGroup:\[Group SID\]|Specifies the SID of the domain or local group that will be granted access to Management server. If no value is specified, the default local group is used.|
|\/OrchestratorRemote|Specifies that remote access should be granted to the Runbook Designer.|
|\/UseMicrosoftUpdate:\[0&#124;1\]|Specifies whether to opt in for Microsoft Update. A value of 1 will opt in. A value of 0 does not change the current opt in status of the computer.|
|\/SendCEIPReports:\[0&#124;1\]|Specifies that [!INCLUDE[orchshort](Token/orchshort_md.md)] should send CEIP \(Customer Experience Improvement Program\) reports to Microsoft. A value of 1 opts in. A value of 0 does not change the current opt\-in status of the computer.|
|\/EnableErrorReporting:\[value\]|Specifies that [!INCLUDE[orchshort](Token/orchshort_md.md)] should send program error reports to Microsoft. Possible values are always, queued, and never.|

For example, you could use the following command to install all of the [!INCLUDE[orchshort](Token/orchshort_md.md)] components using Windows Authentication.

```
.\Setup.exe /Silent /ServiceUserName:<UserName> /ServicePassword:<password> /Components:All /DbServer:<DBServerName> /DbNameNew:Orchestrator /WebServicePort:81 /WebConsolePort:82 /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always
```

## See Also
[Install Orchestrator](Install-Orchestrator.md)


