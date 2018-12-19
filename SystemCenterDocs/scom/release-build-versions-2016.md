---
title: System Center 2016 - Operations Manager Release Build Versions
description: This article shows the list of release builds for System Center 2016 - Operations Manager.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 08/12/2018
ms.custom: na
ms.prod: system-center
ms.assetid: 
ms.technology: operations-manager
ms.topic: article
---

# System Center 2016 - Operations Manager build versions
This article describes how to determine your current Microsoft System Center 2016 - Operations Manager version number and the corresponding update rollup.  Each update rollup (UR) release has a link to a support article describing the UR changes as well as links to the package downloads.

>[!NOTE]
>All System Center Operations Manager update rollups are cumulative. This means you do not need to apply them in order, you can always apply the latest update. If you have deployed System Center 2016 - Operations Manager and never applied an update rollup, you can go proceed to install the latest one available. 
>

## Build versions
The following table lists the release history for Operations Manager 2016.

|Build Number |KB |Release Date |Description |  
|-------------|---|-------------|------------|  
|7.2.11719.0 ||September 2016 |General Availability release|  
|7.2.11759.0 |[KB3190029](https://support.microsoft.com/kb/3190029) |October 2016 |Update Rollup 1 |  
|7.2.11822.0 |[KB3209591](https://support.microsoft.com/help/3209591) |February 2017 |Update Rollup 2 |  
|7.2.11878.0 |[KB4016126](https://support.microsoft.com/help/4016126/update-rollup-3-for-system-center-2016-operations-manager) |May 2017 |Update Rollup 3|  
|8.0.10977.0 | [KB4024941](https://support.microsoft.com/help/4024941/update-rollup-4-for-system-center-2016-operations-manager) |October 2017 | Update Rollup 4 <sup>1</sup>|

<sup>1</sup> 
All System Center Operations Manager update rollups are cumulative.  This means you do not need to apply them in order, you can always apply the latest update. However, there is one exception to this upgrade behavior. If you want the ability to uninstall UR4, you should make sure you have previously applied UR2 or UR3, which fixed an uninstall issue. Update rollups subsequent to UR4 can be uninstalled without previous rollups being applied.


## Next steps
See [How to monitor the health of the management group](manage-monitor-health-mg.md) to verify all components are operating normally after performing an update.  
