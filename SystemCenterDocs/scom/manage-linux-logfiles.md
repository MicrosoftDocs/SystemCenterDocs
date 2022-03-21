---
ms.assetid:
title: Log file monitoring in System Center Operations Manager
description: This article provides an overview of the Linux log file monitoring in System Center Operations Manager
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 04/02/2020
ms.custom: na
ms.prod: system-center
monikerRange: '>=sc-om-1801'
ms.technology: operations-manager
ms.topic: article
---

# Linux Log file monitoring in System Center Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

System Center Operations Manager now has enhanced log file monitoring capabilities for Linux servers by using the newest version of the agent that uses Fluentd. This update provides the following improvements over previous log file monitoring:

- Wild card characters in log file name and path.
- New match patterns for customizable log search like simple match, exclusive match, correlated match, repeated correlation and exclusive correlation.
- Support for generic Fluentd plugins published by the fluentd community.

## Basic operation
The basic operation of log file monitoring in Linux includes the following steps:

1. Record is written to a log on a Linux agent.
2. Fluentd collects the record and creates an event on pattern match.
3. Event is sent to OMED service on management server.
3. Rules and monitors in a custom management pack collect events and create alerts in Operations Manager.


::: moniker range="sc-om-1801"

[!INCLUDE [log-file-monitoring-1801-1807.md](../includes/linux-log-file-monitoring-1801-1807.md)]

::: moniker-end

::: moniker range="sc-om-1807"

[!INCLUDE [log-file-monitoring-1801-1807.md](../includes/linux-log-file-monitoring-1801-1807.md)]

::: moniker-end

::: moniker range=">=sc-om-2019"

[!INCLUDE [log-file-monitoring-2019.md](../includes/linux-log-file-monitoring-2019.md)]

::: moniker-end

## Next steps

* To create a custom view to review the monitoring data from your custom log file management pack, review [Using views in Operations Manager](/previous-versions/system-center/system-center-2012-R2/hh212694(v=sc.12)).  

* Review [Viewing active alerts and details](manage-alert-view-alerts-details.md) to learn how to investigate issues identified by your custom log file management pack.
