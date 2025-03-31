---
description: This article describes the  pre and post backup scripts for Data Protection Manager.
ms.topic: article
ms.service: system-center
keywords:
ms.date: 03/31/2025
title: Use Pre-backup and Post-backup scripts
ms.subservice: data-protection-manager
ms.assetid: 4d64ee84-fc7d-45a8-b337-fbef001b75a3
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.custom: UpdateFrequency2, engagement-fy24
---

# Pre-backup and Post-backup scripts for DPM

This article details the pre- and post-backup scripts that you can use for DPM and how to use them.

A *pre-backup script* is a script that resides on a protected computer. It's executed before each DPM backup job and prepares the protected data source for backup.

A *post-backup script* is a script that runs after a DPM backup job to do any post-backup processing, such as bringing a virtual machine back online.

When you install a protection agent on a computer, a *ScriptingConfig.xml* file is added to the install path *\Microsoft Data Protection Manager\DPM\Scripting* folder on the protected computer. For each protected data source on the computer, you can specify a pre-backup script and a post-backup script in ScriptingConfig.xml.

> [!NOTE]
> The pre-backup and post-backup scripts can't be VBScripts. Instead, you must use a wrapper command around your script containing **cscript myscript.vbs**.

When DPM runs a protection job, *ScriptingConfig.xml* on the protected computer is checked. If a pre-backup script is specified, DPM runs the script and then completes the job. If a post-backup script is specified, DPM completes the job and then runs the script.

> [!NOTE]
> Protection jobs include replica creation, express full backup, synchronization, and consistency check.

DPM runs the pre-backup and post-backup scripts by using the local system account. As a best practice, ensure that the scripts have Read and Execute permissions for the administrator and local system accounts only. This level of permissions prevents unauthorized users from modifying the scripts.

**ScriptingConfig.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScriptConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns="http://schemas.microsoft.com/2003/dls/ScriptingConfig.xsd">
   <DatasourceScriptConfig DataSourceName="Data source">
     <PreBackupScript>"Path\Script Parameters" </PreBackupScript>
     <PostBackupScript>"Path\Script Parameters" </PostBackupScript>
     <TimeOut>30</TimeOut>
   </DatasourceScriptConfig>
</ScriptConfiguration>
```

## Specify pre-backup and post-backup scripts

To specify pre-backup and post-backup scripts, follow these steps:

1. On the protected computer, open the *ScriptingConfig.xml* file in an XML or text editor.

   > [!NOTE]
   > The *DataSourceName* attribute must be provided as **Drive:** (for example, **D:** if the data source is on the D drive).

2. For each data source, complete the *DatasourceScriptConfig* element:

    For the *DataSourceName* attribute, use one of the following:

    | DataSourceName | Attribute |
    |---|---|
    |Volume or file share data sources|DataSourceName = “volume_letter” <br>Example:  \<DatasourceScriptConfig DataSourceName="C:"\>   - Don't use backslash `\` after drive letter.|
    |Volume Mountpoints|DataSourceName=” Volume\mountpoint_name” <br>Example: \<DatasourceScriptConfig DataSourceName="C:\mountpoint"\>|
    |Microsoft SQL Server|DataSourcename= "Instance\Database" <br>Example:  \<DatasourceScriptConfig DataSourceName="MySQLInstance\MySQLDB"\>|
    |Microsoft Exchange|DataSourceName="Storage group name" <br>Example: \<DatasourceScriptConfig DataSourceName="First Storage Group"\>|
    |Windows SharePoint Services|DatasourceName=“SharePoint Farm\SQL Server Name\SQL Instance Name\SharePoint_Config”   <br>Example: \<DatasourceScriptConfig DataSourceName="SharePoint Farm\MY-SQL\MYINSTANCE\SharePoint_Config"\>|
    |Client Protection|DataSourceName= "DisconnectedClient" <br>Example: \<DatasourceScriptConfig DataSourceName="DisconnectedClient"\>|
    |SystemState or BMR|DataSourceName="System Protection " <br>Example: \<DatasourceScriptConfig DataSourceName="System Protection "\> |
    |Hyper-V Server|DataSourceName = “ComponentID” <br>Example: \<DatasourceScriptConfig DataSourceName="44b31766-c87d-416e-b2c0-08fd297a0c8b"\>|

    >[!NOTE]
    >To get the VM ComponentID, run the PowerShell command Get-VM on the Hyper-V Server to list VM names and ID.
    > ```powershell
    > PS C:\> Get-VM  | select-object Name,ID
    > ```
    >| Name | Id |
    >| --- | --- |
    >| Windows2022 | 44b31766-c87d-416e-b2c0-08fd297a0c8b |
    >| Windows10-2 | 01d9ed67-5c79-4bbf-8f42-0f509b07aeda |

3. Save the *ScriptingConfig.xml* file.

    > [!NOTE]
    > DPM will suffix an additional Boolean (true/false) parameter to the post-backup script command, indicating the status of the DPM backup job.

## Next steps

- [Back up Hyper-V virtual machines](back-up-hyper-v-virtual-machines.md).