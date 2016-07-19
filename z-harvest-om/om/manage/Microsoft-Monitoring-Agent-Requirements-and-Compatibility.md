---
title: Microsoft Monitoring Agent Requirements and Compatibility
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4161fc9b-3471-480c-905a-33dbf129a99f
author:mgoedtel
manager:cfreemanwa
---
# Microsoft Monitoring Agent Requirements and Compatibility
  
## System Requirements  
Microsoft Monitoring Agent includes many features that each have different requirements:  
  
-   [Infrastructure and Workload Monitoring with System Center Operations Manager](../../om/manage/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md#bkmk_InfraWrkflowMonitor)  
  
-   [APM with System Center Operations Manager](../../om/manage/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md#bkmk_APMwithSysCenter)  
  
-   [APM with Stand\-Alone Monitoring using IntelliTrace log as an output](../../om/manage/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md#bkmk_APMwithMonitor)  
  
### <a name="bkmk_InfraWrkflowMonitor"></a>Infrastructure and Workload Monitoring with System Center Operations Manager  
When connected to System Center Operations Manager, the agent calculates the health state of the monitored computers and objects, and then reports back to the management server. The management servers centrally distribute the configuration to agents and store data received from the monitored computers. Management packs installed on the management server control this type of data collected, tasks, and alerts you receive in Operations Manager.  
  
**Supported Operating System**  
  
Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 SP2, Windows Server 2008 R2, Windows Server 2003 SP2, Windows 8, Windows 8.1, Windows Embedded POSReady 2009, Windows Embedded Standard 7 SP1,  Windows XP SP3, Windows XP SP2  
  
-   File system: %SYSTEMDRIVE% must be formatted with the NTFS file system.  
  
-   Processor Architectures: x64, x86.  
  
-   Microsoft Core XML Services \(MSXML\) version: Microsoft Core XML Services 6.0 is required when installing on Windows Server 2003.  
  
-   Windows PowerShell 2.0 or Windows PowerShell 3.0.  
  
-   Microsoft .NET Framework 3.5 or later.  
  
> [!NOTE]  
> Windows PowerShell is required to run System Center Operations Manager management packs that use PowerShell scripts.  
  
### <a name="bkmk_APMwithSysCenter"></a>APM with System Center Operations Manager  
By using APM with System Center Operations Manager, you can monitor web applications and Windows NT Services written with .NET Framework.  
  
-   Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008  
  
    Windows 8.1, Windows 8, Windows 7  
  
-   Internet Information Services \(IIS\) 8.5, IIS 8, IIS 7.5, IIS 7  
  
-   .NET Framework 2.0 and above  
  
-   Processor Architectures: x64, x86  
  
### <a name="bkmk_APMwithMonitor"></a>APM with Stand\-Alone Monitoring using IntelliTrace log as an output  
By using APM with stand\-alone monitoring using IntelliTrace logs as an output, you can monitor web applications written with .NET Framework.  
  
-   Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008  
  
-   Windows 8.1, Windows 8, Windows 7  
  
-   IIS 8.5, IIS 8, IIS 7.5, or IIS 7  
  
-   .NET Framework 2.0 and above  
  
-   Windows PowerShell 2.0 or Windows PowerShell 3.0  
  
-   Processor Architectures: x64, x86  
  
## Compatible Products  
  
### System Center:  
  
-   System Center 2012 R2 Operations Manager  
  
-   System Center 2012 Service Pack 1 \(SP1\) – Operations Manager. If you want to use Application Performance Monitoring \(APM\), you must be running System Center 2012 SP1 UR 4 or later.  
  
-   System Center 2012 – Operations Manager. If you want to use APM, you must upgrade to System Center 2012 SP1 UR 4 or later.  
  
-   System Center Operations Manager 2007 R2. APM is not available in this version of Operations Manager.  
  
### Visual Studio:  
  
-   Microsoft Visual Studio Ultimate 2013 or a later version \(**recommended**\). You can open IntelliTrace logs collected with stand\-alone monitoring, and System Center.  
  
-   Microsoft Visual Studio Ultimate 2012 Update 2 or a later version. You can open IntelliTrace logs collected with stand\-alone monitoring, and System Center.  
  
    > [!NOTE]  
    > When using Visual Studio Ultimate 2012 to view APM IntelliTrace logs, you only see details about exceptions but not performance data. To see complete APM traces, including performance events, use Visual Studio Ultimate 2013 or a later release.  
  
