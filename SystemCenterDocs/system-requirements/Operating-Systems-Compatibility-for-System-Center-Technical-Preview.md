---
title: Operating Systems Compatibility for System Center Technical Preview
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 466af3dd-17e5-46b3-b33b-b21a4a65b875
---
# Operating Systems Compatibility for System Center Technical Preview

>Applies To: System Center Technical Preview

Use this information to evaluate if your server-side operating system environment is ready to support the installation of or upgrade to System Center 2016 Technical Preview. Use this information whether you are deploying one or multiple components.

|System Center  component|Windows Server 2008|Windows Server 2008 SP2|Windows Server 2008 R2|Windows Server 2008 R2 SP1|Windows Server® 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server® Technical Preview(Server with Desktop Experience)|Windows Server® Technical Preview|Windows Server® Technical Preview Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
|**DPM** Remote Administration console*|||?|?|?|?|?|||
|**DPM** Server*|||?|?|?|?|?|?||
|**Operations Manager** Management Server||||||?|?|||
|**Operations Manager** Data Warehouse||||||?|?|||
|**Operations Manager** Gateway Server||||||?|?|||
|**Operations Manager** Web Console||||||?|?|||
|**Operations Manager** Operational Database||||||?|?|||
|**Operations Manager** Reporting Server||||||?|?|||
|**Orchestrator** management server||||||?|?|||
|**Orchestrator** runbook server||||||?|?|||
|**Orchestrator** web service||||||?|?|||
|**Orchestrator** Runbook Designer||||||?|?|||
|**Service Management Automation**Web Service|||||||?|?||
|**Service Management Automation**Runbook Worker|||||||?|?||
|**Service Management Automation**PowerShell Module|||||||?|?||
|**Service Manager** Management Server||||||?|?|||
|**Service Manager**<br /><br />Data Warehouse Management Server||||||?|?|||
|**Service Manager** Database or Data Warehouse Database||||||?|?|||
|**Service Manager** Self-Service Portal (SharePoint Server and Web Content Server)||||||?|?|||
|**Service Provider Foundation**|||||||?|?||
|**Virtual Machine Manager** Management Server|||||||?|||
|**Virtual Machine Manager** Virtual Machine Hosts||||||?|?||?|
|**Virtual Machine Manager** Scale-out File Server||||||?|?||?|
|**Virtual Machine Manager** PXE Server||||||?|?|||
|**Virtual Machine Manager** Update Server||||||?|?|||
|**Virtual Machine Manager** Library||||||?|?|||

> [!IMPORTANT]
> You must download Windows Management Framework 4.0 if you plan to install DPM on Windows Server 2008 R2. See the [Release Notes for System Center Technical Preview 5](../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for more information,

> [!IMPORTANT]
> You can perform  fabric operations such as patching, cluster creation, and cluster rolling upgrades, on either Windows Server 2012 R2 or Windows Server 2016 TP3 hosts managed  by System Center 2016 Technical Preview. However   live migration and workload creation are only supported on Windows Server 2016 TP3 hosts and clusters.



