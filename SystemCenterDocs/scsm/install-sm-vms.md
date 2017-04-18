---
title: Install Service Manager on virtual machines
description: This article provides guidance that you should consider when you install Service Manager in a Hyper-V virtual environment.
manager:  carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3614b9db-20de-41c0-9780-a27624258da0
---

# Install Service Manager on virtual machines

>Applies To: System Center 2016 - Service Manager

This article provides guidance that you should consider when you install System Center - Service Manager in a Hyper\-V virtual environment. If you are installing Microsoft SQL&nbsp;Server into an environment without Hyper\-V, consult your vendor's documentation for guidance regarding the use of SQL&nbsp;Server.  

## Deploying SQL&nbsp;Server in a virtual environment  
 Before you deploy SQL&nbsp;Server in a Hyper\-V environment, see [Running SQL Server&nbsp;2008 in a Hyper\-V Environment](http://go.microsoft.com/fwlink/p/?LinkID=144622). Keep the following in mind when you prepare a virtual environment for SQL&nbsp;Server:  

-   Using a dynamic virtual hard drive \(VHD\) can decrease performance. We do not recommend using a VHD.  

-   Allocate at least two virtual CPUs for the instance of SQL Server.  

-   Do not allocate more virtual CPUs than the number of available logical CPUs.  

-   If you observe a drop in Service Manager performance in a virtual environment, check CPU and memory utilization on the virtual machines that are hosting the instance of SQL&nbsp;Server and the Service Manager management server. If CPU utilization is near 100&nbsp;percent, either allocate additional virtual CPUs or reduce the number of concurrent Service Manager console sessions.  

## Memory  
 The amount of memory you have in your logical computer and the amount of memory you allocate to each virtual machine are critical. If you deploy an instance of SQL&nbsp;Server, Service Manager management server, and Service Manager console to the same virtual machine, the memory requirements are cumulative. You need enough memory to meet the requirements of each part of Service Manager. In this environment, 8&nbsp;gigabytes \(GB\) of memory is the minimum recommended amount.  

## Deploying Service Manager databases in a virtual environment  
If you are installing Service Manager and data warehouse databases on virtual machines, we recommend that you use one virtual machine for the Service Manager database and another virtual machine for the data warehouse databases. Furthermore, each virtual machine should be configured for two CPUs.

## Next steps

- Review [Configure PowerShell to run in Service Manager](../sm/deploy/deploy-configure-windows-powershell-to-run-in-system-center-2016-service-manager.md) to set execution policy to RemoteSigned and import the data warehouse cmdlet module. 
