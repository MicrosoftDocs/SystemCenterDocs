---
title: Guidance for load balancing System Center - Service Manager
description: Use network load balancing in Windows Server to configure a pool of computers so that they take turns responding to requests.
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
ms.assetid: 129bc3fe-8a6f-4edb-b15f-1f0d42e6bf24
---

# Guidance for load balancing in Service Manager

>Applies To: System Center 2016 - Service Manager

This article describes how you can load-balance Service Manager management servers in Service Manager.  

## Load-balancing Service Manager management servers

You can use network Load Balancing \(NLB\) in Windows Server to configure a pool of computers so that they take turns responding to requests. In System Center - Service Manager, the initial Service Manager management server that you deploy is the server that processes workflows. You can deploy additional management servers to provide failover for a failed initial management server and to provide load balancing for handling Service Manager console. For more information about Windows&nbsp;Server&nbsp;2008 NLB, see the [Network Load Balancing Deployment Guide](http://go.microsoft.com/fwlink/p/?LinkID=183567). For more information about additional Service Manager management servers, see [Deploying Additional Service Manager Management Servers](deploy-deploying-additional-service-manager-management-servers.md).  

 As a minimum, you have to deploy an initial Service Manager management server-the management server that hosts the workflow processes-and at least one additional Service Manager management server. In an environment of this kind that consists of two Service Manager management servers, configure NLB to use both management servers, as shown in the following illustration.  

 ![network load balancing one](../media/deploy-networkloadbalancingfigureone.png)  

 If you deploy two or more additional Service Manager management servers, you can isolate the initial Service Manager management server from the NLB pool. This reduces the workload on the initial Service Manager management server, resulting in better workflow performance. It also load\-balances all of the Service Manager consoles across the remaining Service Manager management servers. This scenario is shown in the following illustration.  

 ![network load balancing two](../media/deploy-networkloadbalancingfiguretwo.png)

## Next steps

- Review [Complete deployment by backing up the encryption key](deploy-completing-deployment-by-backing-up-the-encryption-key.md) to use the Encryption Key Backup or Restore Wizard to back up and restore encryption keys.
