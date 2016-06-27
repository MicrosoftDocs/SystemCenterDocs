---
title: Using Reporting in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce536f0a-0614-4220-9081-53f4ecec1a3b
---
# Using Reporting in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

After you connect Virtual Machine Manager (VMM) with System Center Operations Manager, you can create and view reports relating to VMM managed components, including virtual machine hosts, virtual machines, and VMM-related servers (for example, library servers.)

> [!NOTE]
> For information about connecting VMM to System Center Operations Manager, see [How to connect VMM to Operations Manager](How-to-connect-VMM-to-Operations-Manager.md).

You can view reports in the **Reporting** workspace in System Center Operations Manager, or by using a web browser and entering this address:

`http[s]://<OpsMgrReportServer>[:<port>]/<reports>`

-   `<OpsMgrReportServer>` is the reporting server

-   `<port>` is 80 for http and 443 for https, by default

-   `<reports>` is the reporting server virtual directory, by default, `reports`

You can view the following preconfigured reports for VMM managed components.

> [!NOTE]
> To use the forecasting reports, SQL Server Analysis Services must be installed on the System Center Operations Manager Reporting server. For more information, see [How to configure SQL Server Analysis Services for VMM](How-to-configure-SQL-Server-Analysis-Services-for-VMM.md).

|Report|Description|
|----------|---------------|
|Capacity Utilization|Details usage for virtual machine hosts and other objects. This report provides an overview of how capacity is being used in your datacenter. This information can inform decisions about how many systems you need to support your virtual machines.|
|Host Group Forecasting|Predicts host activity based on history of disk space, memory, disk IO, network IO, and CPU usage.|
|Host Utilization|Shows the number of virtual machines that are running on each host and average usage, along with total or maximum values for host processors, memory, and disk space.|
|Host Utilization Growth|Shows the percentage change in resource usage and the number of virtual machines that are running on selected hosts during a specified time period.|
|Power Savings|Shows how much power is saved through Power Optimization. You can view total hours of processor power saved for a date range and host group, as well as detailed information for each host in a host group. For more information about Power Optimization, see [Configuring dynamic optimization and power optimization in VMM](Configuring-dynamic-optimization-and-power-optimization-in-VMM.md).|
|SAN Usage Forecasting|Predicts SAN usage based on history.|
|Virtual Machine Allocation|Provides information about allocation of virtual machines.|
|Virtual Machine Utilization|Provides information about resource utilization by virtual machines, including average usage and total or maximum values for virtual machine processors, memory, and disk space.|
|Virtualization Candidates|Helps identify physical computers that are good candidates for conversion to virtual machines. You can use the Virtualization Candidates report to identify little-used servers and display average values for a set of commonly requested performance counters for CPU, memory, and disk usage, along with hardware configurations, including processor speed, number of processors, and total RAM. You can limit the report to computers that meet specified CPU and RAM requirements, and you can sort the results by selected columns in the report.|

You can also design your own reports.

## See Also
[Integrating VMM and System Center Operations Manager](Integrating-VMM-and-System-Center-Operations-Manager.md)
[Monitoring and reporting for VMM resources](Monitoring-and-reporting-for-VMM-resources.md)



