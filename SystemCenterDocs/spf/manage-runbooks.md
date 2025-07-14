---
title: Automate and invoke runbooks from SPF
description: Provides information about integrating System Center SPF and SMA.
author: jyothisuri
ms.author: jsuri
ms.date: 08/07/2023
ms.topic: how-to
ms.service: system-center
ms.subservice: service-provider-foundation
ms.custom: UpdateFrequency2, engagement-fy24
---

# Automate and invoke runbooks from SPF



You can use System Center - Service Provider Foundation (SPF) and Service Management Automation (SMA) together to provide automated solutions for your tenants. You can configure events in SPF that the SMA web service uses.

## Automate runbooks

You can automate runbooks using SMA, if you've configured SMA to use SPF, using the `Set\-SCSPFEventRegisration and Get\-SCSPFEventRegistation` cmdlets. This is shown in the following example:  

```powershell  
PS C:\> # This command sets a runbook to be invoked when the Create event for a new virtual machine is raised.  
PS C:\> Set-SCSPFEventRegistration -ResourceName "VMM.VirtualMachine" - ActionName "Create" -RunbookName "Invoke-SampleCmdlet"  
PS C:\>   
PS C:\> # This command gets an event with the Action parameter and stores it in the $event_backup variable.  
PS C:\> $event_backup = Get-SCSPFEventRegistration -Action "Backup"  

```  

## Invoke runbooks

You can set a runbook in System Center - Orchestrator to run whenever a new VM or service is created by remote calls to SPF with System Center - Virtual Machine Manager (VMM).

- You can set the runbook to be invoked using the Windows PowerShell `T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler` cmdlet.
- SPF raises internal events to invoke the runbook. The runbook is continuously invoked if the extensible event handler is enabled.
- SPF won't invoke the runbook if the VM or service was created by other means. For example, using Windows PowerShell cmdlets or by using the VMM console.
- To support the infrastructure for invoking a runbook, SPF calls the `Start-SCOrchestratorRunbook` cmdlet internally. It doesn't need to be explicitly called by the user.
- Ensure that you've applied the following before you call the `T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler` cmdlet:
    - The URL of the Orchestrator web service.
    - The identity settings for the SPF application pools in **Internet Information Services \(IIS\) Manager** must be included in the Orchestrator Users Group.  

Then, invoke a runbook as follows:

1. Call the `T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler` with the following parameters:  

    |Parameter|Value|  
    |-------------|---------|  
    |EventName|Specify either "VirtualMachineCreated" or "ServiceCreated".|  
    |OrchestratorUri|The URI to the Orchestrator web service.|  
    |RunbookPath|The local path to the runbook.|  
    |Enable|Specify to enable the runbook.<br /><br />To disable the runbook from being invoked, omit this parameter.|  

    Example:  

    ```  
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "http://east.contoso.com:82/Orchestrator2016/Orchestrator.svc" -RunbookPath "\SPF Runbooks\Extensibility\VM Created" -Enable  
    ```  

2. To determine the setting for the extensible event handler, call the `T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler` cmdlet.  
3. To disable a runbook from being invoked, repeat the `T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler` command, but without the **Enable** parameter. You can also specify empty strings for the **OrchestratorUrl** and **Runbookpath** parameters as shown in the following example:  

    ```  
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "" -RunbookPath ""  
    ```  
## Runbook parameters

This list of parameters is automatically provided to the runbook. A runbook doesn't need to process all the parameters it receives. It ignores parameters that have no purpose in the runbook.  

### Parameters for a new VM  

The following table lists the parameters available when a new VM is created. All the parameters are optional unless indicated.  

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

### Parameters for a new service  
The following table lists the parameters available when a new service is created. All the parameters are optional unless indicated.  

|Parameter|Data Type|  
|-------------|-------------|  
|StampID \(required\)|Guid|  
|CloudID \(required\)|Guid|  
|ServiceTempateId|Guid|  
|NewServiceDeployment|PSObject|  
|IgnorePlacementErrors|Boolean|  
