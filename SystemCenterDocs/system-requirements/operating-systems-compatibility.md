---
description:  
manager:  cfreeman
ms.topic:  article
author:  cfreemanwa
ms.author: cfreeman
ms.prod:  system-center-threshold
keywords:  
ms.date:  10/12/2016
title:  Operating Systems Compatibility for System Center 2016
ms.technology:  system-center-2016
ms.assetid:  466af3dd-17e5-46b3-b33b-b21a4a65b875
---

# Operating Systems Compatibility for System Center 2016

>Applies To: System Center 2016

Use this information to evaluate if your server-side operating system environment is ready to support the installation of or upgrade to System Center 2016. Use this information whether you are deploying one or multiple components.

|System Center  component|Windows Server 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server 2016|Windows Server 2016 (Server with Desktop Experience)|Windows Server 2016 Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|
|**DPM** Remote Administration console*|&#8226;|&#8226;||&#8226;||
|**DPM** Server*|&#8226;|&#8226;|&#8226;|&#8226;||
|**Operations Manager** Management Server||&#8226;|&#8226;|&#8226;||
|**Operations Manager** Data Warehouse||&#8226;||&#8226;||
|**Operations Manager** Gateway Server||&#8226;||&#8226;||
|**Operations Manager** Web Console||&#8226;|&#8226;|&#8226;||
|**Operations Manager** Operational Database||&#8226;||&#8226;||
|**Operations Manager** Reporting Server||&#8226;||&#8226;||
|**Orchestrator** Management Server||&#8226;||&#8226;||
|**Orchestrator** Runbook Server||&#8226;||&#8226;||
|**Orchestrator** Web Service||&#8226;||&#8226;||
|**Orchestrator** Runbook Designer||&#8226;||&#8226;||
|**Service Management Automation** Web Service|||&#8226;|&#8226;||
|**Service Management Automation** Runbook Worker|||&#8226;|&#8226;||
|**Service Management Automation** PowerShell Module|||&#8226;|&#8226;||
|**Service Manager** Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Data Warehouse Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Database or Data Warehouse Database||&#8226;|&#8226;|&#8226;||
|**Service Manager** Self-Service Portal (HTML 5)||&#8226;|&#8226;|&#8226;||
|**Service Provider Foundation**|||&#8226;|&#8226;||
|**Virtual Machine Manager** Management Server|||&#8226;|&#8226;||
|**Virtual Machine Manager** Virtual Machine Hosts||&#8226;|&#8226;|&#8226;|&#8226;|
|**Virtual Machine Manager** Scale-out File Server||&#8226;|&#8226;|&#8226;|&#8226;|
|**Virtual Machine Manager** PXE Server||&#8226;||&#8226;||
|**Virtual Machine Manager** Update Server||&#8226;||&#8226;||
|**Virtual Machine Manager** Library||&#8226;||&#8226;|||

> [!IMPORTANT]
> You must download Windows Management Framework 4.0 if you plan to install DPM on Windows Server 2008 R2. See the [Release Notes for System Center 2016](../get-started/release-notes.md) for more information,

> [!IMPORTANT]
> You can perform fabric operations such as patching, cluster creation, and cluster rolling upgrades, on either **Windows Server 2012 R2** or **Windows Server 2016** hosts managed by System Center 2016. However, live migration and workload creation are only supported on Windows Server 2016 hosts and clusters.

> [!Note]
> When you install **Windows Server 2016** using the Setup wizard, you can choose between **Windows Server 2016** and **Windows Server (Server with Desktop Experience)**. The Server with Desktop Experience option is the Windows Server 2016 equivalent of the Full installation option available in Windows Server 2012 R2 with the Desktop Experience feature installed. If you do not make a choice in the Setup wizard, **Windows Server 2016** is installed; this is the Server Core installation option.
