---
ms.assetid: 
title: Migrate from Operations Manager on-premises to Operations Manager managed instance (preview)
description: This article describes how to migrate from Operations Manager on-premises to Operations Manager managed instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/17/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Migrate from Operations Manager on-premises to Operations Manager managed instance (preview)

This article provides detailed migration steps to the below artefacts from Operations Manager on-premises to Operations Manager managed instance (preview):

- Management Packs and Overrides 
- Dashboard and Reports 
- User roles and permissions 
- Notification subscriptions 
- Groups 
- 1P Integrations 
- Agent mapping and configuration 

>[!Note]
>Other artefacts are also supported in Operations Manager Managed Instance even though the migration steps are not provided.

## Procedure to migrate from On-premises to Operations Manager managed instance (preview)

Follow the below steps to migrate from On-premises to Operations Manager managed instance (preview):

# [Management Packs and Overrides](#tab/mp-overrides)

1. Run the below script to create an inventory of all existing MPs deployed in Operations Manager: 

\<Script to be provided by Operations Manager PG\>

2. [Export unsealed MPs](/system-center/scom/manage-mp-import-remove-delete?#how-to-export-an-operations-manager-management-pack)

3. [Import Sealed MPs in Operations Manager managed instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#importing-a-management-pack)

    - You must have a copy of any custom sealed Management Packs that you need to import. 

4. [Import unsealed (exported) MPs in Operations Manager managed instance (preview)](/system-center/scom/manage-mp-import-remove-delete?#import-a-management-pack-from-disk)

5. Validation of post migration 

    1. **Groups**: Go to **Authoring** workspace in the Operations Manager console and select **Groups**.  Review the membership of any groups created by the Management Packs and verify that they've been populated with the correct objects. 

    1. **Data collection**: To verify that the intended objects are discovered, go to **Monitoring** of the Operations Manager console and review the views for each Management Pack.

        1. Verify that the state views are populated with the correct objects (Servers, Databases, Websites, and so on) and they're being monitored (Health State isn't **Unmonitored**).

        1. Check the Performance Views and verify that performance data has been collected.

# [Dashboard and Reports](#tab/dashboard-reports)

Four types of data visualization are available in Operations Manager. 
Below is a quick summary of what can be migrated:

| Types                                          | Can be migrated to Operations Manager manager instance | Documentation | Microsoft Recommendations |
|------------------------------------------------|----------------------------|---------------|---------------------------|--|
| Dashboards/Views that are available in MP      | Yes                        | Not required  | Operations console        |
| Dashboards/Views created on Operations console | Yes                        | Yes           | Operations Console        |
| Reports that are available in MP               | No                         | No            | Power BI reports           |
| Reports that are created on Operations console | No                         | No            | Power BI reports           |

- For Dashboards/Views that are available in MP, as dashboards/views are built into Management Pack, they'll continue to display data as they did on Operations Manager on-premises.
- For Dashboards/Views created on Operations console, you need to reconfigure custom dashboards and views in Operations Manager managed instance (preview). 
- For Reports that are available in MP and on Operations console, Reporting Server doesn't exist in Operations Manager managed instance (preview). So, you need to reconfigure all reports on PowerBI. 

# [User roles and permissions](#tab/userrole-permission)

No 1:1 mapping between User roles in Operations Manager managed instance (preview) to Operations Manager on-premises. In preview, only two user roles are available whereas Operations Manager on-premises has 10 User profile roles. For more information, see [Operations associated with user role profiles](/system-center/scom/manage-security-create-runas-account). 

Use the below mapping chart to provide access on Operations Manager managed instance (preview) with appropriate permissions. 

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

1. Export the list of User roles and users in each role. 

\<Script to be provided by Operations Manager PG\>.

2. With the exported list and mapping recommendations, manually add the users to respective Azure (Operations Manager managed instance (preview)) User roles. 

# [Notification subscriptions](#tab/notification-subscriptions)

Below are the supported notification channels in Operations Manager managed instance (preview)

- Emails 
- Teams 
- SMS/Text 

Export the **Notifications Internal Library** Management pack from Operations Manager Management Group to migrate all your Notification settings and import to Operations Manager managed instance (preview).

After you migrate the notification configuration to Operations Manager managed instance (preview), copy the local files that are used in Command Channels to the same path on all Management Servers in the Notification Resource Pool. If you migrate from Operations Manager 2016, configuring Notification Channel requires additional steps.

# [Groups](#tab/groups)

Groups are migrated as part of Management Packs. For more information, see  

# [1P Integrations](#tab/integrations)

Below are the supported Integrations:

- Service Manager 
- System Center Virtual Machine Manager
- Azure Monitor 

Below is the recommendation on Azure equivalent services 

- System Center Orchestrator to Azure Automation 


# [Agent mapping and configuration](#tab/agent-mapping-config)

To migrate from Agent to Operations Manager managed instance, see [High level overview of upgrading agents and running two environments](/scom/deploy-upgrade-overview#high-level-overview-of-upgrading-agents-and-running-two-environments-1)

--- 