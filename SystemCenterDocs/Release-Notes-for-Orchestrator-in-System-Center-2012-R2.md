---
title: Release Notes for Orchestrator in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5c79366-fa0f-4f93-aa63-b605a589206d
---
# Release Notes for Orchestrator in System Center 2012 R2
Before you install and use [!INCLUDE[orchshort](../Token/orchshort_md.md)] in [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], read these release notes.

## Known Issues

### Signature block must be removed for SMA sample runbooks to run as child runbooks
**Description:** Signature block comments are present in SMA sample runbooks, which will cause the runbooks to fail to run if called by another runbook.

**Workaround:** Remove the signature block at the end of the sample runbook. To remove the signature block, edit the runbook and remove the whole signature block, which has a beginning line of `# SIG # Begin signature block` and an ending line of `# SIG # End signature block`.  After removal, save the runbook and then publish it.

### SMA can only be installed on domain\-joined computers
**Description:** If the computer you are installing the Service Management Automation \(SMA\) feature on is not part of a domain, the SMA Web service and the SMA Runbook Worker installation will fail.

**Workaround:** Ensure the computer has been joined to a domain beforehand.

### Setup fails when deploying IPs or executing runbooks on Windows Server 2012 and Windows Server 2012 R2 without .NET 3.5
**Description:** When trying to deploy an IP or execute a runbook on a computer running Windows Server 2012 or Windows Server 2012 R2 on which .NET Framework 3.5 is not enabled, the execution will fail.

**Workaround:** Enable .NET Framework 3.5 manually on the computer running Windows Server 2012 or Windows Server 2012 R2 and try again.

### Custom Enum values must be unique
**Description:** If you create a custom Enum value that duplicates the name of an existing Enum value, the activity will fail.

**Workaround:** All customized Enum values must have names that are different from all other Enum values.

### Orchestrator server restarts after deploying the Service Manager IP
**Description:** After deploying the IP for Service Manager in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] to the runbook server, the [!INCLUDE[orchshort](../Token/orchshort_md.md)] server is automatically restarted without any further notice.

**Workaround:** None. The computer must be restarted so that the Service Manager IP can update some of the binary files that have been used.

### Run Program activity doesn't work in Interactive mode on Windows Server 2012
**Description:** For example, on a runbook server that is running Windows Server 2012, start a runbook containing a Run Program activity that has been configured to run notepad.exe in Interactive mode. Notepad.exe is started as a background process instead of as a foreground process.

**Workaround:** In the registry key HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Windows, the value for the NoInteractiveServices subkey defaults to 1, which means that no service is allowed to run interactively, regardless of whether it has SERVICE\_INTERACTIVE\_PROCESS. When NoInteractiveServices is set to a 0, services with SERVICE\_INTERACTIVE\_PROCESS are allowed to run interactively. Change the value of the NoInteractiveServices subkey to 0, and then restart the computer.

## See Also
[Release Notes for System Center 2012 - Orchestrator_1](../Topic/Release-Notes-for-System-Center-2012---Orchestrator_1.md)

