---
title: How to Automate a Runbook from Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b47867e-a3b3-47dc-89b1-5ded85242d16
---
# How to Automate a Runbook from Service Provider Foundation
Starting with [!INCLUDE[spflong](../Token/spflong_md.md)][!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)] you can configure [!INCLUDE[sma_1](../Token/sma_1_md.md)] to use [!INCLUDE[spfshort](../Token/spfshort_md.md)]. For more information see the "Connect to the SMA web service" section of [Manage Web Services and Connections in Service Provider Foundation](../Topic/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md). You can also invoke runbooks with the older invoke runbook scenario.

You can automate runbooks using Service Management Automation provided that you have configured the [!INCLUDE[sma_1](../Token/sma_1_md.md)] to use [!INCLUDE[spfshort](../Token/spfshort_md.md)] by using the Set\-SCSPFEventRegisration and Get\-SCSPFEventRegistation cmdlets, as shown in the following example.

```powershell
PS C:\> # This command sets a runbook to be invoked when the Create event for a new virtual machine is raised.
PS C:\> Set-SCSPFEventRegistration –ResourceName "VMM.VirtualMachine" – ActionName "Create" –RunbookName "Invoke-SampleCmdlet"
PS C:\> 
PS C:\> # This command gets an event with the Action parameter and stores it in the $event_backup variable.
PS C:\> $event_backup = Get-SCSPFEventRegistration –Action "Backup"

```

The remainder of this topic describes the older scenario.

## Invoking runbooks \(not automation\)
You can set a runbook in [!INCLUDE[orchlong](../Token/orchlong_md.md)] to be run whenever a new virtual machine or new service is created by remote calls to [!INCLUDE[spflong](../Token/spflong_md.md)] with the [Virtual Machine Manager Service](http://go.microsoft.com/fwlink/?LinkId=298612). You can set the runbook to be invoked by using the Windows PowerShell T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler  cmdlet. [!INCLUDE[spfshort](../Token/spfshort_md.md)] raises internal events to invoke the runbook and the runbook will continue to be invoked continuously as long as the extensible event handler is enabled.

[!INCLUDE[spfshort](../Token/spfshort_md.md)] will not invoke the runbook if the virtual machine or service was created by other means such as by using Windows PowerShell cmdlets or by using the console in [!INCLUDE[vmm12long](../Token/vmm12long_md.md)].

To support the infrastructure for invoking a runbook, [!INCLUDE[spfshort](../Token/spfshort_md.md)] calls the **Start\-SCOrchestratorRunbook** cmdlet internally and it does to need to be explicitly called by the user.

Make sure you have the following information and settings applied before you call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler cmdlet:

-   The URI to the [!INCLUDE[orchshort](../Token/orchshort_md.md)] web service.

-   The identity settings for the [!INCLUDE[spfshort](../Token/spfshort_md.md)] Application Pools in **Internet Information Services \(IIS\) Manager** must be included in the Orchestrator Users Group. For information about determining the credentials that were applied for [!INCLUDE[spfshort](../Token/spfshort_md.md)], see the "Verify Local user credentials for portal access" section in [Verify local user credentials for portal access](../Topic/Configuring-Portals-for-Service-Provider-Foundation.md#LocalCreds). For information about adding credentials the Orchestrator Users Group, see [How to Change the Orchestrator Users Group](../Topic/How-to-Change-the-Orchestrator-Users-Group.md).

See [Parameters for Runbooks Invoked from Service Provider Foundation](../Topic/Parameters-for-Runbooks-Invoked-from-Service-Provider-Foundation.md) for a list of parameters that are automatically provided to the runbook.

#### To invoke a runbook from Service Provider Foundation

-   Call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFExtensibleEventHandler with following parameters:

    |Parameter|Value|
    |-------------|---------|
    |EventName|Specify either "VirtualMachineCreated" or "ServiceCreated".|
    |OrchestratorUri|The URI to the [!INCLUDE[orchshort](../Token/orchshort_md.md)] web service.|
    |RunbookPath|The local path to the runbook.|
    |Enable|Specify to enable the runbook.<br /><br />To disable the runbook from being invoked, omit this parameter.|

    Example:

    ```
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "http://east.contoso.com:82/Orchestrator2012/Orchestrator.svc" -RunbookPath "\SPF Runbooks\Extensibility\VM Created" -Enable
    ```

To determine what the extensible event handler is set to, call the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler cmdlet.

#### To disable a runbook from being invoked

-   Repeat the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFExtensibleEventHandler command but without the *Enable* parameter. You can also specify empty strings for the *OrchestratorUri* and *Runbookpath* parameters as shown in the following example:

    ```
    PS C:\> Set-SCSPFExtensibleEventHandler -EventName "VirtualMachineCreated" -OrchestratorUri "" -RunbookPath ""
    ```

## See Also
[Manage Web Services and Connections in Service Provider Foundation](../Topic/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md)
[Parameters for Runbooks Invoked from Service Provider Foundation](../Topic/Parameters-for-Runbooks-Invoked-from-Service-Provider-Foundation.md)
[Extensibility in Service Provider Foundation](../Topic/Extensibility-in-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)
[Cmdlets in System Center 2012 \- Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263677)
[How to Configure the Orchestrator Web Service to use HTTPS](assetId:///9f3f07f4-db1a-48e6-80c6-6085e7fed092)

