---
ms.assetid: 
title: Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)
description: This article describes the errors that might occur when you deploy or use Azure Monitor SCOM Managed Instance (preview) and how to resolve them.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 12/09/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)

This article describes the errors that might occur when you deploy or use Azure Monitor SCOM Managed Instance (preview) and how to resolve them.

## Scenario: SCOM Managed Instance (preview) creation/deployment

### General troubleshooting

1.	Ensure all the prerequisites are met. Creation issues may arise due to improper/incomplete prerequisites.
2.	Ensure you read/check the error message carefully. The error messages capture the issue/error in creation.
3.	Check the **SCOM Setup logs** link provided in the error message. Select the link to download the System Center Operations Manager setup logs.
4.	If you're unable to identify the issue with the above steps, login to the Virtual Machine Scale Sets instance and check the logs under *C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.SCOMMIServer.ScomServerForWindows\1.0.66*, which helps you identify the issue.
5. If the issue persists, raise a support ticket with all relevant details [`correlation-id`, `subscription-id`, etc.,]


### Issue: Resource group `%ResourceGroupName%` is managed by other Azure resource

**Cause**: Occurs when the *ManagedBy* property is set for the resource group.

**Resolution**: Provide another resource group with *ManagedBy* property as empty.

### Issue: The subnet `%SubnetName%` selected is dedicated to another service

**Cause**: Occurs when the subnet has delegations.

**Resolution**: Provide a subnet, which isn't delegated to any other service.

### Issue: Error when SCOM Managed Instance (preview) is unable to reach SQL Managed Instance `%instance%`

**Cause**: This error can be caused by any of the following reasons:
   -  Missing Line-of-sight visibility from SCOM Managed Instance (preview) VNet to SQL Managed Instance endpoint.
   -  Missing the right level of NSG rules to allow traffic over SQL Managed Instance public endpoint.
   -  MSI isn't added as Active Directory admin.
   - SCOM Managed Instance (preview) might not have read permissions on the SQL Managed Instance.
   - There might be an issue with your VNet/Region.


