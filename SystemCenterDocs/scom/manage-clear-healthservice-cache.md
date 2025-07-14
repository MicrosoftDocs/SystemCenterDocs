---
title: How and When to Clear the Cache
description: This article provides guidance on how to manage the cache for the HealthService on management servers and agents in System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: bea86d42-4838-46b0-96ac-75a0e8988e3c
---

# How and When to Clear the Cache



In System Center Operations Manager, when troubleshooting an issue with the Operations console or with an agent, you may see recommendations to "clear the cache." For more information on troubleshooting an issue with an agent, see [Not monitored and gray agents](manage-agents-not-healthy.md).  

## Operations Console

A possible reason to clear the Operations Console cache is to fix errors that occur when you access data in views, such as ObjectNotFoundExceptions. Another reason is to free up disk space when the cache file becomes too large.

> [!IMPORTANT]
> Before proceeding close any open consoles.

#### [PowerShell](#tab/powershell)

This may need to be executed from an Administrator PowerShell console, depending on organization policy.

```powershell
# Option 1: This will read the console install directory from registry and then execute. Useful if installed in a non-default directory
Start-Process ((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Console").InstallDirectory + "Microsoft.EnterpriseManagement.Monitoring.Console.exe") -ArgumentList "/clearCache"

# Option 2: This will start the process in the default ProgramFiles directory
Start-Process "$Env:ProgramFiles\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" -ArgumentList "/clearCache"
```

#### [Command Prompt](#tab/command-prompt)

This may need to be executed from an Administrator Command Prompt, depending on organization policy.

```cmd
"%ProgramFiles%\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" /clearcache
```

#### [Manual Clear](#tab/manual-clear)

1. Close any open Operations Manager consoles.
2. Delete the console cache file: `%LocalAppData%\Microsoft\Microsoft.EnterpriseManagement.Monitoring.Console\momcache.mdb`
3. Reopen the Operations Manager console.

---

### Management servers

One of the last steps in troubleshooting is to clear the cache. This will remove any unsaved data along with the current configuration and management packs. After clearing the cache, we will receive a new configuration from the database, which includes updated management packs, and reconnect with clients. This can help if a management server has faulty or missing management packs that cause workflow errors or is delayed in sending data to the database.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

> [!NOTE]
> Know that this task works differently than that of an agent as all the workflows that are running under the HealthService on the management server (which could be in the tens of thousands) needs to be stopped, and this can take time, to the point where the task may time out or throw an error. If this occurs, you may want to consider performing the cache clear manually.

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

This may need to be executed from an Administrator console depending on organization policy.

PowerShell:

```powershell
# This will read the install directory from registry and perform the same steps outlined
Stop-Service HealthService -Force -Verbose;
Remove-Item -Path "$((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Server").InstallDirectory + 'Health Service State')" -Recurse -Force;
Start-Service HealthService -Verbose
```

Command Prompt (as a batch file):

```cmd
:: Clear Health Service State (Cache)
ECHO OFF
net stop HealthService
FOR /F "usebackq tokens=2,* skip=2" %%L IN (`reg query "HKLM\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup" /v InstallDirectory`) DO SET installpath=%%M
echo %installpath%
@RMDIR "%installpath%Health Service State" /S /Q
net start HealthService
```

#### [Perform steps manually](#tab/perform-steps-manually)

1. Navigate to the server.
2. Stop the Microsoft Monitoring Agent (HealthService) service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\Health Service State`.
4. Restart the Microsoft Monitoring Agent (HealthService) service.

---

### Gateway servers

One of the last steps in troubleshooting is clearing the cache. Sometimes, the gateway may not communicate with the management server and appear greyed out in the System Center Operations Manager console. In such cases, we need to clear the cache for gateways. We also need to do this when the gateway has outdated or unusable management packs or data that cannot be inserted into the database.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Gateway Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

This may need to be executed from an Administrator console depending on organization policy.

PowerShell:

```powershell
# This will read the install directory from registry and perform the same steps outlined
Stop-Service HealthService -Force -Verbose;
Remove-Item -Path "$((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Gateway").InstallDirectory + 'Health Service State')" -Recurse -Force;
Start-Service HealthService -Verbose
```

Command Prompt (as a batch file):

```cmd
:: Clear Health Service State (Cache)
ECHO OFF
net stop HealthService
FOR /F "usebackq tokens=2,* skip=2" %%L IN (`reg query "HKLM\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup" /v InstallDirectory`) DO SET installpath=%%M
echo %installpath%
@RMDIR "%installpath%Health Service State" /S /Q
net start HealthService
```

#### [Perform steps manually](#tab/perform-steps-manually)

1. Navigate to the server.
2. Stop the **Microsoft Monitoring Agent (HealthService)** service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Gateway\Health Service State`.
4. Restart the **Microsoft Monitoring Agent (HealthService)** service.

---

### Client servers

A possible way to fix problems with workflows or communication between the agent on a client server and the management group is to clear the cache and restart the agent. This is a last resort for troubleshooting, but it can resolve some issues effectively.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Agent Details**.
2. Select **Agent Health State**.
3. In the **Agent State** column, select one or several agents.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

> [!NOTE]
> Because this action deletes the cached data in the health service store files, including the record of this task itself, no true task status is reported in the console upon completion of the task, it will always "Succeed" so long as the command was sent.

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

This may need to be executed from an Administrator console depending on organization policy.

PowerShell:
```powershell
# This will read the install directory from registry and perform the same steps outlined
Stop-Service HealthService -Force -Verbose;
Remove-Item -Path "$((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Agent").InstallDirectory + 'Health Service State')" -Recurse -Force;
Start-Service HealthService -Verbose
```

Command Prompt (as a batch file):
```cmd
:: Clear Health Service State (Cache)
ECHO OFF
net stop HealthService
FOR /F "usebackq tokens=2,* skip=2" %%L IN (`reg query "HKLM\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup" /v InstallDirectory`) DO SET installpath=%%M
echo %installpath%
@RMDIR "%installpath%Health Service State" /S /Q
net start HealthService
```

#### [Perform steps manually](#tab/perform-steps-manually)

1. Navigate to the client machine.
2. Stop the **Microsoft Monitoring Agent (HealthService)** service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State`.
4. Restart the **Microsoft Monitoring Agent (HealthService)** service.

---

## Next steps

- To understand how it can help you review alerts that have been generated by rules and monitors that are still active, review [Viewing Active Alerts and Details](manage-alert-view-alerts-details.md).

- To understand how Operations Manager monitors the communication channel between an agent and its primary management server to ensure it's responsive and available, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).
