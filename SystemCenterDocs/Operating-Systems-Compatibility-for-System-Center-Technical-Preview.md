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
Use this information to evaluate if your server\-side operating system environment is ready to support the installation of or upgrade to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]. Use this information whether you are deploying one or multiple components.

|System Center  component|Windows Server 2008|Windows Server 2008 SP2|Windows Server 2008 R2|Windows Server 2008 R2 SP1|[!INCLUDE[win8_server_1](Token/win8_server_1_md.md)] Standard, Datacenter|[!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)] Standard, Datacenter|[!INCLUDE[winthreshold_server_1](Token/winthreshold_server_1_md.md)]\(Server with Desktop Experience\)|[!INCLUDE[winthreshold_server_1](Token/winthreshold_server_1_md.md)]|[!INCLUDE[winthreshold_server_1](Token/winthreshold_server_1_md.md)] Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
|**[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)]** Remote Administration console\*|||●|●|●|●|●|||
|**[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)]** Server\*|||●|●|●|●|●|●||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Management Server||||||●|●|||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Data Warehouse||||||●|●|||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Gateway Server||||||●|●|||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Web Console||||||●|●|||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Operational Database||||||●|●|||
|**[!INCLUDE[om12short](Token/om12short_md.md)]** Reporting Server||||||●|●|||
|**[!INCLUDE[orchshort](Token/orchshort_md.md)]** management server||||||●|●|||
|**[!INCLUDE[orchshort](Token/orchshort_md.md)]** runbook server||||||●|●|||
|**[!INCLUDE[orchshort](Token/orchshort_md.md)]** web service||||||●|●|||
|**[!INCLUDE[orchshort](Token/orchshort_md.md)]** Runbook Designer||||||●|●|||
|**[!INCLUDE[sma_1](Token/sma_1_md.md)]**Web Service|||||||●|●||
|**[!INCLUDE[sma_1](Token/sma_1_md.md)]**Runbook Worker|||||||●|●||
|**[!INCLUDE[sma_1](Token/sma_1_md.md)]**PowerShell Module|||||||●|●||
|**[!INCLUDE[smshort12](Token/smshort12_md.md)]** Management Server||||||●|●|||
|**[!INCLUDE[smshort12](Token/smshort12_md.md)]**<br /><br />Data Warehouse Management Server||||||●|●|||
|**[!INCLUDE[smshort12](Token/smshort12_md.md)]** Database or Data Warehouse Database||||||●|●|||
|**[!INCLUDE[smshort12](Token/smshort12_md.md)]** Self\-Service Portal \(SharePoint Server and Web Content Server\)||||||●|●|||
|**[!INCLUDE[spflong](Token/spflong_md.md)]**|||||||●|●||
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** Management Server|||||||●|||
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** Virtual Machine Hosts||||||●|●||●|
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** Scale\-out File Server||||||●|●||●|
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** PXE Server||||||●|●|||
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** Update Server||||||●|●|||
|**[!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)]** Library||||||●|●|||

> [!IMPORTANT]
> You must download Windows Management Framework 4.0 if you plan to install DPM on Windows Server 2008 R2. See the [Release Notes for System Center Technical Preview 5](Release-Notes-for-System-Center-Technical-Preview-5.md) for more information,

> [!IMPORTANT]
> You can perform  fabric operations such as patching, cluster creation, and cluster rolling upgrades, on either Windows Server 2012 R2 or Windows Server 2016 TP3 hosts managed  by [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]. However   live migration and workload creation are only supported on Windows Server 2016 TP3 hosts and clusters.


