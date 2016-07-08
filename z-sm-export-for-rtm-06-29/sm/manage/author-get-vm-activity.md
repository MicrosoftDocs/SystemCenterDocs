---
title: Get VM Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be67b2b9-8490-408d-8965-d7f1f7629349


















---
# Get VM Activity
This activity in System Center 2012 - Service Manager retrieves a list of one or more virtual machine IDs from a System Center Virtual Machine Manager \(VMM\) Library.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
  
-   The Virtual Machine Manager console and Service Manager must both be installed on the same server.  
  
-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active Directory Domain Services \(AD DS\).  
  
## Properties  
 The **Get VM** activity uses the input properties in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Parameter Set|ParameterSet|String|No; the default is **Connection**.|Specifies a subset of parameters, organized for a particular purpose. For the **Get VM** activity, you can select one of the following parameter sets:<br /><br /> -   **All:** Search for all of the available virtual machines.<br />-   **ID:** Search for a virtual machine with a known ID.<br />-   **Connection:** Search for virtual machines that are connected to the Virtual Machine Manager \(VMM\) server that is designated by the **VMMServer** property.<br />-   **VMHostGroup:** Search for virtual machines that are connected to the virtual machine host that is designated by the **VM Host** property.|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies if the activity has an error set. \(Read\-only\)|  
|All|All|Boolean|No. \(The default setting is True.\)|Available if the **Parameter Set** is **All**. If it is set to **True**, the **Get VM** activity returns a list of the virtual machine IDs of all of the available virtual machines.|  
|ID|ID|String|Required if **Parameter Set** is **ID**.|Available if the **Parameter Set** is **ID**. If it is set to **True**, the **Get VM** activity returns a list of the virtual machine IDs of all of the virtual machines whose virtual machine IDs match all or part of the specified ID value.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. \(Read\-only\)|  
|Script Server|Target|String|Yes|Specifies the Domain Name System \(DNS\) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM Host|VMHost|String|Required if the **Parameter Set** is **VMHostGroup**|Available if the **Parameter Set** is **VMHostGroup**. If this parameter set is selected, the **Get VM** activity returns a list of the virtual machine IDs of all of the virtual machines running on the specified host.|  
|VM Name|VMName|String|No|Specifies the name or part of a name of the virtual machine to search for. If the string is part of a name, the activity retrieves the IDs of all virtual machines that contain the string.|  
|VMMServer|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager \(VMM\) server that manages the virtual machines.|  
  
 The **Get VM** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM IDs|VMIDList|Array of strings|Specifies the list of the IDs of virtual machines with names that match all or part of the **VM Name** string.|  
  
## Errors and Exceptions  
 The **Get VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## See Also  
 [DeleteVirtual Machine Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7b249a87-858f-4f80-9be8-17cfa4533aba)
