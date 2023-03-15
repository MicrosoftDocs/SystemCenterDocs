---
description: This article describes the  pre and post backup scripts for Data Protection Manager.
manager: evansma
ms.topic: article
author: jyothisuri
ms.prod: system-center
keywords:
ms.date: 07/08/2021
title: Use Pre-backup and Post-backup scripts
ms.technology: data-protection-manager
ms.assetid: 4d64ee84-fc7d-45a8-b337-fbef001b75a3
ms.author: jsuri
ms.custom: UpdateFrequency2
---

# Pre-backup and Post-backup scripts for DPM

::: moniker range=">= sc-dpm-1801 <= sc-dpm-1807"

[!INCLUDE [eos-notes-data-protection-manager.md](../includes/eos-notes-data-protection-manager.md)]

::: moniker-end

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

```
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

1. On the protected computer, open the *ScriptingConfig.xml* file in an XML or text editor.

   > [!NOTE]
   > The *DataSourceName* attribute must be provided as **Drive:** (for example, **D:** if the data source is on the D drive).

2. For each data source, complete the *DatasourceScriptConfig* element as follows:
   -  For the *DataSourceName* attribute, enter the data source volume (for file data sources) or name (for all other data sources). The data source name for application data should be in the form of _Instance\Database_ for SQL, _Storage group name_ for Exchange, _Logical Path\Component Name_ for Virtual Server, and _SharePoint Farm\SQL Server Name\SQL Instance Name\SharePoint Config DB_ for Windows SharePoint Services.

   - In the **PreBackupScript** tag, enter the path and script name.
   - In the **PreBackupCommandLine** tag, enter command-line parameters to be passed to the scripts, separated by spaces.
   - In the **PostBackupScript** tag, enter the path and script name.
   - In the **PostBackupCommandLine** tag, enter command-line parameters to be passed to the scripts, separated by spaces.
   - In the **TimeOut** tag, enter the time in minutes that DPM should wait after invoking a script before timing out and marking the script as failed.

3. Save the *ScriptingConfig.xml* file.


> [!NOTE]
> DPM will suffix an additional Boolean (true/false) parameter to the post-backup script command, indicating the status of the DPM backup job.
