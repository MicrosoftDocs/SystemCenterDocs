---
ms.assetid: 
title: Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)
description: This article describes the errors that might occur when you deploy or use Azure Monitor SCOM Managed Instance (preview) and how to resolve them.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/25/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)

This article describes the errors that might occur when you deploy or use Azure Monitor SCOM Managed Instance (preview) and how to resolve them.

## SCOM Managed Instance (preview) creation/deployment

### Issue: Resource group `%ResourceGroupName;` is managed by other Azure resource

**Cause**

Occurs when the *ManagedBy* property is set for this resource group.

**Resolution**

To resolve, provide another resource group with *ManagedBy* property as empty.

### Issue: The subnet `%SubnetName;` selected is dedicated to other service

**Cause**

Occurs when the subnet has delegations.

**Resolution**

To resolve, provide a subnet without any delegation.

### Issue: Error when SCOM Managed Instance (preview) is reaching SQL Managed Instance `%instance;`

**Cause**:	

This error can be caused by multiple reasons: 
   - SCOM Managed Instance might not have read permissions on the SQL Managed Instance or 
   - There might be an issue with your VNet/Region. 
For more information, see [Create and configure an SQL Managed Instance](/system-center/scom/create-operations-manager-managed-instance?tabs=prereqs-portal#create-and-configure-an-sql-mi-instance).

**Resolution**:	

To resolve, provide read permission to the SQL managed instance.

### Issue: No enough cores to create `%instance;` in the given region.

**Cause**

Occurs when there's no enough cores to create an instance in the given region.

**Resolution**

To resolve, allocate more cores in the region.

### Issue: Secret key with same name is already present in the Key vault

**Cause**

Occurs when the secret key with the same name is already present in the Key vault.

**Resolution**

To resolve, either change the name of the instance or select a different resource group.

### Issue: Error when you install SCOM. `%ErrorMessage;`

**Cause**

Check the error message and resolve the issue.

**Resolution**

Resolve issue and try again.

### Issue: VM has reported a failure when processing extension `joindomain` to join to the domain  `%DomainName;`

**Cause**

Occurs due to the following reasons:
1. Line-of-sight visibility from SCOM Managed Instance (preview) Server to Domain Controller.
2. Domain User Credentials.
3. OU Path for AD Domain.

**Resolution**

Resolve the issue and try again.

### Issue: Error when SCOM Server is reaching SQL Managed Instance endpoint `%endpoint;`

**Cause**

Occurs due to the following reasons:
1. Line-of-sight visibility from SCOM Managed Instance (preview) VNet to SQL Managed Instance (preview) endpoint or
2. Missing the right level of NSG rules to allow traffic over SQL Managed Instance public endpoint.

**Resolution**

Resolve the issue and try again.

### Issue: Static IP already in use

**Cause**

Occurs if static IP is used by another instance.

**Resolution**

To resolve, use another static IP.

### Issue: Invalid Identity Type `%identityType;`

**Cause**

Occurs due to invalid Managed identity.

**Resolution**

To resolve, provide one of the possible Identity types (`None`, `UserAssigned`, `SystemAssigned`, `SystemAssigned,UserAssigned`) and try again.

### Issue: Private static IP address `%LbIpAddr;` doesn't belong to the range of subnet `%subnet;`

**Cause**

Occurs as the IP address isn't in the subnet range

**Resolution**

To resolve, provide an available IP from the subnet range and retry the operation.

## Deploy Reports on Power BI 

### Issue: SQL Managed Instance isn't reachable

**Cause**

Occurs if the public endpoint isn't enabled. Power BI won't be able to reach SQL Managed Instance.

**Resolution**

To resolve, enable public endpoint on SQL Managed Instance.

### Issue: Unable to refresh dataset credentials

**Cause**

Occurs if the user doesn't have appropriate permissions on the SQL Managed Instance.

**Resolution**

To resolve, check the user permissions on SQL Managed Instance and provide the required permissions.

### Issue: Report unable to refresh

**Cause**

Occurs due to large data size. The report might not refresh.

**Resolution**

To resolve, if the Power BI workspace is in *pro* tier, change it to *premium* tier or change the capacity of the workspace.

## Manual Scale up/down 

### Issue: QUOTA Exceeded

**Cause**

Occurs if there are no cores available for scaling.

**Resolution**

To resolve, increase the number of cores in the subscription or delete existing VMs/Virtual Machine Scale Sets.

### Issue: Extension provisioning error

**Cause**

This error might occur during the provisioning of SCOM extension or SCOM installation.

**Resolution**

To resolve, contact Microsoft support.

### Issue: Conflict

**Cause**

Occurs if patching or scaling is in progress. A new operation can't be triggered.

**Resolution**

To resolve, wait for the ongoing process to complete and try again.

## Patch UI

### Issue: One or more controls on the patching blade aren't visible

**Cause** 

Development Issue.

**Resolution**
	
To resolve, contact Microsoft support.

### Issue: Notification is stuck at *Fetching updates* even though the update operation is complete

**Cause**

Network issue/development issue.

**Resolution**

To resolve, try refreshing for updates. If not resolved, contact Microsoft support.

### Issue: Update state isn't reflected correctly on the card

**Cause**

Network issue/development issue.

**Resolution**

To resolve, try refreshing for updates. If not resolved, contact Microsoft support.

### Issue: Inconsistency in the controls within the card

For example, the update button is enabled even though the title of the card reads **SCOM is up to date**.

**Cause**

Development issue.

**Resolution**

To resolve, contact Microsoft support.

### Issue: Warning message pops up for updates

**Cause**

Occurs due to the following reasons:
1. New update is available, and the user hasn't triggered the update instance
2. Last update failed and the user hasn't triggered another update instance

**Resolution**

To resolve, trigger an *update instance*.

### Issue: Update fails on more than one retries
	
**Resolution**

To resolve, contact Microsoft support.

### Issue: Update fails, and rollback fails leaving an inconsistent state where the number of VMs on the VMSS instance has been modified

**Resolution**

To resolve, contact Microsoft support.

### Issue: Update fails but database update is successful

**Cause**

Occurs due to failed update after the successful database update.

**Resolution**

To resolve, contact Microsoft support.

### Issue: After successful update, SCOM console isn't functioning properly on the instance

**Cause**

Occurs if SCOM isn't installed properly or some process might be stuck.

**Resolution**

To resolve, try to restart the instance. If the issue persists, contact Microsoft support.

### Issue: Update is taking more than 3 hours and fails eventually

**Cause**

Occurs when the update takes more than 3 hours.

**Resolution**

To resolve, contact Microsoft support.

### Issue: Some intermittent issue during update

**Cause**

Occurs if the service fabric or RP crashes or restarts.

**Resolution**

To resolve, restart the update.

### Issue: Scaling and Patching triggered simultaneously and then fails

**Cause**

Occurs if scaling and patching requests are sent and accepted at the same time.

**Resolution**

In case you've triggered a scaling operation, wait for the operation to complete before you try to update operation.

### Issue: Extension takes more time to update and fails

**Cause**

Occurs if SQL Managed Instance and SCOM Managed Instance (preview) are in different regions due to which the extension takes more time to update and eventually fails.

**Resolution**

To resolve, have SQL Managed Instance and SCOM Managed Instance (preview) in same region.

### Issue: After patching, user data in the database is altered or not retained properly

**Cause**

Occurs if update was not done properly.

**Resolution**

To resolve, restart the update.

### Issue: Patching request fails

**Cause**

Occurs due to portal or ARM issue.

**Resolution**

To resolve, wait for some time and retry. If the issue exists even after fixing the portal/ ARM issue, contact Microsoft support.


### Issue: Patching or scaling operation is already in progress, try again after some time.

**Cause**

Occurs if a patching or scaling operation is already in progress.

**Resolution**

To resolve, wait for the existing operation to complete and try after some time.