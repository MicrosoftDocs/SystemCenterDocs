---
title: Back up and restore workloads in workgroups and untrusted domains
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e050ac1-20d7-44e5-97a5-45b245a4f9ee
---
# Back up and restore workloads in workgroups and untrusted domains
[!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] can protect computers that are in untrusted domains or workgroups. You can authenticate these computers using a local user account \(NTLM authentication\), or using certificates. You set up protection as follows:

1.  **Install a certificate**—If you want to use certificate authentication install a certificate on the DPM server and on the computer you want to protect.

2.  **Install the agent**—Install the agent on the computer you want to protect.

3.  **Recognize the DPM server**—Configure the computer to recognize the DPM server for performing backups. To do this you’ll run the SetDPMServer command.

4.  **Attach the computer**—Lastly you’ll need to attach the protected computer to the DPM server.

Before you started check the supported protection scenarios in the table below. Then follow the instructions depending which type of authentication you want to use:

-   [Set up protection with NTLM authentication](../Topic/Set-up-protection-with-NTLM-authentication.md)

-   [Set up protection with certificate authentication](../Topic/Set-up-protection-with-certificate-authentication.md)

## Supported protection scenarios

||Support|
|-|-----------|
|Files|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM and certificate authentication for single server. Certificate authentication only for cluster.|
|System State|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM authentication only|
|SQL Server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />Mirroring not supported.<br /><br />NTLM and certificate authentication for single server. Certificate authentication only for cluster.|
|Hyper\-V server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />NTLM and certificate authentication|
|Hyper\-V cluster|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />CSV not supported.<br /><br />Certificate authentication only|
|Exchange Server|Workgroup: Not applicable<br /><br />Untrusted: Supported for single server only. Cluster not supported. CCR, SCR, DAG not supported. LCR supported.<br /><br />NTLM authentication only|
|Secondary DPM server \(For backup of primary DPM server|Workgroup: Supported<br /><br />Untrusted: Supported<br /><br />Certificate authentication only|
|SharePoint|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|Client computers|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|Bare metal recovery \(BMR\)|Workgroup: Not supported<br /><br />Untrusted: Not supported|
|End\-user recovery|Workgroup: Not supported<br /><br />Untrusted: Not supported|

## Network settings

|Settings|Computer in workgroup or untrusted domain|
|------------|---------------------------------------------|
|Control data|Protocol: DCOM<br /><br />Default port: 135<br /><br />Authentication: NTLM\/certificate|
|File transfer|Protocol: Winsock<br /><br />Default port: 5718 and 5719<br /><br />Authentication: NTLM\/certificate|
|DPM account requirements|Local account without admin rights on DPM server. Uses NTLM v2 communication|
|Certificate requirements||
|Agent installation|Agent installed on protected computer|
|Perimeter network|Perimeter network protection not supported.|
|IPSEC|Ensure IPSEC doesn’t block communications.|

