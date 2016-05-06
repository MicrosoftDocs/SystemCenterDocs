---
title: Service Management Automation sample runbooks
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3b33c07-efe9-43de-9a31-fad1123dd7f9
---
# Service Management Automation sample runbooks
The following runbooks ship with [!INCLUDE[sma_1](./Token/sma_1_md.md)] as sample runbooks to illustrate techniques and best practices. They are available to be used in the [!INCLUDE[sma_2](./Token/sma_2_md.md)] extension in [!INCLUDE[katal_1](./Token/katal_1_md.md)].

## Sample runbooks

|Runbook name|Description|
|----------------|---------------|
|Sample\-Deleting\-VMCloud\-Subscription|Demonstrates a useful scenario for triggering a runbook when a user deletes a VM Clouds subscription.|
|Sample\-Managing\-Azure|Shows how to connect to a Windows Azure subscription and perform basic operations using the Windows Azure PowerShell module.|
|Sample\-Managing\-ConfigurationManager|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)] to connect into System Center Configuration Manager.|
|Sample\-Managing\-DataProtectionManager|Demonstrates how to connect to a Data Protection Manager \(DPM\) server and view information about the disks found on the DPM server.|
|Sample\-Managing\-MySQLServers|Demonstrates how to retrieve a security token which will be used to then retrieve a list of host servers.|
|Sample\-Managing\-OperationsManager|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)]to connect to System Center Operations Manager.|
|Sample\-Managing\-Orchestrator|Shows how to connect to System Center Orchestrator and start an Orchestrator runbook to leverage your existing infrastructure.|
|Sample\-Managing\-Plans|Demonstrates how to create a new plan and add the SQL Server service with a defined quota to the new plan.|
|Sample\-Managing\-ServiceBusClouds|Demonstrates how to connect to a Service Bus Cloud server and view information about the created namespaces.|
|Sample\-Managing\-SQLServers|Demonstrates how create a new server group and add a SQL hosting server.|
|Sample\-Managing\-UserAccounts|Demonstrates how to create a User in [!INCLUDE[katal_1](./Token/katal_1_md.md)], which will be created in [!INCLUDE[katal_2](./Token/katal_2_md.md)], and appear in the [!INCLUDE[katal_adminportal_1](./Token/katal_adminportal_1_md.md)] Users extension. However, this user should also be integrated into the authentication provider \(for example, AuthSite\) for accessing the [!INCLUDE[katal_tenantportal_1](./Token/katal_tenantportal_1_md.md)], which is not included in this sample.|
|Sample\-Managing\-VirtualMachineManager|Demonstrates how to connect to a Virtual Machine Manager \(VMM\) server and view information about the VMM server license.|
|Sample\-Managing\-VMClouds|Demonstrates how to access information about a Service Provider Foundation server's database connection and information about the VMM server objects managed by Service Provider Foundation.|
|Sample\-Managing\-WebSiteCloud|Demonstrates how to connect to a Web Site Clouds controller server and view information about the Web Site Clouds deployed servers.|
|Sample\-Modify\-VMCloud\-Subscription|Demonstrates a useful scenario for triggering a runbook when tenant or administrator suspends or activates a VM Clouds subscription.|
|Sample\-Using\-Activities|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)] to use activities|
|Sample\-Using\-Checkpoints|Demonstrates the capability to use checkpoints in [!INCLUDE[sma_1](./Token/sma_1_md.md)].|
|Sample\-Using\-Connections|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)] to use connections to connect into remote systems.|
|Sample\-Using\-Credentials|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)] to use credentials, and outputs the user who the [!INCLUDE[sma_1](./Token/sma_1_md.md)] runbook is running as. Then, it connects to the server 'ServerName' and outputs the user specified by 'SampleCredential' who is accessing the server.|
|Sample\-Using\-Modules|Demonstrates importing modules in runbooks, and outputs the number of already imported modules on the server 'ServerName'. Then, it imports the module specified by 'ModulePath' and outputs the new module count and information corresponding to the newly imported module.|
|Sample\-Using\-RunbookParameters|Demonstrates how to use input parameters for runbooks and also specify whether parameters are required, provide default parameter values, and use parameter values later in the workflow.|
|Sample\-Using\-Runbooks|Demonstrates how to call a runbook from within another runbook.|
|Sample\-Using\-SuspendWorkflow|Demonstrates how to force a runbook to suspend. This could be useful if a manual step is required before a runbook should continue, such as receiving sign\-off approval from a specific person. Once the manual step is completed, the suspended runbook would be resumed manually to continue the runbook.|
|Sample\-Using\-Variables|Demonstrates the capability of [!INCLUDE[sma_1](./Token/sma_1_md.md)] to use variables.|
|Sample\-Using\-VMCloud\-Automation|Demonstrates a useful scenario for triggering a runbook at the start of a Service Provider Foundation event.|


