---
ms.assetid:
title: What's New in Operations Manager
description: This article describes the new features supported in Operations Manager 2022
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 10/16/2024
ms.custom: intro-whats-new
ms.service: system-center
ms.subservice: operations-manager
ms.topic: include
---

## New features in Operations Manager 2022

The following sections introduce new and updated features in System Center Operations Manager 2022 - Operations Manager.

### Enhanced Operations Manager RBAC

With Operations Manager 2022, new build-in roles are created for enhanced user experience.  

- A new built-in role **Read-only Administrator** is supported. This role provides all the read permissions in Operations Manager including reporting.
- You can create custom user roles with specific permissions. The **Agent Management** now supports two new subcategories - **Deploy Agents** and **Repair Agents**, that implicitly provide permission to **Agent Pending Actions**.
- A new **Delegated Administrator** profile has been introduced, which is Read-Only Administrator except reporting. You can create a custom user role with **Delegated Administrator** as the base profile and add one or more permissions to it from the available categories.

### Support for Reporting Services on NTLM hardened enterprises

With Operations Manager 2022, for organizations with NTLM disabled, you can select the Reporting Manager *Authentication Type* as **Windows Negotiate**, while installing.

### Changes in Alert closure experience

With Operations Manager 2022, admin can opt to close an alert of a health monitor, which is in unhealthy state.

### Create Operations Manager database on existing SQL Always On

With Operations Manager 2022, you can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

### SHA2 encryption for certificates

Prior to Operations Manager 2016, the Linux Agent used to generate certificates and encrypt it with SHA1. From 2016, the Linux Agent generates an SHA1 certificate and then, as part of the discovery process, the certificate gets encrypted with SHA256.

With Operations Manager 2022, the certificate gets encrypted with SHA256.

### Get Alert data via REST API scoped by Group

Operations Manager 2022 supports *groupId* in Get Alert data API.

### View source FQDN for alerts

With Operations Manager 2022, you can view the source (FQDN) while tuning a management pack.

### Sort option in Overrides summary

Operations Manager 2022 supports sort option by column, in Overrides Summary.

### Improved installation experience

Operations Manager 2022 provides improved installation experience as detailed below:

Values of few registries that are customized (commonly) are retained when an update (UR/Hotfix) is installed or upgraded from Operations Manager 2019 to Operations Manager 2022.  Here's the list of registries that are backed up & retained:

| Registry Key Location                                            | Value                                      |
|------------------------------------------------------------------|--------------------------------------------|
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Cache Maximum                  |
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Checkpoint Depth Maximum       |
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Initial Database Page Count    |
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Maximum Sessions               |
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Page Hit Cache Size            |
| HKLM:\System\CurrentControlSet\Services\HealthService\Parameters | Persistence Version Store Maximum          |

- Value of custom install location of Monitoring Agent is retained when an update (UR/Hotfix) is installed or upgraded from Operations Manager 2019 to Operations Manager 2022.
- Installation of Reporting and Web Console will be successful irrespective of the updates installed on Operations Manager Management Server.
- While upgrading nonprimary Management Servers, Data warehouse registry details are retained (which were previously deleted).
- Support for group managed service accounts in the Installer setup.
- Operations Manager 2022 supports .NET 4.8.
- The Web console now utilizes HTML5 instead of Silverlight.

### View alert source under active alerts

Operations Manager 2022 supports the display of Alert source (monitor/rule) under **Console** > **Monitoring** > **Active Alerts**.

### Removed dependency on LocalSystem account

Operations Manager 2022 provides the following changes:   

- LocalSystem is no longer used internally instead of the Default Action Account. This was used earlier for APM configuration, Privileged Monitoring Account, RunAs Profile fallback. There was an association created for the Validate Subscription Account RunAs Profile.  
- LocalSystem account is still being added to Operations Manager Administrators Group by Setup, but it's now visible in the console and can be removed and added later as required.  

### Folderization of Change Tracking Reports

With Operations Manager 2022, all change tracking reports are available in one single folder by name **Change Tracking**.

### Other updates

Operations Manager 2022 also includes the following updates:

- Supports .NET 4.8
- PowerShell 3.0 version is the required minimum version. PowerShell 3.0 runs with higher .NET (.NET 4.8) version and higher CLR version.
- You must install MSOLEDBSQL before you install Operations Manager.
- Supports the following newer browsers Chrome and Edge:
    - Internet Explorer version 11.
    - Microsoft Edge version 88 and later.
    - Google Chrome version 88 and later.
- Supports Ubuntu 20, Oracle Linux 8, Debian 10, and Debian 11.
- Removed support for AIX, Solaris, RHEL 5, RHEL 6, RHEL 7 (PPC), Debian 8, SLES 11, and SLES 12 PPC.

### Discover Azure Migrate from Operations Manager console

Operations Manager 2022 allows you to discover Azure Migrate from console. You can now generate a complete inventory of your on-premises environment without appliance. This can be used in Azure Migrate to assess machines at scale. [Learn more](https://support.microsoft.com/topic/discover-azure-migrate-for-operations-manager-04b33766-f824-4e99-9065-3109411ede63).

## New features in Operations Manager 2022 UR1

The following sections introduce the new features or feature updates supported in Operations Manager 2022 Update Rollup 1 (UR1).

For problems fixed in UR1 and the installation instructions for UR1, see the [KB article](https://support.microsoft.com/topic/update-rollup-1-for-system-center-2022-operations-manager-3f5780c9-36d9-4bba-8361-d40ca7c7ae80).
