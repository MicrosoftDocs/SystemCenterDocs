---
ms.assetid: 
title: Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 02/13/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)

This article provides detailed information on how you can migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview).

Provided the procedure for the following artifacts as an example:

- Management Packs and Overrides 
- Dashboard
- User roles and permissions 
- Notification subscriptions 
- Groups 
- 1P Integrations 
- Agent mapping and configuration

[Here's](#supported-artifacts-for-migration) the complete list of supported artifacts.

## Migrate from on-premises to SCOM Managed Instance (preview)

Select the required artifact to view the migration procedure from on-premises to SCOM Managed Instance (preview):

# [Management Packs and Overrides](#tab/mp-overrides)

1. Run the below script to create an inventory of all existing Management Packs deployed in Operations Manager: 

    ```powershell
    Get-SCOMManagementPack | Select-Object DisplayName, Name, Sealed, Version, LastModified | Sort-Object DisplayName | Format-Table
    ```

2. Export [unsealed Management Packs](/system-center/scom/manage-mp-import-remove-delete?#how-to-export-an-operations-manager-management-pack):

   ```powershell
   Get-SCOMManagementPack | Where{ $_.Sealed -eq $false } | Export-SCOMManagementPack -Path "C:\Temp\Unsealed Management Packs"
   ```

3. Import [Sealed Management Packs in SCOM Managed Instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#importing-a-management-pack).

    - You must have a copy of any custom sealed Management Packs that you need to import. 

4. Import [unsealed (exported) Management Packs in SCOM Managed Instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#import-a-management-pack-from-disk).

### Post migration validation

Follow these steps to validate the migration of Groups and Data collection.

1. **In Groups**: Go to **Authoring** workspace in the Operations Manager console and select **Groups**. Review the membership of any groups created by the Management Packs and verify that they've been populated with the correct objects. 

1. **In Data collection**: To verify that the intended objects are discovered, go to **Monitoring** in the Operations Manager console and review the views for each Management Pack.

    1. Verify that the state views are populated with the correct objects (Servers, Databases, Websites, and so on) and they're being monitored (Health State isn't **Unmonitored**).

    1. Check the performance views and verify that the performance data has been collected.

# [Dashboard](#tab/dashboard)

Operations Manager supports the following four types of data visualizations. 
Below is a quick summary of what can be migrated:

| Types of data visualizations | Can be migrated to SCOM Managed Instance (preview) | Recommendations |
|---|---|---|---|---|
| Dashboards/Views that are available in Management Pack | Yes | Operations console |
| Dashboards/Views created on Operations console | Yes | Operations console |
| Reports that are available in Management Pack | No | Power BI reports |
| Reports that are created on Operations console | No | Power BI reports |

- For Dashboards/Views that's available in Management Pack, you can view the data similar to the one in Operations Manager on-premises (as they're built into Management Pack).
- For Dashboards/Views created on the Operations console, you need to reconfigure custom dashboards and views in SCOM Managed Instance (preview). 
- For (SSRS) reports that are available in Management Pack and on the Operations console, you need to reconfigure all reports on Power BI as the Reporting Server doesn't exist in SCOM Managed Instance (preview).  

# [User roles and permissions](#tab/userrole-permission)

>[!Note]
> No 1:1 mapping is permitted between user roles in SCOM Managed Instance (preview) to Operations Manager on-premises.

In preview, only two user roles are available, whereas Operations Manager on-premises has 10 user profile roles. For more information, see [Operations associated with user role profiles](/system-center/scom/manage-security-create-runas-account). 

Use the following mapping chart to provide access on SCOM Managed Instance (preview) with appropriate permissions:

### Mapping chart 

| Operations Manager on-premises  | SCOM Managed Instance (preview) |
|---------------------------------|-----------------------------------------------|
| Report Operator                 | Reader                                        |
| Read-Only Operator              | Reader                                        |
| Operator                        | Reader                                        |
| Advanced Operator               | Reader                                        |
| Application Monitoring Operator | Reader                                        |
| Author                          | Contributor                                   |
| Administrator                   | Contributor                                   |
| Report Security Administrator   | Contributor                                   |
| Read-only Administrator         | Contributor                                   |
| Delegated administrator         | Contributor                                   |

1. Export the list of user roles and users in each role. 

    ```powershell
    # This script will export the SCOM User Roles to CSV and Text File Format.
    # -----------------------------------------------
    # Outputs the file to the current users desktop
    # -----------------------------------------------
    $UserRoles = @()
    $UserRoleList = Get-SCOMUserRole
    Write-Output "Processing User Role:  "
    foreach ($UserRole in $UserRoleList)
    {
      Write-Output "    $UserRole"
      $UserRoles += New-Object -TypeName psobject -Property @{
        Name = $UserRole.Name;
        DisplayName = $UserRole.DisplayName;
        Description = $UserRole.Description;
        Users = ($UserRole.Users -join "; ");
      }
    }
    $UserRolesOutput = $UserRoles | Select-Object Name, DisplayName, Description, Users
    # Table Output
    $UserRolesOutput | Format-Table -AutoSize
    # CSV Output
    $UserRolesOutput | Export-CSV -Path "$env:USERPROFILE`\Desktop\UserRoles.csv" -NoTypeInformation
    # Text File Output
    $UserRolesOutput | Out-File "$env:USERPROFILE`\Desktop\UserRoles.txt" -Width 4096
    ```

2. With the exported list and mapping recommendations, manually add the users to the respective Azure (SCOM Managed Instance (preview)) user roles. 

# [Notification subscriptions](#tab/notification-subscriptions)

SCOM Managed Instance (preview) supports the following notification channels:

- Emails
- SMS/Text

Export the **Notifications Internal Library** Management pack from the Operations Manager Management Group to migrate all your notification settings and import them to SCOM Managed Instance (preview).

After you migrate the notification configuration to SCOM Managed Instance (preview), copy the local files that are used in Command Channels to the same path on all Management Servers in the Notification Resource Pool. If you migrate from Operations Manager 2016, configuring Notification Channel requires more steps.

# [Groups](#tab/groups)

Groups are migrated as part of Management Packs. For more information, see **step 5** in the **Management Packs and Overrides** tab.

# [1P Integrations](#tab/integrations)

The following integrations are supported:

- Service Manager 
- System Center Virtual Machine Manager
- Azure Monitor 

System Center Orchestrator to Azure Automation is the recommendation on Azure equivalent services.

# [Agent mapping and configuration](#tab/agent-mapping-config)

To migrate from Agent to SCOM Managed Instance (preview), see [High level overview of upgrading agents and running two environments](/system-center/scom/deploy-upgrade-overview#high-level-overview-of-upgrading-agents-and-running-two-environments-1).

--- 

### Supported artifacts for migration

- Management Packs and Overrides 
- Dashboard
- User roles and permissions 
- Notification subscriptions 
- Groups 
- 1P Integrations 
- Agent mapping and configuration
- Gateways 
- Custom and 3P Solutions 

## Next steps

[Create a SCOM Managed Instance (preview) on Azure](create-operations-manager-managed-instance.md).

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).

