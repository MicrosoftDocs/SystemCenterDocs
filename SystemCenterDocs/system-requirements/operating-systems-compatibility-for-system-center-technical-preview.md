---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  cfreemanwa
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-07-01
title:  Operating Systems Compatibility for System Center Technical Preview
ms.technology:  system-center-2016
ms.assetid:  466af3dd-17e5-46b3-b33b-b21a4a65b875
---

# Operating Systems Compatibility for System Center Technical Preview

>Applies To: System Center Technical Preview

Use this information to evaluate if your server-side operating system environment is ready to support the installation of or upgrade to System Center 2016 Technical Preview. Use this information whether you are deploying one or multiple components.

|System Center  component|Windows Server 2008 R2|Windows Server 2008 R2 SP1|Windows Server 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server Technical Preview(Server with Desktop Experience)|Windows Server Technical Preview|Windows Server Technical Preview Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
|**DPM** Remote Administration console*|&#8226;|&#8226;|&#8226;|&#8226;|&#8226;|||
|**DPM** Server*|&#8226;|&#8226;|&#8226;|&#8226;|&#8226;|&#8226;||
|**Operations Manager** Management Server||||&#8226;|&#8226;|||
|**Operations Manager** Data Warehouse||||&#8226;|&#8226;|||
|**Operations Manager** Gateway Server||||&#8226;|&#8226;|||
|**Operations Manager** Web Console||||&#8226;|&#8226;|||
|**Operations Manager** Operational Database||||&#8226;|&#8226;|||
|**Operations Manager** Reporting Server||||&#8226;|&#8226;|||
|**Orchestrator** management server||||&#8226;|&#8226;|||
|**Orchestrator** runbook server||||&#8226;|&#8226;|||
|**Orchestrator** web service||||&#8226;|&#8226;|||
|**Orchestrator** Runbook Designer||||&#8226;|&#8226;|||
|**Service Management Automation**Web Service|||||&#8226;|&#8226;||
|**Service Management Automation**Runbook Worker|||||&#8226;|&#8226;||
|**Service Management Automation**PowerShell Module|||||&#8226;|&#8226;||
|**Service Manager** Management Server||||&#8226;|&#8226;|||
|**Service Manager**<br /><br />Data Warehouse Management Server||||&#8226;|&#8226;|||
|**Service Manager** Database or Data Warehouse Database||||&#8226;|&#8226;|||
|**Service Manager** Self-Service Portal (SharePoint Server and Web Content Server)||||&#8226;|&#8226;|||
|**Service Provider Foundation**|||||&#8226;|&#8226;||
|**Virtual Machine Manager** Management Server|||||&#8226;|||
|**Virtual Machine Manager** Virtual Machine Hosts||||&#8226;|&#8226;||&#8226;|
|**Virtual Machine Manager** Scale-out File Server||||&#8226;|&#8226;||&#8226;|
|**Virtual Machine Manager** PXE Server||||&#8226;|&#8226;|||
|**Virtual Machine Manager** Update Server||||&#8226;|&#8226;|||
|**Virtual Machine Manager** Library||||&#8226;|&#8226;|||

> [!IMPORTANT]
> You must download Windows Management Framework 4.0 if you plan to install DPM on Windows Server 2008 R2. See the [Release Notes for System Center Technical Preview 5](../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for more information,

> [!IMPORTANT]
> You can perform  fabric operations such as patching, cluster creation, and cluster rolling upgrades, on either Windows Server 2012 R2 or Windows Server 2016 TP3 hosts managed  by System Center 2016 Technical Preview. However   live migration and workload creation are only supported on Windows Server 2016 TP3 hosts and clusters.
