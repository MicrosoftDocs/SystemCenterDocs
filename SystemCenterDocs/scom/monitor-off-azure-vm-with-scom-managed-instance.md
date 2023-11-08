---
ms.assetid: 
title: Monitor Azure and Off-Azure Virtual machines with Azure Monitor SCOM Managed Instance
description: This article describes how it monitor Azure and Off-Azure virtual machines with SCOM Managed Instance.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/07/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Monitor Azure and Off-Azure Virtual machines with Azure Monitor SCOM Managed Instance

Azure Monitor SCOM Managed Instance provides a cloud-based alternative for Operations Manager users providing monitoring continuity for cloud and on-premises environments across the cloud adoption journey.

## SCOM Managed Instance Agent

In Azure Monitor SCOM Managed Instance, an agent is a service that is installed on a computer that looks for configuration data and proactively collects information for analysis and reporting, measures the health state of monitored objects like an SQL database or logical disk, and executes tasks on demand by an operator or in response to a condition. It allows SCOM Managed Instance to monitor Windows operating systems and the components installed on them, such as a website or an Active Directory domain controller. For more information, see [Azure Monitor SCOM Managed Instance Agents](/system-center/scom/plan-planning-agent-deployment-scom-managed-instance).

## Supported scenarios

The following are the supported monitoring scenarios:

- Azure and Arc-enabled VMs
- On-premises agents that have Line of sight connectivity to Azure
- On-permises agents with no Line of sight connectivity (must use managed Gateway) to Azure

## Prerequisites

Following are the prerequisites required on desired monitoring endpoints:

1. Ensure to Allowlist the following Azure URL on the desired monitoring endpoints:
      `*.workloadnexus.azure.com`
2. Confirm the Line of sight between SCOM Managed Instance and desired monitoring endpoints by running the following command. Obtain LB DNS information by navigating to SCOM Managed Instance **Overview** > **DNS Name**.

    ```    
    Test-NetConnection -ComputerName <LB DNS> -Port 5723
    ```
3. Ensure to install [.NET Framework 4.7.2](https://support.microsoft.com/topic/microsoft-net-framework-4-7-2-offline-installer-for-windows-05a72734-2127-a15d-50cf-daf56d5faec2) or higher on desired monitoring endpoints.
4. Ensure TLS 1.2 or higher is enabled.

To Troubleshooting connectivity problems, see [Troubleshoot issues with Azure Monitor SCOM Managed Instance](https://learn.microsoft.com/system-center/scom/troubleshoot-scom-managed-instance?view=sc-om-2022).

## Install agent for Windows virtual machine

To install agent for Windows virtual machine, see [Install an agent on a computer running Windows by using the Discovery Wizard](https://learn.microsoft.com/system-center/scom/manage-deploy-windows-agent-console#install-an-agent-on-a-computer-running-windows-by-using-the-discovery-wizard).

## Install Managed Gateway

To install Managed Gateway, [download the Gateway software](https://go.microsoft.com/fwlink/?linkid=2252000) and follow [these steps](https://learn.microsoft.com/system-center/scom/deploy-install-gateway-server?view=sc-om-2022&tabs=InstallGatewayServer).
 
## Monitor Linux machine

With SCOM Managed Instance, you can monitor Linux workloads that are on-premises and behind a gateway server. At this stage, we don't support monitoring Linux VMs hosted in Azure. For more information, see [How to monitor on-premises Linux VMs](https://learn.microsoft.com/system-center/scom/manage-deploy-crossplat-agent-console).
