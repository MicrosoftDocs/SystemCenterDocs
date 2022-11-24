---
ms.assetid: 
title: Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)
description: This article describes the errors that might occur when you deploy or use Azure Monitor SCOM Managed Instance (preview) and how to resolve them.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/24/2022
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

This occurs when *ManagedBy* property is set for this resource group.

**Resolution**

To resolve this, provide another resource group with *ManagedBy* property as empty.

### Issue: The subnet `%SubnetName;` selected is dedicated to other service

**Cause**

This occurs when subnet has delegations.

**Resolution**

To resolve this, provide subnet without any delegation.

### Issue: Error when SCOM Managed Instance (preview) is reaching SQL MI `%instance;`

**Cause**:	

This error can be because of multiple reasons: 
   - SCOM Managed Instance might not have read permissions on the SQL MI or 
   - There might be an issue with your VNet/Region. 
For more information, see [Create and configure an SQL MI](/system-center/scom/create-operations-manager-managed-instance?tabs=prereqs-portal#create-and-configure-an-sql-mi-instance).

**Resolution**:	

To resolve this, provide read permission to the SQL managed instance.

### Issue: No enough cores to create `%instance;` in the given region.

**Cause**

This occurs as there is no enough cores to create instance in the given region.

**Resolution**

To resolve this, allocate more cores in the region.

### Issue: Secret key with same name is already present in the Key vault

**Cause**

This occurs as the secret key with same name is already present in the Key vault.

**Resolution**

To resolve this, either change the name of instance or select different resource group.

### Issue: Error when you install SCOM. `%ErrorMessage;`.

**Cause**: Check the error message and resolve the issue.
**Resolution**:	Resolve issue and try again.

### Issue: VM has reported a failure when processing extension `joindomain` to join to the domain  `%DomainName;`.

**Cause**

This occurs due to the following:
1. Line of sight visibility from SCOM Managed Instance (preview) Server to Domain Controller.
2. Domain User Credentials.
3. OU Path for AD Domain.

**Resolution**

Resolve the issue and try again.

### Issue: Error when SCOM Server is reaching SQL MI endpoint `%endpoint;`

**Cause**

This occurs due to the following:
1. Line of sight visbility from SCOM Managed Instance (preview) VNet to SQL Managed Instance (preview) endpoint or
2. Missing right level of NSG rules to allow traffic over SQL MI public endpoint.

**Resolution**

Resolve the issue and try again.

### Issue: Static IP already in use

**Cause**

This occurs if static IP is used by other instance.

**Resolution**

To resolve this, use another static IP.

### Issue: Invalid Identity Type `%identityType;`

**Cause**

This occurs due to invalid Managed identity.

**Resolution**

To resolve this, provide One of the Possbile Identity types (`None`, `UserAssigned`, `SystemAssigned`, `SystemAssigned,UserAssigned`) and try again.

### Issue: Private static IP address `%LbIpAddr;` doesn't belong to the range of subnet `%subnet;`

**Cause**

This occurs as the IP address is not in the subnet range

**Resolution**

To resolve this, provide an available IP from the subnet range and retry the operation.

## Deploy Reports on Power BI 

### Issue: SQLMI is not reachable

**Cause**

This occurs if the public endpoint isn't enabled. Power BI won't be able to reach SQL MI.

**Resolution**

To resolve this, enable public endpoint on SQL MI.

### Issue: Unable to refresh dataset credentials

**Cause**

This occurs if user doesn't have appropriate permissions on the SQL MI.

**Resolution**

To resolve this, check the user permissions on SQL MI and provide required permissions.

### Issue: Report unable to refresh

**Cause**

This occures due to large data size report might not refresh.

**Resolution**

To resolve this, if the Power BI workspace is in *pro* tier, change it to *premium* tier or change the capacity of the workspace.

## Manual Scale up/down 

### Issue: QUOTA Exceeded

**Cause**

This occurs if there are no cores available for scaling.

**Resolution**

To resolve this, increase the number of cores in subscription or delete existing VMs/VMSS.

### Issue: Extension provisioning error

**Cause**

This error might happen during the provisioning of SCOM extension or SCOM installation.

**Resolution**

To resolve this, report to Development Team.

### Issue: Conflict

**Cause**

This occurs if patching or scaling is already on going. Another operation can't be triggered.

**Resolution**

To resolve tihs, Wait for the ongoing process to complete and try again.

## Patching UI

### Issue: One or more controls on the patching blade are not visible

**Cause** 

Development Issue.

**Resolution**
	
To resolve this, report to Development Team.

### Issue: Notification is stuck at *Fetching updates* even though the update operation is complete

**Cause**

Network Issue/ Development Issue.

**Resolution**

To resolve this, try refreshing for updates. If not resolved, report to Dev Team.

### Issue: Update state isn't reflected correctly on the card

**Cause**

Network Issue/ Development Issue.

**Resolution**

To resolve this, try refreshing for updates. If not resolved, report to Dev Team.

### Inconsistency in the controls within the card

For example, the update button is enabled even though the title of the card reads - **SCOM is up to date**.

**Cause**

Development Issue.

**Resolution**

To resolve this, report to Development Team.

### Issue: Warning ribbon for updates pop up in scenarios

**Cause**

This occures due to the following:
1. New update is available, and the user has not triggered update instance
2. Last update failed and the user has not triggered update instance

**Resolution**

To resolve this, trigger *update instance*.

### Issue: Update fails on more than 1 retries

**Cause**	
**Resolution**

To resolve this, report to Development Team.

### Issue: Update fails and rollback fails leaving an inconsistent state where the number of VMs on the VMSS instance has been modified

**Cause**
**Resolution**

To resolve this, report to Development Team.

### Update fails but database update is successful

**Cause**

This occurs due to failed update after the successful database update.

**Resolution**

To resolve this, report to Development Team.

### Issue:	After successful update, SCOM console isn't functioning properly on the instance

**Cause**

This occures if SCOM is not installed properly or some process might be stuck.

**Resolution**

To resolve this, try to restart the instance. If issue persists report to the dev team.

### Issue: Update is taking more than 3 hours -> FAILS eventually

**Cause**

This occurs when the update takes more than 3 hours.

**Resolution**

To resolve this, report to Development Team.

### Issue: Some intermittent issue during update

**Cause**

This occurs if service fabric or RP crashes or restarts.

**Resolution**

To resolve this, restart the update.

### Issue: Scaling and Patching triggered simultaneously -> FAILS

**Cause**

This occurs if scaling and patching requests are sent and accepted at the same time.

**Resolution**

In case you have triggered a scaling operation, wait for the operation to complete before you try update operation.

### Issue: Extension takes more time to update -> FAILING

**Cause**

This occures if SQL MI and SCOM Managed Instance (preview) are in different regions. Due to this, extension takes more time to update and eventually fails.

**Resolution**

To resolve this, have SQL MI and SCOM Managed Instance (preview) in same region.

### Issue: After patching, user data in database is altered or not retained properly

**Cause**

This occurs if update did not happen properly.

**Resolution**

To resolve this, restart the update.

### Issue: Patching request fails

**Cause**

This occurs due to portal or ARM Issue.

**Resolution**

To resolve this, wait for some time and retry. If issue exists even after fixing portal/ ARM issue, report to Development Team.


### Issue: Patching or scaling operation is already in progress, please try again after sometime.

**Cause**

This occurs if patching or scaling operation is already in progress.

**Resolution**

To resolve this, wait for existing operation to complete and try after sometime.