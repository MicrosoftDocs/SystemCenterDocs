---
title: Improving performance for a WAN deployment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6ea9eeb-e924-4fcb-ab52-d9d2dc60d60c
---
# Improving performance for a WAN deployment
If your deployment of [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] for disaster recovery requires [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] to send large amounts of data over a WAN, you can improve [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)]’s use of your WAN latency by adjusting the following registry settings:

**On the remote [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server:**

<pre>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWindowSize
HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWindowSize\Tcp1323Opts</pre>

**On the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server:**

`HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWindowSize\Tcp1323Opts`

For example, using the following settings over a 100 Mbps link with 40 ms latency produces the following results:

|||
|-|-|
|**Settings**||
|On the remote [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server: `HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWindowSize`|524288|
|On both [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers: `HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpWindowSize\Tcp1323Opts`|3|
|**Results**||
|One job running|3.45 MB\/sec|
|Three jobs running|~3.00 MB\/sec per job|

