---
description: include file to detail the release notes for Service Manager 1807
manager:  vvithal
ms.topic: include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center-threshold
ms.technology: service-manager
keywords:
ms.date: 07/24/2018
title: include file
ms.assetid: 5e9ce306-b397-47a8-ba86-a77027bd7ca8
---

## Release Notes for System Center 1807 - Service Manager
The following sections detail the release notes for Service Manager 1807 and include the issues fixed, known issues and workarounds.

## Issues fixed  
The following issues are fixed in SM 1807:

- 	System Center Operations Manager (SCOM) Console and System Center Service Manager (SCSM) Console or PowerShell   components cannot coexist on the same server.
- 	The date and time format in some views is not consistent with the settings on the local computer.
-   SM Console does not release the  memory that is used as soon as the respective window (UI) is closed.
- 	Console might crash (non en-us locale)  when importing a connector as a CSV file.  
- 	Console might crash when it is brought back into focus after it is left out of focus for some time.
- 	Workflow status view was not quickly loading.
- 	Stale reports from Data Warehouse (DW) Cube.
- 	DateDim tables in DWDataMart were not available until 12/31/2050.
-   TargetWarningDate in Service Level Objects (SLO) does not consider the working hours and days as defined in       the associated calendar.
- Self Service Portal requests with attachments, generate erroneous failure messages even after successful generation.
- For synchronizing the active directory connector with a specific domain controller, users cannot  specify the domain controller in the LDAP query of the active directory connector.
-	System Center Configuration Manager 1802 was not supported for Configuration Manager Connectors in Service Manager.

## Known issues and workarounds

### Inconsistent formats for time in some areas
**Description:**
The time format in some views, such as Workitems/IncidentManagement/All Incident, is not consistent with the system local settings. This behavior might occur when you work with the views in unsealed Management Packs (MP).

**Workaround:**
To resolve this issue, follow the steps:

1.	Export the Service Manager Incident Management Configuration Library management pack.
2.	Modify the management pack. Locate the **LastModified** column and modify the binding as shown below:

**Before modification**
<mux:Column Name="lastModified" DisplayMemberBinding="{Binding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

**After modification**
<mux:Column Name="lastModified" DisplayMemberBinding="{datebinding:DateBinding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

1.	Repeat steps 1–2 for columns that are named **LastModified**.
2.	Re-import the modified management pack.
3.	Restart the console.
