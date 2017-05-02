---
description: Features what is new and available in Service Management Automation (SMA) 2016
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  What s new in Service Management Automation 2016
ms.technology:  service-management-automation
ms.assetid:  204ba9e4-a03e-4598-9489-15a0f1a2394c
---

# What's new in Service Management Automation 2016

The following new features are available in Service Management Automation (SMA) 2016.  

## Support for PowerShell script

SMA 2016 now supports PowerShell Script in addition to PowerShell Workflow which was the only runbook format supported in previous versions. You can read more about this on the [team](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/powershell-script-runbook-support-in-system-center-service-management-automation-2016-sma-part-1/) [blog](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/powershell-script-runbook-support-in-system-center-service-management-automation-2016-sma-part-2/).

## PowerShell ISE add-on

The Service Management Automation (SMA) PowerShell ISE add-on makes it easier to author and test your runbooks in your local PowerShell ISE environment. You can read more about this on the [team blog](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/introducing-service-management-automation-ise-add-on/).

## Specify a runbook worker

By default, SMA randomly picks a Runbook worker to service a job when a Runbook is invoked.     SMA 2016 adds a property to a runbook that specifies a particular runbook worker it should run on. You can read more about this on the [team blog](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/designating-a-runbook-to-a-runbook-worker-in-system-center-service-management-automation-2016-technical-preview-5/).

## Support for PowerShell 5.0

Service Management Automation 2016 now supports Windows Management Framework 5.0.

## What's new since Technical Preview 5

### PowerShell ISE Add-on v1.1

- You can now designate runbook worker for runbooks from ISE
- New columns added for designated runbook and runbook type

### The following bugs have been fixed since Technical Preview 5

- Error messages thrown by Start/Stop buttons in Test Job window are inappropriate
- The past draft job shown in Test Job window is not the latest job
- Unicode characters in a runbook get replaced on downloading the runbook
