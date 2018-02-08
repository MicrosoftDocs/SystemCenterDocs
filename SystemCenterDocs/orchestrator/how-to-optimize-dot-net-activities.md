---
title: Optimize performance of  .NET activities in System Center - Orchestra
description: Describes how to configure runbook servers in System Center - Orchestrator, to optimize performance of .NET activities.
ms.date: 01/17/2018
ms.prod: system-center-threshold
ms.technology: orchestrator
ms.topic: article
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Optimize performance of .NET activities



If a runbook contains an activity that references the .NET libraries, the first reference to the .NET libraries takes additional time to initialize. This delay can be as much as 30 seconds. All remaining activities that reference the .NET libraries run immediately. This delay can also occur when a runbook is started on a computer without Internet access, because Windows cannot verify the Microsoft Authenticode signature for the .NET libraries, and this causes a delay during the initialization of the activity.

In order to remove the delay you can either deactivate **generatePublisherEvidence** in **PolicyModule.exe** or you can create a profile for the service account.

## To deactivate generatePublisherEvidence in policymodule.exe.config

1.  On the runbook server where runbooks that contain an activity referencing the .NET libraries run, locate the file **C:\\Program Files \(x86\)\\Microsoft System Center <version>\\Orchestrator\\Runbook Server\\policymodule.exe.config**.

2.  Add the following code to policymodule.exe.config:

    ```
    <runtime>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<generatePublisherEvidence enabled="false"/>
    </runtime>
    ```

## To create a profile for the service account

1. On the runbook server where runbooks run that contain an activity referencing the .NET libraries, log on to the computer using the service account credentials. A profile is created on first logon.

## Next steps
Learn more about [creating runbooks](design-and-build-runbooks.md).  
