---
title: Parameters for Runbooks Invoked from Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c3c412d-34be-4311-8d8a-1f74f2bfba8f
---
# Parameters for Runbooks Invoked from Service Provider Foundation
This topic describes the parameters that [!INCLUDE[spflong](../Token/spflong_md.md)] automatically provides to a runbook that it invokes in [!INCLUDE[orchlong](../Token/orchlong_md.md)], as described in [How to Automate a Runbook from Service Provider Foundation](../Topic/How-to-Automate-a-Runbook-from-Service-Provider-Foundation.md). A runbook is not required to process all the parameters it receives, and will simply ignore the parameters which have no purpose in the runbook.

## Parameters for a new virtual machine
The following table lists the parameters available when a new virtual machine is created. All parameters are optional unless indicated as required.

|Parameter|Data Type|
|-------------|-------------|
|StampId \(required\)|Guid|
|Name \(StampID name – required\)|String|
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
[How to Automate a Runbook from Service Provider Foundation](../Topic/How-to-Automate-a-Runbook-from-Service-Provider-Foundation.md)
[Extensibility in Service Provider Foundation](../Topic/Extensibility-in-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)

