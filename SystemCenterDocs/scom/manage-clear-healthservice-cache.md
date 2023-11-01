---
title: How and When to Clear the Cache
description: This article provides guidance on how to manage the cache for the HealthService on management servers and agents in System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 01/04/2018
ms.custom: UpdateFrequency3
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid: bea86d42-4838-46b0-96ac-75a0e8988e3c
---

# How and When to Clear the Cache

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

In System Center Operations Manager, when troubleshooting an issue with the Operations console or with an agent, you may see recommendations to "clear the cache." For more information on troubleshooting an issue with an agent, see [Not monitored and gray agents](manage-agents-not-healthy.md).  

## To clear the cache

The following explains how and when to clear the console, server, or agent cache.  

### Operations Console

You may need to clear the Operations Console cache if you experience errors trying to retrieve data in views, such as ObjectNotFoundExceptions, or when the cache file grows too large, and you want to reduce its size on disk.

> [!IMPORTANT] 
> Before proceeding close any open consoles.

Clearing the cache using a command:

#### [Command Prompt](#tab/command-prompt)
This may need to be executed from an Administrator Command Prompt, depending on organization policy.
```cmd
"%ProgramFiles%\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" /clearcache
```

#### [PowerShell](#tab/powershell)
This may need to be executed from an Administrator PowerShell console, depending on organization policy.
```powershell
# This will read the console install directory from registry and then execute. Useful if installed in a non-default directory
Start-Process ((Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\System Center Operations Manager\12\Setup\Console").InstallDirectory + "Microsoft.EnterpriseManagement.Monitoring.Console.exe") -ArgumentList "/clearCache"

# This will start the process in the default ProgramFiles directory
Start-Process "$Env:ProgramFiles\Microsoft System Center\Operations Manager\Console\Microsoft.EnterpriseManagement.Monitoring.Console.exe" -ArgumentList "/clearCache"
```

Or to clear it manually:
1. Close any open consoles
2. Delete this file: `%LocalAppData%\Microsoft\Microsoft.EnterpriseManagement.Monitoring.Console\momcache.mdb`
3. Reopen the Operations Manager console.

---


### Management Servers

#### [From the console](#tab/from-the-console)
1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

> [!NOTE] 
> Know that this task works differently than that of an agent as all the workflows that are running under the HealthService on the management server needs to be stopped, and this can take time, to the point where the task may time out or throw an error. If this occurs, you may want to consider performing the cache clear manually.

#### [On the server directly](#tab/on-the-server-directly)
1. Navigate to the server.
2. Stop the Microsoft Monitoring Agent (HealthService) service.
3. Delete this folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\Health Service State`.
4. Restart the Microsoft Monitoring Agent (HealthService) service.

---

### Gateway Servers

#### [From the console](#tab/from-the-console)
1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Management Server**.
2. Select **Management Server State**.
3. In the **Gateway Management Server State** column, select one or several servers.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

#### [On the server directly](#tab/on-the-gateway-directly)
1. Navigate to the server.
2. Stop the Microsoft Monitoring Agent (HealthService) service.
3. Delete this folder: `%ProgramFiles%\Microsoft System Center\Operations Manager\Gateway\Health Service State`.
4. Restart the Microsoft Monitoring Agent (HealthService) service.

---

### Client Servers
If the agent on a client server is having issues with running workflows, old workflows, or is not communicating with the management group, you can try clearing the cache and restarting the agent. This should be one of the final steps in troubleshooting, however it can be very effective in solving some issues.

#### [From the console](#tab/from-the-console)
1. In the **Monitoring** workspace, expand **Operations Manager**, and then expand **Agent Details**.
2. Select **Agent Health State**.
3. In the **Agent State** column, select one or several agents.
4. In the **Tasks** pane, select **Flush Health Service State and Cache**.
5. In the prompt window, enter the credentials used for this task, or use default and hit **Run**

> [!NOTE] 
> Because this action deletes the cached data in the health service store files, including the record of this task itself, no task status is reported in the console upon completion of the task, it will always "Succeed" if we sent the command.

#### [On the client directly](#tab/on-the-client-directly)
1. Navigate to the client machine.
2. Stop the Microsoft Monitoring Agent (HealthService) service.
3. Delete this folder: `%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State`.
4. Restart the Microsoft Monitoring Agent (HealthService) service.

---

## Next steps

- To understand how it can help you review alerts that have been generated by rules and monitors that are still active, review [Viewing Active Alerts and Details](manage-alert-view-alerts-details.md).

- To understand how Operations Manager monitors the communication channel between an agent and its primary management server to ensure it's responsive and available, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).


