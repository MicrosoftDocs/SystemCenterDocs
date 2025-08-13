---
ms.assetid: 50e3914b-4047-4dce-97f1-0bca1619f4a1
title: Operations Associated with User Role Profiles
description: This article describes the user roles in Operations Manager and they what actions they can perform in the management group.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Operations associated with user role profiles



This article provides a list of the operations in System Center Operations Manager that are associated with each profile.  

::: moniker range="sc-om-2022"

You can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

In addition to the existing operations, Operations Manager 2022 supports *Read-only Administrator* and *Delegated administrator* roles. The operations for these roles are detailed in the sections below.

::: moniker-end

## Report Operator  

The Report Operator profile includes a set of privileges designed for users who need access to reports. A role based on the Report Operator profile grants members the ability to view reports according to their configured scope.  

-   Retrieve the instance of the data warehouse for the management group  

-   Write to favorite reports  

-   Delete favorite reports  

-   Read favorite reports  

-   Update favorite reports  

-   Read reports  

-   Run reports  

-   Access Application Advisor  

## Read-Only Operator  

The Read-Only Operator profile includes a set of privileges designed for users who need read-only access to alerts and views. A role based on the Read-Only Operators profile grants members the ability to view alerts and access views according to their configured scope.  

-   Read alerts  

-   Retrieve the instance of the data warehouse for the management group  

-   Read state of a resolution  

-   Read instance of a connector  

-   Read console tasks  

-   Enumerate diagnostic objects  

-   Enumerate the results of diagnostics  

-   Enumerate discovery objects as defined in a management pack  

-   Read discovery rules  

-   Read events  

-   Write to favorite console tasks  

-   Delete favorite console tasks  

-   Enumerate favorite console tasks  

-   Update favorite console tasks  

-   Write favorite views  

-   Delete favorite views  

-   Enumerate favorite views  

-   Update favorite views  

-   Enumerate monitoring objects  

-   Enumerate monitoring classes  

-   Enumerate monitoring relationship classes  

-   Enumerate management packs  

-   Enumerate monitor types  

-   Enumerate module types  

-   Enumerate monitors  

-   Enumerate overrides  

-   Enumerate performance data  

-   Enumerate discovery objects as defined in a management pack  

-   Enumerate the status of past recoveries  

-   Enumerate relationship between monitored objects  

-   Enumerate rules  

-   Enumerate saved searches  

-   Update saved searches  

-   Write to saved searches  

-   Delete saved searches  

-   Enumerate state  

-   Allows access to connected management groups  

-   Enumerate views  

-   Enumerate view types  

-   Review application monitoring alerts<sup>1</sup>  

<sup>1</sup> Permissions scope can be fine-tuned for the role.  

## Operator  

The Operator profile includes a set of privileges designed for users who need access to alerts, views, and tasks. A role based on the Operators profile grants members the ability to interact with alerts, run tasks, and access views according to their configured scope. The Operator profile contains all of the privileges found in the Read-Only Operator profile in addition to those listed below.  

-   Update alerts  

-   Run diagnostics  

-   Create favorite tasks  

-   Delete favorite tasks  

-   Enumerate favorite tasks  

-   Update favorite tasks  

-   Run recovery routines  

-   Update maintenance mode settings  

-   Enumerate notification actions  

-   Delete notification actions  

-   Update notification actions  

-   Enumerate notification endpoints  

-   Enumerate notification recipients  

-   Delete notification recipients  

-   Update notification recipients  

-   Enumerate notification subscriptions  

-   Delete notification subscriptions  

-   Update notification subscriptions  

-   Enumerate tasks  

-   Enumerate task status  

-   Run tasks  

-   Run monitoring compatibility check task<sup>1</sup>  

    > [!NOTE]  
    > Additional permissions are required for files/folders to create report files.  

-   Review application monitoring alerts  

-   Close application monitoring alerts<sup>1</sup>  

<sup>1</sup> Permissions scope can be fine-tuned for the role.  

## Advanced Operator  

The Advanced Operator profile includes a set of privileges designed for users who need access to limited tweaking of monitoring configurations in addition to the Operators privileges. A role based on the Advanced Operators profile grants members the ability to override the configuration of rules and monitors for specific targets or groups of targets within the configured scope. The Advanced Operator profile contains all of the privileges found in the Operator and Read-Only Operator profiles in addition to those listed below.  

-   Update management packs  

-   Enumerate templates  

-   Customize APM configuration with the overrides<sup>1</sup>  

-   Run monitoring compatibility check task<sup>1</sup>  

    > [!NOTE]  
    > Additional permissions are required for files/folders to create report files.  

-   Review application monitoring alerts<sup>1</sup>  

-   Close application monitoring alerts<sup>1</sup>  

