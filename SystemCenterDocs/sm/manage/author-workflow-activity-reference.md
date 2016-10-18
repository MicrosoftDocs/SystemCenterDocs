---
title: Workflow Activity Reference
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08966e4d-19ef-47d8-a415-776409b51a32
---

# Workflow Activity Reference

>Applies To: System Center 2016 - Service Manager

This section provides guidance for information technology (IT) developers so that they can create custom Windows Workflow Foundation (WF) activities that IT pros can use to build WF workflows that are specific to their IT processes. Custom WF activities extend the Activity Library-the activities that are distributed with the Service Manager Authoring Tool. The Workflow Activity Reference section of this document provides details of the default WF activities in the Activity Library. This information is intended to help developers (or IT pros acting as developers) create custom WF activities, as needed.  

 For information about how to use WF activities and WF workflows with Service Manager, see [Automating IT Processes with Workflows](author-automating-it-processes-with-workflows.md).  

## Active Directory Activities

Use Active Directory Domain Services (AD&nbsp;DS) activities to make Active&nbsp;Directory functions part of your workflow in Service Manager.  

 The Service Manager Authoring Tool provides two default Service Manager activities in the **Active Directory Activities** group in the **Activities Toolbox** pane. The topics in this section describe these activities.  

### Add AD DS Computer to a Group Activity

This activity adds a computer to a security group in Active Directory Domain Services (AD&nbsp;DS) in Service Manager. The computer and the group must belong to the same domain, and all containers in the domain are searched.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD&nbsp;DS.  

#### Properties  
 The **Add AD DS Computer to Group** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Computer Domain|ComputerDomain|String|Yes|The fully qualified DNS domain name where the computer is located (for example, contoso.com)|  
|Computer Name|FullyQualifiedComputerName|String|Yes|The name of the computer.|  
|Group Name|FullyQualifiedGroupName|String|Yes|The name of the Active Directory Domain Services group.|  

 The **Add AD DS Computer to Group** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Description|  
|------------------|-------------------|----------|-----------------|  
|Output|Output|Boolean|The result of the operation: **True** if the addition succeeded, **False** if it failed.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 None.  

#### Example  
 None.  

### Add AD DS User to Group Activity

This activity adds a user to a security group in Active Directory Domain Services (AD&nbsp;DS) in Service Manager. The user and the group must belong to the same domain, and all the containers in the domain are searched.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD&nbsp;DS.  

#### Properties  
 The **Add AD DS User to Group** activity uses the input properties that are listed in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|User Domain|UserDomain|String|Yes|The fully qualified domain name (FQDN) of the user.|  
|User Name|UserName|String|Yes|The logon name of the user.|  
|Group Name|FullyQualifiedGroupName|String|Yes|The FQDN of the group.|  

 The **Add AD DS User to Group** activity generates the output that is described in the following table.  

|Display Name|Internal Name|Type|Description|  
|------------------|-------------------|----------|-----------------|  
|Output|Output|Boolean|The result of the operation: **True** if the addition succeeded, **False** if it failed.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 None.  

#### Example  
 None.  

## Control Flow Activities

Use control flow activities to provide structure-branches, loops, or timer delays-for your workflow in Service Manager.  

 The Authoring Tool provides four default control flow activities in the **Control Flow** group in the **Activities Toolbox** pane.  

### Delay Activity
This activity introduces a delay between activities in a workflow in Service Manager. The **Delay** activity is derived from the Microsoft .NET&nbsp;Framework **DelayActivity** class.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 None.  

#### Properties  
 The **Delay** activity uses the input properties that are listed in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Initialize TimeoutDuration|InitializeTimeoutDuration||Internal|Specifies a handler to initialize the **TimeoutDuration** property.|  
|TimeoutDuration|TimeoutDuration|Timespan|Yes|Duration of the delay.|  

 The **Delay** activity does not produce an output property.  

#### Errors and Exceptions  
 None.  

