---
title: Optimize performance of .NET activities in System Center - Orchestrator
description: Describes how to configure runbook servers in System Center - Orchestrator, to optimize performance of .NET activities.
ms.date: 01/17/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.custom: UpdateFrequency3
---

# Optimize performance of .NET activities

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

## Improve assembly load time

When a runbook containing an activity that references the .NET assemblies executes, the job process has to load the referenced assembly when such an activity is executed. Any subsequent execution of the same activity or other activities from the assembly will reuse the loaded assembly.

Loading an assembly may cause a delay of up to 30 seconds. This delay can also occur when a runbook is started on a computer without Internet access, because Windows can't verify the Microsoft Authenticode signature for the .NET assemblies.

To remove the delay you can either deactivate `generatePublisherEvidence` in `PolicyModule.exe`, or you can create a profile for the service account.

### Deactivate `generatePublisherEvidence` in `policymodule.exe.config`

::: moniker range="<=sc-orch-2019"
1. Locate the file `C:\Program Files (x86)\Microsoft System Center\Orchestrator\Runbook Server\policymodule.exe.config` on the runbook server that executes runbooks containing an activity referencing a .NET assembly. 
::: moniker-end

::: moniker range="sc-orch-2022"
1.  Locate the file `C:\Program Files\Microsoft System Center\Orchestrator\Runbook Server\policymodule.exe.config` on the runbook server that executes runbooks containing an activity referencing a .NET assembly.
::: moniker-end

2.  Add the following code to `policymodule.exe.config`:

    ```xml
    <runtime>
      <generatePublisherEvidence enabled="false"/>
    </runtime>
    ```

### Create a profile for the service account

1. On the runbook server where runbooks run that contain an activity referencing the .NET assemblies, sign in to the computer using the service account credentials. A profile is created on first sign-in.

## Next steps
Learn more about [creating runbooks](design-and-build-runbooks.md).  