<sup>1</sup> Permissions scope can be fine-tuned for the role.  

## Application Monitoring Operator  

The Application Monitoring Operator profile includes a set of privileges designed for users that need access to Application Diagnostics. A user role based on the Application Monitoring Operator profile grants members the ability to see the Application Monitoring events in Application Diagnostics web console.  

-   Access Application Diagnostics  

## Author  

The Author profile includes a set of privileges designed for authoring monitoring configurations. A role based on the Author's profile grants members the ability to create, edit, and delete monitoring configuration (tasks, rules, monitors, and views) within the configured scope. For convenience, Authors can also be configured to have Advanced Operator privileges scoped by group. The Author profile contains all of the privileges found in the Advanced Operator, Operator, and Read-Only Operator profiles in addition to those listed below.  

-   Create management packs  

-   Delete management packs  

-   Enumerate Run As Profiles  

-   Customize APM configuration with the overrides<sup>1</sup>  

-   Author new APM workflows<sup>1</sup>  

-   Run monitoring compatibility check task<sup>1</sup>  

    > [!NOTE]  
    > Additional permissions are required for files/folders to create report files.  

-   Review application monitoring alerts<sup>1</sup>  

-   Close application monitoring alerts<sup>1</sup>  

<sup>1</sup> Permissions scope can be fine-tuned for the role.  

## Administrator  

The Administrator profile includes full privileges to Operations Manager. No scoping of the Administrator profile is supported. The Administrator profile contains all the privileges found in the Author, Advanced Operator, Operator, and Read-Only Operator profiles in addition to those listed below.  

-   Create a resolution state  

-   Delete a resolution state  

-   Update a resolution state  

-   Deploy an agent  

-   Repair or update an installed agent  

-   Uninstall an agent  

-   Enumerate agent settings  

-   Update agent settings  

-   Enumerate agents  

-   Start or stop managing computers or devices via a proxy health service  

-   Enumerate computers or devices managed via a proxy health service  

-   Insert a new instance of a computer or device  

-   Delete an instance of a computer or device  

-   Run discovery task  

-   Create events  

-   Enumerate global settings  

-   Update global settings  

-   Export management packs  

-   Enumerate management servers  

-   Delete notification endpoint  

-   Update notification endpoint  

-   Create performance data  

-   Create Run As Accounts  

-   Delete Run As Accounts  

-   Enumerate Run As Accounts  

-   Update Run As Accounts  

-   Create mappings between Run As Accounts and Run As Profiles  

-   Delete mappings between Run As Accounts and Run As Profiles  

-   Enumerate mappings between Run As Accounts and Run As Profiles  

-   Update mappings between Run As Accounts and Run As Profiles  

-   Create connected management groups  

-   Delete connected management groups  

-   Enumerate user roles  

-   Delete user roles  

-   Update user roles  

-   Write favorite reports  

-   Delete favorite reports  

-   Read favorite reports  

-   Update favorite reports  

-   Read reports  

-   Run reports  

-   Run APM Wizard or change APM settings  

-   Access Application Diagnostics  

-   Access Application Advisor  

-   Author new APM workflows  

-   Customize APM configuration with the overrides  

-   Run monitoring compatibility check task  

-   Review application monitoring alerts  

-   Close application monitoring alerts  

-   Control access rights to application monitoring  

-   Create group  

-   Edit group  

-   Delete group  

## Report Security Administrator  

The Report Security Administrator profile includes a set of privileges designed to enable the integration of SQL Server Reporting Services security with Operations Manager.  

-   Export management packs  

-   Enumerate classes as defined in the management packs  

-   Enumerate management packs  

-   Run reports  

-   Enumerate rules  

-   Access Application Advisor  

::: moniker range="sc-om-2022"

## Read-only Administrator

The Read-only Administrator profile includes all the read privileges in Operations Manager along with reporting.

You can create custom user roles with specific permissions. The **Agent Management** now supports two new subcategories - **Deploy Agents** and **Repair Agents**, that implicitly provide permission to **Agent Pending Actions**.

**Deploy Agents** and **Repair Agents** has dependency on **Agent Pending Actions**.

>[!NOTE]
>Uninstallation of agents works independently.

## Delegated administrator

The Delegated administrator profile includes all the read privileges in Operations Manager except reporting. Create a custom role with Delegated administrator as the base profile, and one or more permissions from the following categories:

-   Agent management

-   Account management

-   Connector management

-   Global settings

-   Management pack authoring

-   Notification management

-   Operations permissions

-   Reporting permissions

::: moniker-end

## Next steps

- To understand the profiles defined in Operations Manager to manage authorization and security, and configure user roles to perform administration and access to operational data in the management group, review [Implementing User Roles](~/scom/manage-security-overview.md).
