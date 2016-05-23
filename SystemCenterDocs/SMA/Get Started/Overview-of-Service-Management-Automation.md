---
title: Overview of Service Management Automation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-management-automation-(sma)
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 490faacf-b798-40ea-bb6e-106e6ad7ebaf
---
# Overview of Service Management Automation
[!INCLUDE[sma_1](../../Token/sma_1_md.md)] is a set of tools that is integrated as the [!INCLUDE[sma_1](../../Token/sma_1_md.md)] extension in [!INCLUDE[katal_1](../../Token/katal_1_md.md)]. IT pros and IT developers can use [!INCLUDE[sma_1](../../Token/sma_1_md.md)] to construct, run, and manage runbooks to integrate, orchestrate, and automate IT business processes. [!INCLUDE[sma_1](../../Token/sma_1_md.md)] runbooks run on the Windows PowerShell workflow engine.

## What’s in [!INCLUDE[sma_1](../../Token/sma_1_md.md)]?
[!INCLUDE[sma_1](../../Token/sma_1_md.md)] uses the following three underlying components that are connected to [!INCLUDE[katal_2](../../Token/katal_2_md.md)] through the [!INCLUDE[sma_1](../../Token/sma_1_md.md)] service endpoint:

**Web service**

-   Connects to [!INCLUDE[katal_2](../../Token/katal_2_md.md)]

-   Distributes runbook jobs to runbook workers

-   Supports HTTPS

-   Enables security group to control access

**Runbook worker**

-   Executes runbook jobs

-   Runs under a service account

**PowerShell module**

-   Enables [!INCLUDE[sma_1](../../Token/sma_1_md.md)] management by using Windows PowerShell cmdlets

### Should I use [!INCLUDE[sma_1](../../Token/sma_1_md.md)] or [!INCLUDE[scor_threshold_1](../../Token/scor_threshold_1_md.md)]?
In [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)], the [!INCLUDE[orchshort](../../Token/orchshort_md.md)] component enables you to automate business processes and IT operations in your data center without scripting or programming. [!INCLUDE[orchshort](../../Token/orchshort_md.md)] is a feature in [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)]. If you already have [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)] installed, and you do not plan to install [!INCLUDE[katal_2](../../Token/katal_2_md.md)], use [!INCLUDE[orchshort](../../Token/orchshort_md.md)].

[!INCLUDE[sma_1](../../Token/sma_1_md.md)] in [!INCLUDE[katal_2](../../Token/katal_2_md.md)] enables you to automate processes within the [!INCLUDE[katal_2](../../Token/katal_2_md.md)]. Because [!INCLUDE[sma_1](../../Token/sma_1_md.md)] runs Windows PowerShell workflows, you can also use Windows PowerShell cmdlets to run other [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)] components, including [!INCLUDE[orchshort](../../Token/orchshort_md.md)]. If you are planning to use the [!INCLUDE[katal_2](../../Token/katal_2_md.md)], use [!INCLUDE[sma_1](../../Token/sma_1_md.md)], and then you can continue to leverage your [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)] installation \(if one exists\).

> [!IMPORTANT]
> The [Service Management Automation Developer's Guide](http://go.microsoft.com/fwlink/?LinkId=398741) is now available. This is a set of REST API reference documentation for the Service Management Automation web service.