#### Remarks  
 For more information about this activity, see [DelayActivity Class](http://go.microsoft.com/fwlink/p/?LinkID=186252) in the .NET&nbsp;Framework Class Library.  

#### Example  
 None.  

### For Each Loop Activity
The **For Each Loop** activity takes as an input an array (*collection*) of objects and repeats the set of activities within the loop for each object in the collection. For example, if the input collection has five objects, the loop iterates five times. If the collection is empty, the loop does not iterate. There is no upper limit to the number of objects in the collection. The **For Each Loop** activity always runs on the computer on which the workflow runs.  

 The **For Each Loop** activity is a composite activity with two containers for activities:  

-   **Input Container**: This activity sets up the loop and defines the input collection. You can use the **Get Incident** or the **Get Virtual Machine** activity in this role.  

-   **Loop Container**: Named **ForEachChildActivity**, this activity contains the loop activities. Most Windows Workflow Foundation (WF) activities that you place in this container have two additional properties: **Current Item** and **Property to Bind**. For each activity within the loop container, set these properties as follows:  

    1.  Set **Current Item** to the **Current Item** property of the **Loop Container** activity of the **ForEach** activity. Note that if this activity is the first activity in the **For Each Loop** activity, **Current Item** is set automatically.  

    2.  Set the value of the **Property to Bind** property to the value of the property of the current activity that uses the **Current Item** value.  

     Two types of activities do not get the **Current Item** and **Property to Bind** properties and therefore cannot use the objects in the input collection:  

    -   Script activities, such as the **Windows PowerShell Script** activity.  

    -   Custom activities or other activities that do not inherit from the **WorkflowActivityBase** class. Such activities include those activities that are based on the **Activity** base class, such as native Visual Studio activities.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 None.  

#### Properties  
 The **For Each Loop** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Input Collection|InputCollection|Array/Object|N/A|A collection of objects to be passed, one at a time, to the activities within the **For Each Loop** activity. If the activity that resides in the input container produces an array of objects as its output property, **Input Collection** is automatically set to that property. To view the current value of this property, right-click the loop container, and then click **Properties**.|  
|Current Item|CurrentItem|Object|N/A|An index into **Input Collection** that activities within the loop can use as an input property. For the first activity in the loop container, this property is set automatically.|  

#### Errors and Exceptions  
 The **For Each Loop** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions under the following conditions:  

-   If any error occurs in the **ForEachLoop** activity and that is not with the child activities, the workflow terminates.  

-   If any error occurs within the child activities, the workflow terminates unless **ContinueOnError**=true.  

-   If any of the input properties are null. The activity does not iterate.  

 Each activity within the **For Each Loop** activity must write its own errors or exceptions to the custom tracking service. The **For Each Loop** activity does not do so itself.  

#### Remarks  
 None.  

#### Example  
 None.  

### IfElse Activity

This activity controls the sequence of activities within a workflow based on a Boolean (True/False) condition. You can use the outcome of a previous activity, such as a script activity, for the condition.  

 The **IfElse** activity is a Visual Studio activity that uses rules and conditions. For more information about using rules and conditions in Windows Workflow Foundation (WF), see [Tutorial: Use Rules and Conditions in WF](http://go.microsoft.com/fwlink/p/?LinkID=186257) in the MSDN Library.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 None.  

#### Properties  
 None.  

#### Errors and Exceptions  
 None.  

#### Remarks  
 For more information about the **IfElse** activity, see [IfElseActivity Class](http://go.microsoft.com/fwlink/p/?LinkID=164775) in the .NET&nbsp;Framework&nbsp;4 Class Library.  

#### Example  
 None.  

### Parallel Activity

This activity forks the sequence of activities into two simultaneous sequences of activities. The **Parallel** activity is a Visual Studio activity. For more information about the **ParallelActivity** class, see [ParallelActivity Class](http://go.microsoft.com/fwlink/p/?LinkID=186258) in the .NET&nbsp;Framework Class Library.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 None.  

#### Properties  
 None.  

#### Errors and Exceptions  
 None.  

#### Remarks  
 None.  

#### Example  
 None.  


## Virtual Machine Manager Activities

Use virtual machine management activities in Service Manager to build workflows that allow for creating and updating virtual machines. The virtual machine management activities support System Center Virtual Machine Manager.  

 The Service Manager Authoring Tool provides the following five default virtual machine management activities in the **VMM Activities** group in the **Activities Toolbox** pane.  


### Get VM Activity

This activity in Service Manager retrieves a list of one or more virtual machine IDs from a Virtual Machine Manager (VMM) Library.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  

-   The Virtual Machine Manager console and Service Manager must both be installed on the same server.  

-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active&nbsp;Directory Domain Services (AD&nbsp;DS).  

#### Properties  
 The **Get VM** activity uses the input properties in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Parameter Set|ParameterSet|String|No; the default is **Connection**.|Specifies a subset of parameters, organized for a particular purpose. For the **Get VM** activity, you can select one of the following parameter sets:<br /><br /> -   **All:** Search for all of the available virtual machines.<br />-   **ID:** Search for a virtual machine with a known ID.<br />-   **Connection:** Search for virtual machines that are connected to the Virtual Machine Manager (VMM) server that is designated by the **VMMServer** property.<br />-   **VMHostGroup:** Search for virtual machines that are connected to the virtual machine host that is designated by the **VM Host** property.|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies if the activity has an error set. (Read-only)|  
|All|All|Boolean|No. (The default setting is True.)|Available if the **Parameter Set** is **All**. If it is set to **True**, the **Get VM** activity returns a list of the virtual machine IDs of all of the available virtual machines.|  
|ID|ID|String|Required if **Parameter Set** is **ID**.|Available if the **Parameter Set** is **ID**. If it is set to **True**, the **Get VM** activity returns a list of the virtual machine IDs of all of the virtual machines whose virtual machine IDs match all or part of the specified ID value.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. (Read-only)|  
|Script Server|Target|String|Yes|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM Host|VMHost|String|Required if the **Parameter Set** is **VMHostGroup**|Available if the **Parameter Set** is **VMHostGroup**. If this parameter set is selected, the **Get VM** activity returns a list of the virtual machine IDs of all of the virtual machines running on the specified host.|  
|VM Name|VMName|String|No|Specifies the name or part of a name of the virtual machine to search for. If the string is part of a name, the activity retrieves the IDs of all virtual machines that contain the string.|  
|VMMServer|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager (VMM) server that manages the virtual machines.|  

 The **Get VM** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM IDs|VMIDList|Array of strings|Specifies the list of the IDs of virtual machines with names that match all or part of the **VM Name** string.|  

#### Errors and Exceptions  
 The **Get VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  

### Move VM Activity

This activity in Service Manager moves a virtual machine from the Virtual Machine Manager (VMM) Library to a maintenance host.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  

-   The Virtual Machine Manager console and Service Manager must both be installed on the same server.  

-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active&nbsp;Directory Domain Services (AD&nbsp;DS).  

#### Properties  
 The **Move VM** activity uses the input properties in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Block LM If Host Busy|BlockLMIfHostBusy|Boolean|No. (The default setting is False.)|Blocks retrying a Hyper-V live migration if the migration failed because the source host or the destination host is already participating in another live migration.|  
|Job Group|JobGroup|Guid (string)|No|Specifies an identifier for a series of commands that will run as a set.|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. (Read-only)|  
|Path|Path|String|No|Specifies the destination of the virtual machine on the maintenance host.|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization (PRO) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. (The default setting is False.)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the activity to run.|  
|Start VM On Target|StartVMOnTarget|Boolean|No. (The default setting is False.)|Specifies that a virtual machine starts as soon as it reaches its destination host.|  
|Use Cluster|UseCluster|Boolean|No. (The default setting is False.)|Forces the use of Windows Server 2008 Cluster Migration for the transfer of a virtual machine that is in a saved state to a host, even if the cluster supports Hyper-V live migration.|  
|Use LAN|UseLan|Boolean|No. (The default setting is False.)|Forces a transfer over the local area network (LAN) even if a faster transfer mechanism, such as a storage area network (SAN) transfer, is available.|  
|VM Host|VMHostName|String|Yes|Specifies the name of the maintenance host to which the virtual machine will be moved.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be moved.|  
|VMM Server|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager (VMM) server that manages the virtual machines.|  

 The **Move VM** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was moved. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  

#### Errors and Exceptions  
 The **Move VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  

### Shutdown VM Activity

This activity in Service Manager shuts down the guest operating system on a virtual machine.  

 You can use the **Shutdown VM** activity on a virtual machine on a Windows-based host (a Hyper-V host or a Virtual Server host) only if virtualization guest services are installed on the virtual machine. For a virtual machine that is deployed on a Hyper-V host, the virtualization guest service is called Integration Components. For a virtual machine that is deployed on a Virtual Server host, the virtualization guest service is called Virtual Machine Additions.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  

-   The Virtual Machine Manager console and Service Manager must both be installed on the same server.  

-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active&nbsp;Directory Domain Services (AD&nbsp;DS).  

#### Properties  
 The **Shutdown VM** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable that is named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. (Read-only)|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization (PRO) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. (The default setting is False.)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **Localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be shut down.|  
|VMMServer|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager (VMM) server that manages the virtual machines.|  

 The **Shutdown VM** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was shut down. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  

#### Errors and Exceptions  
 The **Shutdown VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  

### Start VM Activity

This activity in Service Manager starts a stopped or paused virtual machine.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  
 None.  

#### Properties  
 The **Start VM** activity uses the input properties in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable that is named by this parameter.|  
|Management Group|ManagementGroup|String|No|The management group in which this activity will run. Set to **localhost**. (Read-only)|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization (PRO) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. (The default setting is False.)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be started.|  
|VMMServer|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager (VMM) server that manages the virtual machines.|  

 The **Start VM** activity generates the output that is described in the following table.  

|Display Name|Internal Name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was started. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  

#### Errors and Exceptions  
 The **Start VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  

### Save State VM Activity

This activity in Service Manager saves the state of a virtual machine and then stops the virtual machine.  

#### Design Time Prerequisites  
 None.  

#### Run Time Prerequisites  

-   The Virtual Machine Manager console and Service Manager must be both installed on the same server.  

-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active&nbsp;Directory Domain Services (AD&nbsp;DS).  

#### Properties  
 The **Save State VM** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable that is named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. (Read-only)|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization (PRO) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. (The default setting is False.)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be saved.|  
|VMM Server|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager (VMM) server that manages the virtual machines.|  

 The **Save State VM** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was saved. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  

#### Errors and Exceptions  
 The **Save State VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  


## Script Activities

Use a script activity in Service Manager to run a script as part of a workflow.  

 Script activities run as a separate process from the workflows; however, they also run under the security context of the Service Manager Workflow account.  

 The Service Manager Authoring Tool provides the following three default script activities in the **Generic Script Activities** subgroup of the **Script Activities** group in the **Activities Toolbox** pane.  

### Command Script Activity

This activity runs a command-line script as part of a Windows Workflow Foundation (WF) workflow.  

#### Design-Time Prerequisites  
 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **Command Script** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. By default, this is set to **localhost**. (Read-only)|  
|Script Parameters|Parameters|Dictionary <string,string>|Yes|Specifies command-line switches or switch/value pairs to be passed into the script when it runs.|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Script Server|Target|String|No|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the script to run.|  

#### Errors and Exceptions  
 The **Command Script** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  


### Windows PowerShell Script Activity

This activity in Service Manager runs a Windows PowerShell script as part of a Windows Workflow Foundation (WF) workflow.  

#### Design-Time Prerequisites  
 The **Windows PowerShell Script** activity depends upon the following prerequisites at design time:  

-   Windows PowerShell 2.0  

#### Run-Time Prerequisites  
 Windows PowerShell 2.0  

#### Properties  
 The **Windows PowerShell Script** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. By default, this is set to **localhost**. (Read-only)|  
|Script Parameters|Parameters|Dictionary <string,string>|Yes|Specifies the name/value list of parameters to be passed into the script when it runs.<br /><br /> You can set parameter values to any of the following management pack references:<br /><br /> -   $Target/...$<br />-   $MPElement[...]<br />-   $Data/...$. $Data references are resolved only at run time in the parameters (not in the script itself).<br /><br /> Using one of these references as the only value for a parameter sets that parameter to the XML string that represents the input data item (from **GetItemXML**).|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Snap-ins|SnapIns|String|No|Lists Windows PowerShell snap-ins to preload into the runspace.|  
|Script Server|Target|String|No|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the script to run.|  

#### Errors and Exceptions  
 The **Windows PowerShell Script** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 For more information about Windows PowerShell, see [Windows PowerShell](http://go.microsoft.com/fwlink/p/?LinkID=164777).  

### VBScript Script Activity

This activity in Service Manager runs a VBScript script as part of a Windows Workflow Foundation (WF) workflow.  

#### Design-Time Prerequisites  
 The **VBScript Script** activity depends on the following prerequisites at design time:  

 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **VBScript Script** activity uses the input properties that are described in the following table.  

|Display Name|Internal Name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is True.)|Determines whether the workflow continues to run if the activity fails.|  
|Has Error|HasError||N/A|Specifies whether the activity has an error set. (Read-only)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. (By default, this is set to **localhost**) (Read-only)|  
|Script Parameters|Parameters|Dictionary <string,string>|Yes|Provides the list of the standard switches and any associated values that this script uses when it runs.|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Script Server|Target|String|No|Specifies the Domain Name System (DNS) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. (The default setting is 300 seconds.)|Specifies the maximum number of seconds to allow for the script to run.|  

### Errors and Exceptions  
 The **VBScript Script** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  

#### Remarks  
 None.  

#### Example  
 None.  

## Service Manager Activities

Use Service Manager activities in Service Manager to make Service Manager functions part of your workflow.  

 The  Service Manager Authoring Tool provides the following four default Service Manager activities in the **SM Activities** group in the **Activities Toolbox** pane.  

### Create Incident Activity

This activity creates and populates an incident in Service Manager.  

#### Design-Time Prerequisites  
 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **Create Incident** activity uses the input properties that are listed in the following table.  

|Display name|Internal name|Type|Required|Comments|  
|------------------|-------------------|----------|--------------|--------------|  
|Incident ID|IncidentID|String|Yes|Specifies the unique identifier who is generated for the **Incident** object.|  
|Action Log Comment|ActionLogComment|String|Yes|Specifies the comment to include in the **Incident** object's action log.|  
|Affected User Domain|AffectedUserDomain|String|Yes|Specifies the name of the Domain Name System (DNS) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|Yes|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|Yes|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. (Category -**enum** data field)|  
|Continue On  Error|ContinueOnError|Boolean|No. (The default setting is true.)|Determines whether the workflow should continue running if the activity fails.|  
|Impact|Impact|Integer|Yes|Specifies the impact of the incident on the affected user or users. The value is the ID of **enum**. (Impact -**enum** data type)|  
|Source|Source|Integer|No|Specifies the source of information about the incident, such as "Phone" or "E-mail". The value is the ID of **enum**. (Source -**enum** data type field)|  
|Summary|Summary|String|Yes|Specifies the summary text that describes the incident.|  
|Urgency|Urgency|Integer|Yes|Specifies the urgency of resolving the incident. The value is the ID of **enum**. (Urgency -**enum** data type field)|  

 The **Create Incident** activity generates the output that is described in the following table.  

|Name|Type|Comments|  
|----------|----------|--------------|  
|SM Incident|System.WorkItem.Incident|Returns the constructed incident class instance.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 None.  

#### Example  
 None.  

### Get Incident Activity

This activity retrieves one or more incidents in Service Manager.  

#### Design-Time Prerequisites  
 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **Get Incident** activity uses the input properties that are listed in the following table.  

|Display name|Internal name|Type|Required|Comments|  
|------------------|-------------------|----------|--------------|--------------|  
|Affected User Domain|AffectedUserDomain|String|No|Specifies the name of the Domain Name System (DNS) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|No|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|No|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. (Category -**enum** data field)|  
|Continue On Error|ContinueOnError|Boolean|No. (The default is true.)|Determines whether the workflow should continue running if the activity fails.|  
|Incident ID|IncidentID|String|No|Specifies the unique identifier that is generated for the incident object.|  
|Search Type|SearchType|Integer?|No|Specifies the title of the search type that is used with the activity.|  
|Status|Status|Integer|No|Specifies the status of incident. The value is the ID of **enum**. (Status -**enum** data field)|  
|Summary Text|SummaryText|String|No|Specifies the summary text that describes the incident.|  

 The **Get Incident** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|SM Incidents|SMIncidents|Array of System.Workitem.Incident|Specifies an array of incident objects.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 The **Get Incident** activity has its own validator to perform error validation on input properties.  

#### Example  
 None.  

### Update Incident Activity

This activity in Service Manager saves property changes to one Service Manager incident.  

#### Design-Time Prerequisites  
 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **Update Incident** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Action Log Comment|ActionLogComment|String|No|Specifies a comment to include in the Incident object's action log.|  
|Affected User Domain|AffectedUserDomain|String|No|Specifies the name of the Domain Name System (DNS) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|No|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|No|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. (Category -**enum** data type)|  
|Continue On Error|ContinueOnError|Boolean|No. (The default setting is true.)|Determines whether the workflow should continue running if the activity fails.|  
|Impact|Impact|Integer|No|Specifies the impact of the incident on the affected user or users. The value is the ID of **enum**. (Impact -**enum** data type)|  
|Source|Source|Integer|No|Specifies the source of information about the incident, such as "Phone" or "E-mail." The value is the ID of **enum**. (Source -**enum** data type)|  
|Service Manager Incident|SMIncident|System.Workitem.Incident|No|The constructed incident class instance to be updated.|  
|Status|Status|Integer|No|Specifies the status of the incident that generated the activity. The value is the ID of **enum**. (Status -**enum** data type)|  
|Summary|Summary|String|No|Specifies the summary text that describes the incident.|  
|Urgency|Urgency|Integer|No|Specifies the urgency of resolving the incident. The value is the ID of **enum**. (Urgency -**enum** data type field)|  

 The **Update Incident** activity generates the output that is described in the following table.  

|Display name|Internal name|Type|Description|  
|------------------|-------------------|----------|-----------------|  
|SM Incident|SMIncident|System.WorkItem.Incident|Returns an update of the incident class instance. The input **SM Incident** and the output **SM Incident**are equal unless the activity failed to find the **SM Incident**. In that case, the output **SM Incident** is set to Null.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 None.  

#### Example  
 None.  

### Set Activity Status to Completed Activity

This activity updates the status of an automated activity in Service Manager.  

#### Design-Time Prerequisites  
 None.  

#### Run-Time Prerequisites  
 None.  

#### Properties  
 The **Set Activity Status to Completed** activity uses the input properties that are described in the following table.  

|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Activity ID|ActivityID|String|Yes|Specifies the identifier of a Service Manager automated activity object.|  

#### Errors and Exceptions  
 None.  

#### Remarks  
 When you are using this activity in a workflow that is triggered by a Service Manager automated activity, enter **$Data/BaseManagedEntityId$** as the value of this property. This value applies to the **Set Activity Status to Completed** activity at the automated activity that triggered the workflow to run.  

#### Example  
 None.  
