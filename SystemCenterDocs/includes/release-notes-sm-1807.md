---
description: include file to detail the release notes for Service Manager 1807
ms.topic: include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service:  system-center
ms.subservice: service-manager
keywords:
ms.date: 07/24/2018
title: include file
ms.assetid: 5e9ce306-b397-47a8-ba86-a77027bd7ca8
---

## Release Notes for System Center 1807 - Service Manager
The following sections detail the release notes for Service Manager 1807 and include the issues fixed, known issues and workarounds.

## Issues fixed  
The following issues are fixed in SM 1807:

- System Center Operations Manager (SCOM) console and System Center Service Manager (SCSM) console or PowerShell components cannot coexist on the same server.

  >[!NOTE]
  > You must install Operations Manager 1807 to resolve this.

- The date and time format in some views isn't consistent with the settings on the local computer.
- SM Console doesn't release the  memory that is used as soon as the respective window (UI) is closed.
- Console might crash (non en-us locale)  when importing a connector as a CSV file.  
- Console might crash when it's brought back into focus after it's left out of focus for some time.
- Workflow status view wasn't quickly loading.
- Stale reports from Data Warehouse (DW) Cube.
- DateDim tables in DWDataMart were not available until 12/31/2050.
- TargetWarningDate in Service Level Objects (SLO) doesn't consider the working hours and days, as defined in the associated calendar.
- Self service portal requests that contain attachments, generate erroneous failure messages even after successful generation.
- For synchronizing the active directory connector with a specific domain controller, users can't specify the domain controller in the LDAP query of the active directory connector.
- System Center Configuration Manager 1802 wasn't supported for Configuration Manager Connectors in Service Manager.

## Known issues and workarounds

### Inconsistent formats for time in some areas
**Description:**
The time format in some views, such as Workitems/IncidentManagement/All Incident, isn't consistent with the system local settings. This issue might occur when you work with the views in unsealed Management Packs (MP).

**Workaround:**
To resolve this issue, follow the steps:

1.	Export the Service Manager Incident Management Configuration Library management pack.
2.	Modify the management pack. Locate the **LastModified** column and modify the binding as shown below:

**Before modification**

<mux:Column Name="lastModified" DisplayMemberBinding="{Binding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

**After modification**

<mux:Column Name="lastModified" DisplayMemberBinding="{datebinding:DateBinding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

1.	Repeat steps 1–2 for columns that're named **LastModified**.
2.	Reimport the modified management pack.
3.	Restart the console.
