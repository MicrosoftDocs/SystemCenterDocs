---
title: The Activity Library
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b92ccc7-868c-476d-8742-6bbf19ab60b3
 

















---
# The Activity Library
The Activity Library in System Center 2016 - Service Manager Authoring Tool provides a number of workflow activities for building basic Windows Workflow Foundation \(WF\) workflows. Each activity performs a discrete function, such as establishing a loop structure within the workflow, running a script, or creating a Service Manager incident. The Activity Library includes the following types of activities:  
  
-   **[DeleteActive Directory Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///45cd915d-cd2d-47fc-b01f-ef78749552bf).** Activities that perform Active&nbsp;Directory functions, such as adding users or computers to groups.  
  
-   **[Delete Control Flow Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7643bc64-8f70-4215-8cad-e2e7901cbfad).** Activities that provide structure for the workflow, such as loops and if\-else branches.  
  
-   **[DeleteVirtual Machine Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7b249a87-858f-4f80-9be8-17cfa4533aba).** Activities that you can use to build workflows that perform simple operations with virtual machines.  
  
-   **[DeleteScript Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///0814abca-00b9-42dd-bbca-0da5a6f69e18).** Activities that run Windows PowerShell, command\-line, or Microsoft Visual Basic Scripting Edition \(VBScript\) scripts.  
  
-   **[DeleteService Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///c338d0ef-503c-40ac-be6b-3b0a1a2edebf).** Activities that perform Service Manager functions, such as creating or updating incidents.  
  
 The following tables list the default activities that are available with the Authoring Tool:  
  
|Active Directory activity|Description|  
|-------------------------------|-----------------|  
|Add AD DS Computer To Group|Use this activity to add a computer to a security group in Active Directory Domain Services \(AD&nbsp;DS\).<br /><br /> When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD&nbsp;DS.|  
|Add AD DS User To Group|Use this activity to add a user to a security group in AD&nbsp;DS.<br /><br /> When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD&nbsp;DS.|  
  
|Control Flow activity|Description|  
|---------------------------|-----------------|  
|Delay|Use this activity to introduce a delay between activities in a workflow.|  
|For Each Loop|Use this activity to repeat a certain set of activities for a defined number of iterations.|  
|IfElse|Use this activity to control the sequence of activities within a workflow based on a Boolean \(True\/False\) condition. You can use the outcome of a previous activity \(such as a script activity\) for the condition.|  
|Parallel|Use this activity to fork the sequence of activities into two simultaneous sequences of activities.|  
  
|Virtual Machine Management activity|Description|  
|-----------------------------------------|-----------------|  
|Get VM|Use this activity to retrieve a list of one or more virtual machine IDs from a System Center Virtual Machine Manager \(VMM\) Library.|  
|Move VM|Use this activity to move a virtual machine from the VMM library to a maintenance host.|  
|Shutdown VM|Use this activity to shut down the guest operating system on a virtual machine.|  
|Start VM|Use this activity to start a stopped or paused virtual machine.|  
|Save State VM|Use this activity to save the state of a virtual machine, and then stop the virtual machine.|  
  
|Script activity|Description|  
|---------------------|-----------------|  
|Command Script|Use this activity to run a command\-line script as part of a WF workflow.|  
|VBScript Script|Use this activity to run a VBScript script as part of a WF workflow.|  
|Windows PowerShell Script|Use this activity to run a Windows PowerShell script as part of a WF workflow.|  
  
|Service Manager activity|Description|  
|------------------------------|-----------------|  
|Create Incident|Use this activity to create and populate a Service Manager incident.|  
|Get Incident|Use this activity to retrieve one or more Service Manager incidents.|  
|Update Incident|Use this activity to save property changes to one Service Manager incident.|  
|Set Activity Status To Completed|Use this activity to update the status of a Service Manager automated activity.|  
  
## See Also  
 [Configuring the Way Activities Manage and Pass Information](../../../sm/manage/author/Configuring-the-Way-Activities-Manage-and-Pass-Information.md)   
 [How to Add an Activity to a Workflow](../../../sm/manage/author/How-to-Add-an-Activity-to-a-Workflow.md)   
 [How to Remove an Activity from a Workflow](../../../sm/manage/author/How-to-Remove-an-Activity-from-a-Workflow.md)   
 [Configuring the Activities Toolbox](../../../sm/manage/author/Configuring-the-Activities-Toolbox.md)   
 [Automating IT Processes with Workflows](../../../sm/manage/author/Automating-IT-Processes-with-Workflows.md)
