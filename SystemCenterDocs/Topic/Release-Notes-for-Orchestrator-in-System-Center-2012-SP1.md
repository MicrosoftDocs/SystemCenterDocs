---
title: Release Notes for Orchestrator in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab9f444a-ed81-4398-accb-4880b4dc60cf
---
# Release Notes for Orchestrator in System Center 2012 SP1
These release notes contain information that is required to successfully install [!INCLUDE[orchshort](../Token/orchshort_md.md)] in [!INCLUDE[sc2012sp1_long](../Token/sc2012sp1_long_md.md)]. They contain information that is not available in the product documentation.

Before you install and use [!INCLUDE[orchshort](../Token/orchshort_md.md)], read these release notes. These release notes apply to [!INCLUDE[orchshort](../Token/orchshort_md.md)] in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)].

If you are looking for the Release Notes for the original release of [!INCLUDE[orchlong](../Token/orchlong_md.md)], see [Release Notes for System Center 2012 - Orchestrator](../Topic/Release-Notes-for-System-Center-2012---Orchestrator.md).

## Known Issues

### Setup program will fail when deploying IPs or executing runbooks on a computer running Windows Server 2012 without .NET 3.5 enabled.
**Description:** When trying to deploy an IP or execute a runbook on a computer running Windows Server 2012 on which .NET 3.5 is not enabled, the execution will fail.

**Workaround:** Enable .NET 3.5 manually on the computer running Windows Server 2012 and try again.

### System Center 2012 \- Service Manager IP: Custom Enum value that duplicates an existing Enum value causes activity to fail.
**Description:** If you create a custom Enum value that duplicates the name of an existing Enum value, the activity will fail.

**Workaround:** All customized Enum values must have names that are different from all other Enum values.

### System Center 2012 \- Service Manager IP: the [!INCLUDE[orchshort](../Token/orchshort_md.md)] server restarts after deploying the IP
**Description:** After Deploying the IP for Service Manager in [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] to the runbook server, the [!INCLUDE[orchshort](../Token/orchshort_md.md)] server is automatically restarted \(without any further notice\).

**Workaround:** None. The computer must be restarted so that the Service Manager IP can update some of the binary files that have been used.

### When running [!INCLUDE[orchshort](../Token/orchshort_md.md)] on Windows Server 2012, the Run Program activity doesn't work in Interactive mode
**Description:** For example, on a runbook server that is running Windows Server 2012, start a runbook containing a Run Program activity that has been configured to run notepad.exe in Interactive mode. Notepad.exe is started as a background process instead of as a foreground process.

**Workaround:** In the registry key HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Windows, the value for the NoInteractiveServices subkey defaults to 1, which means that no service is allowed to run interactively, regardless of whether it has SERVICE\_INTERACTIVE\_PROCESS. When NoInteractiveServices is set to a 0, services with SERVICE\_INTERACTIVE\_PROCESS are allowed to run interactively. Change the value of the NoInteractiveServices subkey to 0, and then restart the computer.

### Send SNMP Trap activity always send Generic identifier as coldStart\(0\) when the value is picked up from the GUI
**Description:** Selecting the property value from the popup selection control doesn't work.  No matter what is selected, the value always reverts to coldStart\(0\).

**Workaround:** Type the integer value directly into the edit box, and that works correctly.

## See Also
[Orchestrator_1](../Topic/Orchestrator_1.md)

