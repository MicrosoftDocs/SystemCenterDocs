---
title: How to Configure Runbook Servers to Optimize Performance of  .NET Activities
description: Describes how to configure runbook servers in System Center 2016 - Orchestrator to optimize performance of .NET activities.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13a804ec-3aea-479a-add1-5bd6cf73eba6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# How to configure Runbook Servers to optimize performance of .NET activities

> Apples To: System Center 2016 - Orchestrator

If a runbook contains an activity that references the .NET libraries, the first reference to the .NET libraries takes additional time to initialize. This delay can be as much as 30 seconds. All remaining activities that reference the .NET libraries run immediately. This delay can also occur when a runbook is started on a computer without Internet access, because Windows cannot verify the Microsoft Authenticode signature for the .NET libraries, and this causes a delay during the initialization of the activity.

In order to remove the delay you can either deactivate **generatePublisherEvidence** in **PolicyModule.exe** or you can create a profile for the service account.

## To deactivate generatePublisherEvidence in policymodule.exe.config

1.  On the runbook server where runbooks that contain an activity referencing the .NET libraries run, locate the file **C:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Runbook Server\\policymodule.exe.config**.

2.  Add the following code to policymodule.exe.config:

    ```
    <runtime>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<generatePublisherEvidence enabled="false"/>
    </runtime>
    ```

## To create a profile for the service account

1. On the runbook server where runbooks run that contain an activity referencing the .NET libraries, log on to the computer that is using the service account credentials. A profile is created on first logon.

## Next steps
Learn more about creating runbooks at [Build and test runbooks for System Center 2016 - Orchestrator](design-and-build-runbooks.md).  
