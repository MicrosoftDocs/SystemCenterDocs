---
description: This article describes logging in DPM.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Set up DPM logging
ms.subservice: data-protection-manager
ms.assetid: 710459cd-75ec-4052-9199-c45828cbc19b
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency2, engagement-fy24
---

# Set up DPM logging

System Center Data Protection Manager (DPM) logs activity in log files (\*.errlog). Log files are tab delimited and can be opened in Excel for easy viewing. You can filter with specific levels and task IDs in order to find events that interest you. Every log entry has a log task ID generated by DPM as a unique GUID for every DPM task. This helps you to track down log entries for specific jobs. Log files are located as follows:

- Log files are located under the DPM Installation folder and can be varied or changed during setup. To locate the install path, run the following from administrative command prompt:

     `Reg query "HKLM\Software\Microsoft\Microsoft Data Protection Manager\Setup" /v Installpath`

     :::image type="content" source="media/set-up-dpm-logging/cmd.png" alt-text="Screenshot of command prompt.":::

::: moniker range="<=sc-dpm-2022"

Based on the above output, the logs will be in the following locations:
         
   - DPM installation information: Logged on the DPM server at *%ProgramFiles%\Microsoft System Center 2022\DPM\DPMLogs*.
   - DPM activity information: Logged on the DPM server at *%ProgramFiles%\Microsoft System Center 2022\DPM\DPM\Temp*.

::: moniker-end

::: moniker range="sc-dpm-2025"
Based on the above output, the logs will be in the following locations:
         
   - DPM installation information: Logged on the DPM server at *%ProgramFiles%\Microsoft System Center 2025\DPM\DPMLogs*.
   - DPM activity information: Logged on the DPM server at *%ProgramFiles%\Microsoft System Center 2025\DPM\DPM\Temp*.

::: moniker-end

- **Protected client activity**: Logged on the client computer at %ProgramFiles%\Microsoft Data Protection Manager\DPM\Temp Logs. Client-initiated activities, such as self-service recovery, are logged on the client computer based on the user (%USERPROFILE%\AppData\Roaming\Microsoft\System Center Data Protection Manager\\).

You can tweak log file settings as follows:

