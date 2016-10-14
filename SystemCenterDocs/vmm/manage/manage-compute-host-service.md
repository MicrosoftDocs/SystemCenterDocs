---
ms.assetid: 74520b3d-e41d-4abd-9da8-8c0bc6d34c37
title: Service hosts and virtual machines in the VMM compute fabric
description: This article describes how to service host and virtual machines in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---



# Service hosts and virtual machines in the VMM compute fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to learn about service Hyper-V hosts and virtual machines in the VMM fabric.

You can service hosts and VMs by:

- **Setting up servicing windows**: Servicing windows provide a method for scheduling servicing outside VMM. You can associate a servicing window with individual hosts, virtual machines, or services. Before using other applications to schedule maintenance tasks, you can use Windows PowerShell scripts or custom applications to query the object and determines if it is currently in a servicing window. Servicing windows do not interfere with the regular use and functionality of VMM.
- **Placing hosts in maintenance mode**: You can start maintenance mode for a virtual machine host whenever you need to perform maintenance tasks on the physical host, such as applying security updates or replacing hardware on the physical host computer. You can place Hyper-V hosts and VMware ESX hosts in the VMM fabric into maintenance mode. Note that:

	- When a host is in maintenance mode, the following restrictions apply:
		- VMs can't be created on the host.
		- VMs can't be moved to the host.
		- The host has a zero rating and can't be selected for placement.
		- The host is excluded from dynamic optimization.

	- For ESX hosts, if the VMware Distributed Resources Scheduler is not configured, all virtual machines on the host must be either manually shut down or moved to another host to successfully start maintenance mode on an ESX host.
	- If you're monitoring with Operations Manager and you have maintenance mode enabled for monitoring, the Operations Manager agent suppresses alerts, notifications, rules, monitors, automatic responses, state changes, and new alerts for hosts that are placed in maintenance mode.

## Set up a servicing window

1. In the VMM console, click **Settings** > **Create** > **Create Servicing Window**.
2. In **New Servicing Window**, specify a name and optional description for the window.
3. In **Category**, enter or select the category of servicing window.
4. In **Start time**, enter the date, time of day, and time zone for the maintenance window.
5. In **Duration**, specify the number of hours or minutes in the servicing window.
6. Under **Recurrence pattern**, select the frequency (Daily, Weekly, or Monthly), and then schedule the occurrences within that frequency.
7. After the window is set up, you can assign it to a host or VM. To assign to a host, click the host properties > **Servicing Window** > **Manage**, and select the window you want to add to the host.



## Put hosts in maintenance mode

1. In the VMM console, click **Fabric**  > **Fabric Resources** > **Servers** > **All Hosts**.
2. Select the host to place in maintenance mode, and in the **Host** group click **Start Maintenance Mode**. You can select to:

	- You can select **Move all virtual machines to other hosts in the cluster** if you want to move all highly available VMs to other hosts in the cluster (the host must be in a cluster that's capable of live migration)
	- Otherwise, select **Place all running virtual machines into a saved state**. Note that list causes a loss of service for users currently using the VM.
3. You can verify that host is in maintenance mode by checking its status in **Fabric** > **Hosts**.

To bring a host out of maintenance node, select it and click **Stop Maintenance Mode**. Note that VMM doesn't automatically restart the VM, and doesn't automatically migrate VMs back to the host.
