---
ms.assetid: b7528d59-28b7-4e98-988e-5fd29590fd6f
title: Automate and invoke runbooks from SPF
description: Provides information about integrating SPF and Service Management Automation to help tenants.
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/16/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
---

ms.assetid: 38695129-ee8d-49ee-a357-b00a7659ba31

# Automate and invoke runbooks from SPF
>Apples To: System Center 2016

You can use SPF and Service Management Automation together to provide automated solutions for your tenants.

- You can configure events in Service Provider Foundation that the Service Management Automation web service will use.
- You can use the older invoke runbook scenario that was included in System Center 2012.

## Automate runbooks

You can automate runbooks using Service Management Automation provided that you have configured the Service Management Automation to use SPF, by using the Set\-SCSPFEventRegisration and Get\-SCSPFEventRegistation cmdlets, as shown in the following example.  

```powershell  
PS C:\> # This command sets a runbook to be invoked when the Create event for a new virtual machine is raised.  
PS C:\> Set-SCSPFEventRegistration -ResourceName "VMM.VirtualMachine" - ActionName "Create" -RunbookName "Invoke-SampleCmdlet"  
PS C:\>   
PS C:\> # This command gets an event with the Action parameter and stores it in the $event_backup variable.  
PS C:\> $event_backup = Get-SCSPFEventRegistration -Action "Backup"  

```  

## Invoke runbooks (old scenario)


You can set a runbook in System Center 2016 or 2012 Orchestrator or System Center 2012 Orchestrator to be run whenever a new VM or service is created by remote calls to SPF with VMM.

- You can set the runbook to be invoked by using the Windows PowerShell T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler  cmdlet.
- SPF raises internal events to invoke the runbook and the runbook will continue to be invoked continuously as long as the extensible event handler is enabled.
- SPF won't invoke the runbook if the VM or service was created by other means, such as by using Windows PowerShell cmdlets, or by using the VMM console.
- To support the infrastructure for invoking a runbook, Service Provider Foundation calls the **Start-SCOrchestratorRunbook** cmdlet internally and it does to need to be explicitly called by the user.
- Make sure you have the following information and settings applied before you call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler cmdlet:
    - The URL to the Orchestrator web service.
    -   The identity settings for the Service Provider Foundation Application Pools in **Internet Information Services \(IIS\) Manager** must be included in the Orchestrator Users Group.  

Invoke a runbook as follows:

1. Call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler with following parameters:  

    |Parameter|Value|  
    |-------------|---------|  
    |EventName|Specify either "VirtualMachineCreated" or "ServiceCreated".|  
    |OrchestratorUri|The URI to the Orchestrator   web service.|  
    |RunbookPath|The local path to the runbook.|  
    |Enable|Specify to enable the runbook.<br /><br />To disable the runbook from being invoked, omit this parameter.|  

    Example:  

    ```  
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "http://east.contoso.com:82/Orchestrator2016/Orchestrator.svc" -RunbookPath "\SPF Runbooks\Extensibility\VM Created" -Enable  
    ```  

2. To determine what the extensible event handler is set to, call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler cmdlet.  
3. If you want to disable a runbook from being invoked, repeat the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler command, but without the *Enable* parameter. You can also specify empty strings for the *OrchestratorUri* and *Runbookpath* parameters as shown in the following example:  

    ```  
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "" -RunbookPath ""  
    ```  
## Runbook parameters

This list of parameters is automatically provided to the runbook. A runbook is not required to process all the parameters it receives, and will simply ignore the parameters which have no purpose in the runbook.  

### Parameters for a new virtual machine  

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

### Parameters for a new service  
The following table lists the parameters available when a new service is created. All parameters are optional unless indicated as required.  

|Parameter|Data Type|  
|-------------|-------------|  
|StampID \(required\)|Guid|  
|CloudID \(required\)|Guid|  
|ServiceTempateId|Guid|  
|NewServiceDeployment|PSObject|  
|IgnorePlacementErrors|Boolean|  
