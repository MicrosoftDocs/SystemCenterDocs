---
ms.assetid: 00667742-29ba-44ea-8dda-587d8944f4a8
title: Monitor VMM
description: This article describes how to monitor VMM with VMM jobs, and System Center Operations Manager
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Monitor VMM

>Applies To: System Center 2016 - Virtual Machine Manager

You configure monitoring and reporting in System Center 2016 - Virtual Machine Manager (VMM) as follows:

- **VMM jobs**: In the VMM console you can monitor the status of processes and operations with VMM jobs.
- **Monitoring in Operations Manager**: To monitor the health and status of VMM servers and the VMM fabric you integrate VMM with System Center Operations Manager
- **Reporting in Operations Manager**: After VMM in integrated with Operations Manager, you can create and view VMM reports


## Monitor with VMM jobs

A VMM job is created for any action that changes the status of a managed object.

- Jobs are composed of steps that are performed sequentially to complete an action. Simple jobs, such as stopping a virtual machine, contain only one step. More complex jobs, or running a wizard, might contain multiple jobs, or job groups.
-  Jobs are tracked in the **Jobs** view in the VMM console. The **Details** tab in the **Jobs** view shows the status of each step in a job.
- Each job is represented by one or more VMM PowerShell cmdlets. You can perform almost any VMM task with [PowerShell](https://technet.microsoft.com/library/jj654428(v=sc.20).aspx). Each wizard includes a **View Script** button on the **Summary** page, that displays the cmdlets that will perform the job that you just requested. You can save Windows PowerShell scripts to the VMM library, and view and run them in **Library** view.
- Each VMM job is independent, and doesn't depend on the status of another job. For example, if you're running jobs to add multiple host servers, the  failure to add one host does not affect the remaining jobs.
When a job completes, an audit record is saved that lists the changes that the job made to the VMM object. You can view the audit record in **Jobs** > **Details** > **Change Tracking**.
- Jobs are started automatically when you perform tasks in the VMM console, or using PowerShell. You can cancel some running jobs, but others, including adding hosts, and system jobs, can't be cancelled after they've started running.
- You can generally restart failed jobs, but note that:
    - If multiple jobs place a VM into a failed state, only the most recent job can be restarted.
    - For jobs that run for a long time, such as virtual machine migration, intermediate results are stored periodically while the job is running, and the Restart action attempts to resume the job from the last known state. All other jobs start from the beginning.


## Monitor with Operations Manager

You can monitor VMM health and status in Operations Manager by installing the VMM management pack which provides a number of dashboards in the Operations Manager console.


**Dashboard** | **Details**
--- | ---
**Virtual Machine Dashboard** | Monitors the health of virtual machines<br/><br/> It shows information about discovered VMs in the VMM fabric. You can view alerts, properties, host, and performance information for the VM.
**VMM Host Dashboard** | Monitors the health of virtualization hosts discovered in the VMM fabric.<br/><br/> It shows information about the host properties, status, VMs, alerts, and performance.
**Fabric Health Dashboard** | Monitors the health of VMM private clouds<br/><br/> For each cloud the dashboard monitors the state of host groups, the compute properties of the cloud (CPU, network adapters etc), storage information such as pools, file share, LUNs, and network monitoring.<br/><br/> A fabric monitoring dashboard diagram view shows the status for each piece of the fabric.<br/><br/> The dashboard can be scoped to physical or virtual resources, or to a particular cloud tenant.

[Learn more](monitors-ops-manager.md) about integrating VMM with Operations Manager.


## Report with Operations Manager

After you've connected VMM to Operations Manager you can view and create reports. VMM provides these default reports:

**Report** | **Details**
--- | ---
**Capacity Utilization** | Details usage for VM hosts and other objects.<br/><br/> Provides an overview of how capacity is being used in your datacenter, and helps you to make resources decisions for supporting your VMs.
**Host Group Forecasting** | Predicts host activity based on history of disk space, memory, disk IO, network IO, and CPU usage.<br/><br/> To use the forecasting reports, SQL Server Analysis Services must be installed on the Operations Manager Reporting server.
**Host Utilization** | Shows the number of virtual machines that are running on each host and average usage, along with total or maximum values for host processors, memory, and disk space.
**Host Utilization Growth** | Shows the percentage change in resource usage and the number of virtual machines that are running on selected hosts during a specified time period.
**Power Savings** | Shows how much power is saved through power optimization.<br/><br/> You can view total hours of processor power saved for a date range and host group, as well as detailed information for each host in a host group.
**SAN Usage Forecasting** | Predicts SAN usage based on history.
**Virtual Machine Allocation** | Provides information about allocation of virtual machines.
**Virtual Machine Utilization** | Provides information about resource utilization by virtual machines, including average usage and total or maximum values for virtual machine processors, memory, and disk space.
**Virtualization Candidates** | Helps identify physical computers that are good candidates for conversion to virtual machines.<br/><br/> You can use this report to identify little-used servers and display average values for a set of commonly requested performance counters for CPU, memory, and disk usage, along with hardware configurations, including processor speed, number of processors, and total RAM.<br/><br/> You can limit the report to computers that meet specified CPU and RAM requirements, and you can sort the results by selected columns in the report.

## View reports

You can view reports in the Reporting workspace in System Center Operations Manager, or by using a web browser and entering this address: `http://ReportingServerName:port/reports`. You can optionally specify "https" instead of http.

- `ReportingServerName` is the name of the Operations Manager reporting server.
- `port` is 80 for HTTP and 443 for HTTPS
- `reports` is the reporting server virtual directory, by default: **reports**