|Value name|Value type/Allowed values|Details|
|--------------|------------------------------|-----------|
|TraceLogLevel|DWORD<br /><br />TRACE_ERROR - Logs all errors and failures - default setting<br /><br />TRACE_DBG_ACTIVITY - Logs all activities such as start, cancel, end<br /><br />TRACE_DBG_NORMAL - Logs activities considered important<br /><br />TRACE_DBG_CRITICAL - Logs critical errors only.<br /><br />TRACE_DBG_FATAL - Logs fatal errors such as task or job failures|Specifies the logging level.<br /><br />Can be overridden per binary. A valid bitmask of allowed values is:<br /><br />enum TRACE_FLAG{<br /><br />TRACE_ERROR = 0x2,<br /><br />TRACE_DBG_ACTIVITY = 0x4,<br /><br />TRACE_DBG_       = 0x8,<br /><br />TRACE_PERF = 0x20,<br /><br />TRACE_DBG_FATAL = 0x200,<br /><br />TRACE_DBG_CRITICAL = 0x400<br />};<br /><br />You can also enable full Verbose logging but remember that this affects performance. If you need this for a limited time, do the following:<br /><br />1.  In the registry, at HKLM\Software\Microsoft\Microsoft Data Protection Manager, add a DWORD value TraceLogLevel and set it to 0x43e.<br />2.  To apply immediately, stop the DPM services for which you want to enable verbose logging and delete the old logs.<br />3.  After you reproduce the issue and finish troubleshooting, delete the registry entry you created, and restart the stopped services so that non-verbose logging works again.|
|TraceLogPath|REG_SZ|Specifies the log location.<br /><br />Requires a valid NTFS volume path with 3 GB of compressed space on DPM server (no quotation marks required in the name for paths that contain spaces).<br /><br />Can be overridden per binary.|
|\<binary\> TraceLogMaxSize|DWORD|Specifies the size of the log file in Bytes<br /><br />15 MB by default<br /><br />A file size (total disk space consumed for this binary's log = size \* number of files to retain)<br /><br />The current size of log files is tracked in HKLM\Software\Microsoft\Microsoft Data Protection Manager: \<binary\>TraceLogMaxSize (DWORD). This is an internal registry key, and we recommend that you don't modify it.|
|\<binary\>TraceLogMaxNumber|DWORD|Maximum number of log files to retain<br /><br />30 by default<br /><br />The current number of log files is tracked in HKLM\Software\Microsoft\Microsoft Data Protection Manager: \<binary\>TraceLogNextNum (DWORD). This is an internal registry key, and we recommend that you don't modify it.|

## <a name="BKMK_Binary"></a>Binary and service mapping

Mappings between some of the log binary names and services are summarized in the following table.

|                    Service/Process                    |      Binary name       |                                                                                                                             Details                                                                                                                              |
|-------------------------------------------------------|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  DPM Engine (MSDPM)                   |         MSDPM          |                                                                               MSDPM engine logs contain info about engine API calls, jobs and task triggers, housekeeping jobs, and so on.                                                                                |
|             DPM Replication Agent (DPMRA)             |         DPMRA          |                                                                 Logs information about tape backups, disk replication, restore, secondary DPM replications. On DPM server and protected client.                                                                  |
|               DPM Library Agent (DPMLA)               |        LAAgent         |                                                                                            Logs library related activities. On DPM server and shared library server.                                                                                             |
|                        DPM UI                         |         DPMUI          |                                                                                                 Logs UI activity such as monitoring, protection, recovery, etc.                                                                                                  |
|                  DPM PowerShell CLI                   |         DPMCLI         |                                                                                                                     Logs all cmdlet actions                                                                                                                      |
|                  DPM Access Manager                   |         DPMMAC         |                                                                                    Logs automatic behavior such as grow, rerun jobs, and Access Control Manager information.                                                                                     |
| Exchange Cmdlet Wrapper<br /><br />E14 Cmdlet Wrapper | ExchangeCmdletsWrapper |                                                                                                   Logs for various cmdlets run by DPMRA on Exchange client side                                                                                                   |
|                   Agent Coordinator                   |   AgentBootStrapper    |                                                                                                            Logs during agent installation and upgrade                                                                                                            |
|                  DPM Client Service                   |  DPMClientProtection   |                                                                                                Logs by DPM client installed on laptops. Used on laptop-side only.                                                                                                |
|                    DPM Backup Tool                    |       DpmBackup        |                                                                                                                  Logs for tool doing DPM backup                                                                                                                  |
|             Install SQL Prep (Remote SQL)             | SQL Prep Bootstrapper  |                                                                                                   Logs during installation of remote SQL Server before Setup.                                                                                                    |
|                      DPM Backup                       |       DpmBackup        |                                                                                                                     Logs for DPM backup tool                                                                                                                     |
|                      DPM Writer                       |       DPMWriter        |                                                                                      Logs during third-party tape backups and secondary server backup. On DPM server only.                                                                                       |
|                  WSS Cmdlet wrapper                   |   WssCmdletsWrapper    |                                   Logs when running WSS cmdlets on SharePoint WFE. On protected client only.<br /><br />Logs at: %USERPROFILE%\AppData\Roaming\Microsoft\Microsoft System Center Data ProtectionManager 2012\                                    |
|                    SQL EUR Client                     |       EurClient        | Installed on machines where SQL EUR client is installed. Logs information about connecting to DPMserver, triggering, and canceling recovery, etc.<br /><br />Logs at: %USERPROFILE%\AppData\Roaming\Microsoft\Microsoft System Center Data ProtectionManager 2012\ |
|                   Laptop Client UI                    |      DPMClientUI       |                                      Logs about various actions triggered from DPM client UI and failures.<br /><br />Logs at: %USERPROFILE%\AppData\Roaming\Microsoft\Microsoft System Center Data ProtectionManager 2012\                                      |
