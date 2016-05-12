---
title: Upgrading System Center 2012 SP1 Orchestrator to System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9488d331-ab28-4a50-8f58-0d74dee95adc
---
# Upgrading System Center 2012 SP1 Orchestrator to System Center 2012 R2
This guide will show you how to upgrade from [!INCLUDE[sc2012sp1_long](Token/sc2012sp1_long_md.md)][!INCLUDE[orchblue_2](Token/orchblue_2_md.md)] to [!INCLUDE[orchblue_1](Token/orchblue_1_md.md)].

> [!WARNING]
> If you are planning to upgrade two or more System Center components, it is important to start by reading the [Upgrade Sequencing for System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=328675) topic.
> 
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:
> 
> 1.  [!INCLUDE[orchshort](Token/orchshort_md.md)]
> 2.  [!INCLUDE[smshort12](Token/smshort12_md.md)]
> 3.  [!INCLUDE[dpm2012sp1long](Token/dpm2012sp1long_md.md)]
> 4.  [!INCLUDE[om12short](Token/om12short_md.md)]
> 5.  [!INCLUDE[cmshort](Token/cmshort_md.md)]
> 6.  [!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]
> 7.  [!INCLUDE[conceroshort](Token/conceroshort_md.md)]

> [!TIP]
> Because your data center must keep running while you upgrade System Center 2012 components one at a time, after you have upgraded the [!INCLUDE[orchshort](Token/orchshort_md.md)] servers to [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)], you can run:
> 
> -   A [!INCLUDE[sc2012](Token/sc2012_md.md)] integration pack on a [!INCLUDE[sc2012](Token/sc2012_md.md)] component.
> -   A [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)] integration pack on a [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)] component.
> -   A [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)] integration pack on a [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] component \(except for Virtual Machine Manager\).
> -   A [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] integration pack on a [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] component \(Virtual Machine Manager\).
> 
> No other configurations are supported.

## See Also
[Tasks to Perform Before You Begin the Upgrade](Tasks-to-Perform-Before-You-Begin-the-Upgrade.md)
[How to Upgrade System Center 2012 SP1 Orchestrator to System Center 2012 R2](How-to-Upgrade-System-Center-2012-SP1-Orchestrator-to-System-Center-2012-R2.md)
[Troubleshoot Your Orchestrator Installation_2](Troubleshoot-Your-Orchestrator-Installation_2.md)


