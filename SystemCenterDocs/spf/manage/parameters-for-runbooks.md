---
title: Parameters for Runbooks Invoked from Service Provider Foundation
description: This topic provides a list of parameters you can use when invoking runbooks from Service Provider Foundation.
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c3c412d-34be-4311-8d8a-1f74f2bfba8f
author:bwren
manager:cfreeman
ms.author: raynew
---
# Parameters for Runbooks Invoked from Service Provider Foundation
>Apples To: System Center 2016

This topic describes the parameters that Service Provider Foundation automatically provides to a runbook that it invokes in System Center 2016 Orchestrator, as described in [How to Automate a Runbook from Service Provider Foundation](../Manage/How-to-Automate-a-Runbook.md). A runbook is not required to process all the parameters it receives, and will simply ignore the parameters which have no purpose in the runbook.  

## Parameters for a new virtual machine  
The following table lists the parameters available when a new virtual machine is created. All parameters are optional unless indicated as required.  

|Parameter|Data Type|  
|-------------|-------------|  
|StampId \(required\)|Guid|  
|Name \(StampID name - required\)|String|  
|CloudId \(required\)|Guid|  
|VMTemplateId|Guid|  
|HardwareProfileId|Guid|  
|VirtualHardDiskId|Guid|  
|Description|String|  
|CostCenter|String|  
|Tag|String|  
|ComputerName|String|  
|BlockDynamicOptimization|Boolean|  
|CPULimitForMigration|Boolean|  
|CPULimitFunctionality|Boolean|  
|CPURelativeWeight|Int32|  
|DelayStartSeconds|Int32|  
|Domain|String|  
|UserName|String|  
|Password|String|  
|DynamicMemoryBufferPercentage|Int32|  
|DynamicMemoryEnabled|Boolean|  
|DynamicMemoryMaximumMB|Int32|  
|FullName|String|  
|Memory|Int32|  
|MemoryWeight|Int32|  
|OrganizationName|String|  
|StartAction|String|  
|StartVM|Boolean|  
|StopAction|String|  
|CPUCount|Byte|  
|Owner|PSObject|  
|ProductKey|String|  
|WorkGroup|String|  
|TimeZone|Int32|  
|RunAsAccountUserName|String|  
|LocalAdminRunAsAccountName|String|  
|LocalAdminUserName|String|  
|LocalAdminPassword|String|  
|NewVirtualNetworkAdapterInput|PSObject|  
|LinuxAdministratorSSHKey|String|  
|LinuxDomainName|String|  

## Parameters for a new service  
The following table lists the parameters available when a new service is created. All parameters are optional unless indicated as required.  

|Parameter|Data Type|  
|-------------|-------------|  
|StampID \(required\)|Guid|  
|CloudID \(required\)|Guid|  
|ServiceTempateId|Guid|  
|NewServiceDeployment|PSObject|  
|IgnorePlacementErrors|Boolean|  

## See Also  
[How to Automate a Runbook from Service Provider Foundation](../Manage/How-to-Automate-a-Runbook.md)  
