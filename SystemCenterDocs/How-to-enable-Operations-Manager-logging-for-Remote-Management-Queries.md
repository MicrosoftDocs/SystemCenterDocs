---
title: How to enable Operations Manager logging for Remote Management Queries
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4803596-4c4c-4cc2-a48f-27147164b100
---
# How to enable Operations Manager logging for Remote Management Queries
This procedure describes how to enable logging for Windows Remote Management queries

## Enable Operations Manager Logging for Windows Remote Management
This verbose tracing method is used to see the Windows Remote Management \(WinRM\) queries used by Operations Manager to gather data from the agent. If you suspect there is a problem with the WinRM connection, this log provides detailed information that can help with troubleshooting.

#### To trace WinRM events

1.  On the Management server that is monitoring the UNIX or Linux agent, open a command prompt.

2.  Type the following commands at the command prompt:

    1.  cd C:\\Program Files\\System Center Operations Manager 2012\\tools

    2.  StopTracing.cmd

    3.  StartTracing.cmd VER

3.  Reproduce the failing issue in Operations Manager.

4.  Type the following commands at the command prompt:

    1.  StopTracing.cmd

    2.  FormatTracing.cmd

5.  Search for WS\-Man in the TracingGuidsNative.log file.

> [!NOTE]
> WinRM is also known as WS\-Management \(WS\-Man\).

> [!NOTE]
> The FormatTracing command opens a Windows Explorer window displaying the c:\\Windows\\temp\\OpsMgrTrace directory. The TracingGuidsNative.log file is in that directory.