**Resolution:**
   - Provide read permission to the SQL Managed Instance.  
   - MSI must be added as Active Directory admin on the SQL Managed Instance.
   - Ensure connectivity between SCOM Managed Instance (preview) and SQL Managed Instance networks. For more information, see [Create and configure an SQL Managed Instance](/system-center/scom/create-operations-manager-managed-instance?tabs=prereqs-portal#create-and-configure-an-sql-mi-instance).

### Issue: Not enough cores to create `%instance%` in the given region

**Cause**: Occurs when there aren't enough cores to create an instance in the given region.

**Resolution**: Check the quota section on Azure portal and allocate more cores of type Standard Ds3v2 in the region if needed.

### Issue: Secret key with same name is already present in the Key vault

**Cause**: Occurs when another secret key with the same name is already present in the Key vault.

**Resolution**: Change the name of the instance.

### Issue: VM has reported a failure when processing extension `joindomain` to join to the domain `%DomainName%`

**Cause**: Occurs due to the following reasons:
1. Line-of-sight visibility from SCOM Managed Instance (preview) Server to Domain Controller.
2. Domain User Credentials aren't provided or incorrect.
3. OU Path for AD Domain isn't provided.

**Resolution**: Check the cause and accordingly try to resolve the issue.

### Issue: Static IP already in use

**Cause**: Occurs if the static IP is being used by another instance.

**Resolution**: Use another static IP.

### Issue: Invalid Identity Type `%identityType%`

**Cause**: Occurs due to incorrect Managed identity.

**Resolution**: Provide one of the possible Identity types ((None), (SystemAssigned,UserAssigned)) and try again.

### Issue: Private static IP address `%LbIpAddr%` doesn't belong to the range of subnet `%subnet%`

**Cause**: Occurs as the IP address isn't in the subnet range.

**Resolution**: Provide an available IP from the subnet range and retry the operation.

## Scenario: Deploy Reports on Power BI

### Issue: SQL Managed Instance isn't reachable

**Cause**: Occurs if the public endpoint isn't enabled. Power BI won't be able to reach SQL Managed Instance.

**Resolution**: Check the user permissions on SQL Managed Instance and provide the required permissions.

### Issue: Unable to refresh dataset credentials

**Cause**: Occurs if the user doesn't have appropriate permissions on the SQL Managed Instance.

**Resolution**: Check the user permissions on SQL Managed Instance and provide the required permissions.

### Issue: Report unable to refresh

**Cause**: Occurs due to large data size. The report might not refresh.

**Resolution**: If the Power BI workspace is in *pro* tier, change it to *premium* tier or change the capacity of the workspace.

## Scenario: Manual Scale up/down

### Issue: Quota Exceeded

**Cause**: Occurs if there are no cores available for scaling.

**Resolution**: Increase the number of cores in the subscription.

Check the quota section on Azure portal and allocate more cores of type Standard Ds3v2 in the region if needed.

### Issue: Extension provisioning error

**Cause**: This error might occur during the provisioning of System Center Operations Manager extension or System Center Operations Manager installation.

**Resolution**: Check the [general troubleshooting](./troubleshoot-scom-managed-instance.md#general-troubleshooting), try to identify the issue and accordingly resolve it.

### Issue: Conflict

**Cause**: Occurs if patching or scaling is in progress. A new operation can't be triggered.

**Resolution**: Wait for the ongoing process to complete and try again.

## Scenario: Patching

### Issue: Notification is stuck at *Fetching updates* even though the update operation is complete

**Cause**: Network issue/development issue.

**Resolution**: Try refreshing for updates. If not resolved, contact Microsoft support.

### Issue: Update state isn't reflected correctly on the card

**Cause**: Network issue/development issue.

**Resolution**: Try refreshing for updates. If not resolved, contact Microsoft support.

### Issue: Inconsistency in the controls within the card

**Cause**: Consistency Issue. 
For example, the update button is enabled even though the title of the card reads **SCOM is up to date**.

**Resolution**: Try refreshing. If not resolved, contact Microsoft support.

### Issue: Warning message pops up for updates

**Cause**: Occurs due to any of the following reasons:
1. New update is available, and the user hasn't triggered the update instance; or
2. Last update failed and the user hasn't triggered another update instance.

**Resolution**: Trigger an *update instance*.

### Issue: Update fails after multiple retries
	
**Resolution**: To resolve, contact Microsoft support.

### Issue: Update fails, and rollback fails to leave an inconsistent state where the number of VMs on the Virtual Machine Scale Sets instance has been modified

**Resolution**: Go to System Center Operations Manager console and remove inconsistent nodes.

### Issue: Update fails but database update is successful

**Cause**: Occurs due to failed update after the successful database update.

**Resolution**: Retry after some time.

### Issue: After successful update, System Center Operations Manager console isn't functioning properly on the instance

**Cause**: Occurs if System Center Operations Manager isn't installed properly or some process might be stuck.

**Resolution**: Try to restart the instance. If the issue persists, contact Microsoft support.

### Issue: Update is taking more than 3 hours and fails eventually

**Cause**: Occurs when the update takes more than 3 hours.

**Resolution**: Contact Microsoft support.

### Issue: Some intermittent issue during update

**Cause**: Occurs if the service fabric or RP crashes or restarts.

**Resolution**: Restart the update.

### Issue: Scaling and Patching triggered simultaneously and then fails

**Cause**: Occurs if scaling and patching requests are sent and accepted at the same time.

**Resolution**: In case you've triggered a scaling operation, wait for the operation to complete before you try to update operation.

### Issue: Extension takes more time to update and fails

**Cause**: Occurs if SQL Managed Instance and SCOM Managed Instance (preview) are in different regions due to which the extension takes more time to update and eventually fails.

**Resolution**: Have SQL Managed Instance and SCOM Managed Instance (preview) in same region.

### Issue: After patching, user data in the database is altered or not retained properly

**Cause**: Occurs if update wasn't done properly.

**Resolution**: Restart the update.

### Issue: Patching request fails

**Cause**: Occurs due to portal or ARM issue.

**Resolution**: Wait for some time and retry. If the issue exists even after fixing the portal/ARM issue, contact Microsoft support.

### Issue: Patching or scaling operation is already in progress, try again after some time.

**Cause**: Occurs if a patching or scaling operation is already in progress.

**Resolution**: Wait for the existing operation to complete and try after some time.

### Issue: Stale Management Servers visible on console

**Cause**: Occurs if a patching or scaling operation has left an inconsistent state after completion.

**Resolution**: Go to System Center Operations Manager console and remove the stale management servers.