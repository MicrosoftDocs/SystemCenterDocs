---
ms.assetid: 
title: Migrate from Operations Manager on-premises to Operations Manager managed instance (preview)
description: This article describes how to migrate from Operations Manager on-premises to Operations Manager managed instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/20/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Migrate from Operations Manager on-premises to Operations Manager managed instance (preview)

This article provides detailed information about how you can migrate from Operations Manager on-premises to Operations Manager managed instance (preview). 

As an example of migration, provided the procedure for the following artifacts:

- Management Packs and Overrides 
- Dashboard and Reports 
- User roles and permissions 
- Notification subscriptions 
- Groups 
- 1P Integrations 
- Agent mapping and configuration

[Here](#supported-artifacts-for-migration) is the complete list of supported artifacts.

## Migrate from on-premises to Operations Manager managed instance (preview)

Select the required artifact to view the migration procedure from on-premises to Operations Manager managed instance (preview):

# [Management Packs and Overrides](#tab/mp-overrides)

1. Run the below script to create an inventory of all existing Management Packs deployed in Operations Manager: 

    \<Script to be provided by Operations Manager PG\>

2. [Export unsealed Management Packs](/system-center/scom/manage-mp-import-remove-delete?#how-to-export-an-operations-manager-management-pack).

3. [Import Sealed Management Packs in Operations Manager managed instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#importing-a-management-pack).

    - You must have a copy of any custom sealed Management Packs that you need to import. 

4. [Import unsealed (exported) Management Packs in Operations Manager managed instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#import-a-management-pack-from-disk).

### Post migration validation

Use these steps to validate the migration of Groups and Data collection.

1. **Groups**: Go to **Authoring** workspace in the Operations Manager console and select **Groups**.  Review the membership of any groups created by the Management Packs and verify that they've been populated with the correct objects. 

1. **Data collection**: To verify that the intended objects are discovered, go to **Monitoring** in the Operations Manager console and review the views for each Management Pack.

    1. Verify that the state views are populated with the correct objects (Servers, Databases, Websites, and so on) and they're being monitored (Health State isn't **Unmonitored**).

    1. Check the performance views and verify that performance data has been collected.

# [Dashboard and Reports](#tab/dashboard-reports)

Operations Manager supports the following four types of data visualizations. 
Here is a quick summary of what can be migrated:

| Types of data visualizations | Can be migrated to Operations Manager managed instance (preview) | Recommendations |
|---|---|---|---|---|
| Dashboards/Views that are available in Management Pack | Yes | Operations console |
| Dashboards/Views created on Operations console | Yes | Operations Console |
| Reports that are available in Management Pack | No | Power BI reports |
| Reports that are created on Operations console | No | Power BI reports |

- For Dashboards/Views that are available in Management Pack, you can view the data similar to the one in Operations Manager on-premises(as they are built into Management Pack).
- For Dashboards/Views created on the Operations console, you need to reconfigure custom dashboards and views in Operations Manager managed instance (preview). 
- For reports that are available in Management Pack and on the Operations console, you need to reconfigure all reports on Power BI as the Reporting Server doesn't exist in Operations Manager managed instance (preview).  

# [User roles and permissions](#tab/userrole-permission)

>[!Note]
>No 1:1 mapping is permitted between user roles in Operations Manager managed instance (preview) to Operations Manager on-premises. 

In preview, only two user roles are available whereas Operations Manager on-premises has 10 user profile roles. For more information, see [Operations associated with user role profiles](/system-center/scom/manage-security-create-runas-account). 

Use the following mapping chart to provide access on Operations Manager managed instance (preview) with appropriate permissions. 

### Mapping chart 

| Operations Manager on-premises  | Operations Manager managed instance (preview) |
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

    \<Script to be provided by Operations Manager PG\>.

2. With the exported list and mapping recommendations, manually add the users to the respective Azure (Operations Manager managed instance (preview)) user roles. 

# [Notification subscriptions](#tab/notification-subscriptions)

Operations Manager managed instance (preview) supports the following notification channels:

- Emails 
- Teams 
- SMS/Text 

Export the **Notifications Internal Library** Management pack from the Operations Manager Management Group to migrate all your notification settings and import them to Operations Manager managed instance (preview).

After you migrate the notification configuration to Operations Manager managed instance (preview), copy the local files that are used in Command Channels to the same path on all Management Servers in the Notification Resource Pool. If you migrate from Operations Manager 2016, configuring Notification Channel requires additional steps.

# [Groups](#tab/groups)

Groups are migrated as part of Management Packs. For more information, see **step 5** in **Management Packs and Overrides** tab.

# [1P Integrations](#tab/integrations)

The following integrations are supported:

- Service Manager 
- System Center Virtual Machine Manager
- Azure Monitor 

System Center Orchestrator to Azure Automation is the recommendation on Azure equivalent services.

# [Agent mapping and configuration](#tab/agent-mapping-config)

To migrate from Agent to Operations Manager managed instance, see [High level overview of upgrading agents and running two environments](/scom/deploy-upgrade-overview#high-level-overview-of-upgrading-agents-and-running-two-environments-1).

--- 

### Supported artifacts for migration

- Management Packs and Overrides 
- Dashboard and Reports 
- User roles and permissions 
- Notification subscriptions 
- Groups 
- 1P Integrations 
- Agent mapping and configuration
- System Center Operations Manager Databases (Ops database and DW) 
- Operations Console 
- Web Console 
- ACS 
- Gateways 
- Active Directory integration 
- Custom and 3P Solutions 
- 3P Management Packs

## Next steps

> [!div class="nextstepaction"]
> [Operations Manager managed instance (preview) overview](operations-manager-managed-instance-overview.md)