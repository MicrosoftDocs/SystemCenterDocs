---
title: How and When to Clear the Cache
description: This article provides guidance on how to manage the cache for the HealthService on management servers and agents in System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.date: 02/04/2026
ms.update-cycle: 180-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: bea86d42-4838-46b0-96ac-75a0e8988e3c
---

# How and when to clear the cache

In System Center Operations Manager, when you troubleshoot an issue with the Operations console or with an agent, you might see recommendations to **clear the cache**. For more information on troubleshooting an issue with an agent, see [Not monitored and gray agents](manage-agents-not-healthy.md).    

## Operations Console

You might need to clear the Operations Console cache to fix errors that occur when you access data in views, such as `ObjectNotFoundExceptions`. You might also need to clear the cache to free up disk space when the cache file becomes too large.

> [!IMPORTANT]
> Before you proceed, close any open consoles.

#### [PowerShell](#tab/powershell)

Depending on your organization policy, you might need to run this command from an Administrator PowerShell console.

```powershell
# Option 1: This will read the console install directory from registry and then execute. Useful if installed in a non-default directory
Start-Process ((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Console").InstallDirectory + "Microsoft.EnterpriseManagement.Monitoring.Console.exe") -ArgumentList "/clearCache"

# Option 2: This will start the process in the default ProgramFiles directory
Start-Process "$Env:ProgramFiles\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" -ArgumentList "/clearCache"
```

#### [Command Prompt](#tab/command-prompt)

Depending on your organization policy, you might need to run this command from an Administrator Command Prompt.

```cmd
"%ProgramFiles%\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" /clearcache
```

#### [Manual Clear](#tab/manual-clear)

1. Close any open Operations Manager consoles.
2. Delete the console cache file: `%LocalAppData%\Microsoft\Microsoft.EnterpriseManagement.Monitoring.Console\momcache.mdb`
3. Reopen the Operations Manager console.

---

### Management servers

One of the last steps in troubleshooting is to clear the cache. This step removes any unsaved data along with the current configuration and management packs. After clearing the cache, you receive a new configuration from the database, which includes updated management packs, and the server reconnects with clients. This step can help if a management server has faulty or missing management packs that cause workflow errors or if the server is delayed in sending data to the database.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials for this task, or use default credentials and select **Run**.

> [!NOTE]
> This task works differently than that of an agent. It stops all the workflows that run under the HealthService on the management server (which could be in the tens of thousands). This process can take time, and the task might time out or throw an error. If this problem occurs, consider manually clearing the cache.

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

Depending on your organization policy, you might need to execute this step from an Administrator console.

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

1. Go to the server.
2. Stop the Microsoft Monitoring Agent (HealthService) service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\Health Service State`.
4. Restart the Microsoft Monitoring Agent (HealthService) service.

---

### Gateway servers

One of the last steps in troubleshooting is clearing the cache. Sometimes, the gateway doesn't communicate with the management server and appears greyed out in the System Center Operations Manager console. In such cases, clear the cache for gateways. Also clear the cache when the gateway has outdated or unusable management packs or data that can't be inserted into the database.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Gateway Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials for this task, or use default credentials and select **Run**.

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

Depending on your organization policy, you might need to execute this step from an Administrator console.

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

1. Go to the server.
2. Stop the **Microsoft Monitoring Agent (HealthService)** service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Gateway\Health Service State`.
4. Restart the **Microsoft Monitoring Agent (HealthService)** service.

---

### Client servers

You can fix problems with workflows or communication between the agent on a client server and the management group by clearing the cache and restarting the agent. Use this troubleshooting step as a last resort, but it can resolve some problems effectively.

#### [From the Operations Console](#tab/from-the-operations-console)

1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Agent Details**.
2. Select **Agent Health State**.
3. In the **Agent State** column, select one or several agents.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials for this task, or use default credentials and select **Run**.

> [!NOTE]
> This action deletes the cached data in the health service store files, including the record of this task itself. Because of this deletion, the console doesn't report any true task status when the task finishes. The task always shows as "Succeed" as long as the command is sent.

#### [Using a Command Line Interface](#tab/using-a-command-line-interface)

Depending on your organization policy, you might need to execute this step from an Administrator console.

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

1. Go to the client machine.
2. Stop the **Microsoft Monitoring Agent (HealthService)** service.
3. Delete the cache folder: `%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State`.
4. Restart the **Microsoft Monitoring Agent (HealthService)** service.

---

## Next steps

- To learn how to review alerts that the system generates by using active rules and monitors, see [Viewing Active Alerts and Details](manage-alert-view-alerts-details.md).

- To understand how Operations Manager monitors the communication channel between an agent and its primary management server to ensure it's responsive and available, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).
