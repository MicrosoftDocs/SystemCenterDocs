---
title: Get Dial-up Status
description: This article describes the functionality of Get Dial-up Status activity.
ms.custom: engagement-fy23
ms.date: 04/16/2026
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: ab465f97-ef96-41b8-bae5-57c5413af14a
caps.latest.revision: 5
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
---

# Get Dial-up Status

> [!NOTE]
> Windows Server 2008, 2008 R2, 2012 and 2012 R2 have reached End of Support (EOS). Review your usage and plan OS upgrades and migrations accordingly. For more information, see End of support for: <br>
>- [Windows Server 2008 and Windows Server 2008 R2](/troubleshoot/windows-server/windows-server-eos-faq/end-of-support-windows-server-2008-2008r2)
>- [Windows Server 2012](/windows/release-health/status-windows-server-2012)
>- [Windows Server 2012 R2](/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)<br>
>[Perform in-place upgrade to Windows Server 2016, 2019, 2022, or 2025](/azure/virtual-machines/windows-in-place-upgrade#perform-in-place-upgrade-to-windows-server-2016-2019-2022-or-2025).

The Get Dial-up Status activity retrieves the status of a dial-up or VPN network connection on the Runbook server. For more information on creating a network connection in Windows Server 2008, see [Establish Network Connections](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/gg252606(v=ws.10))  

## Configure the Get Dial-up Status Activity

 Use the following information to configure the Get Dial-up Status activity.  

> [!NOTE]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

### Connection Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Dial-up or VPN entry**|Enter the name of the entry as entered in the address book, or select the ellipsis **(…)** button and select the entry from the Remote Access Phone Book.|  

### Published Data

The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Dial-up or VPN name|The name assigned to the dial-up connection|  
|Line status|Indicates whether the network connection is connected or disconnected|

