---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-07-28
title:  What s new in Service Management Automation 2016
ms.technology:  service-management-automation
ms.assetid:  204ba9e4-a03e-4598-9489-15a0f1a2394c
---

# What&#39;s new in Service Management Automation 2016
The following new features are available in Service Management Automation (SMA) 2016.  

**Support for PowerShell script**
SMA 2016 now supports PowerShell Script in addition to PowerShell Workflow which was the only runbook format supported in previous versions.  

**PowerShell ISE add-on**
The Service Management Automation (SMA) PowerShell ISE add-on makes it easier to author and test your runbooks in your local PowerShell ISE environment.

**Specify a runbook worker**
By default, SMA randomly picks a Runbook worker to service a job when a Runbook is invoked.     SMA 2016 adds a property to a runbook that specifies a particular runbook worker it should run on.

**Support for PowerShell 5.0**
Service Management Automation 2016 now supports Windows Management Framework 5.0.

## What&#39;s new since Technical Preview 5
### PowerShell ISE Add-on v1.1
- You can now designate runbook worker for runbooks from ISE
- New columns added for designated runbook and runbook type<br>

The following bugs have been fixed since Technical Preview 5
- Error messages thrown by Start/Stop buttons in Test Job window are inappropriate
-	The past draft job shown in Test Job window is not the latest job
- Unicode characters in a runbook get replaced on downloading the runbook
