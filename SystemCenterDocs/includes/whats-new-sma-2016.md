---
description: include file to describe what's new in Service Management Automation (SMA) 2016
manager:  carmonm
ms.topic: include
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 01/22/2018
title:  include file 
ms.technology:  service-management-automation
---

# What's new in Service Management Automation 2016

System Center 2016 - Service Management Automation (SMA) added the features described in this article.

## Support for PowerShell script

SMA 2016 supports PowerShell Script in addition to PowerShell Workflow, which was the only runbook format supported in previous versions. [Learn more](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/powershell-script-runbook-support-in-system-center-service-management-automation-2016-sma-part-1/).

## PowerShell ISE add-on

The SMA PowerShell ISE add-on makes it easier to author and test your runbooks in your local PowerShell ISE environment. [Learn more](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/introducing-service-management-automation-ise-add-on/).

## Specify a runbook worker

By default, SMA randomly picks a Runbook worker to service a job when a Runbook is invoked. SMA 2016 adds a property to a runbook that specifies a particular runbook worker on which it should run. [Learn more](https://blogs.technet.microsoft.com/orchestrator/2016/04/28/designating-a-runbook-to-a-runbook-worker-in-system-center-service-management-automation-2016-technical-preview-5/).

## Support for PowerShell 5.0

SMA 2016 supports Windows Management Framework 5.0.

### PowerShell ISE add-on v1.1

- You can now designate runbook worker for runbooks from ISE.
- New columns added for designated runbook and runbook type.
