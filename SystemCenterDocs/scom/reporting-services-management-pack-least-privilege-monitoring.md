---
ms.assetid: 7820156f-399a-4bad-a7bf-98d40a76be30
title: Least-privilege Monitoring Configuration in Management Pack for SQL Server Reporting Services
description: This article explains least-privilege monitoring configuration
author: Anastas1ya
ms.author: v-fkornilov
manager: evansma
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Least-Privilege Monitoring Configuration

This article explains how to configure least-privilege monitoring in Management Pack for SQL Server Reporting Services.

## Active Directory

To configure permissions in Active Directory, perform the following steps:

1. In Active Directory, create the following domain users for low-privilege access to all target SSRS instances and SQL Server instances hosting reporting database:

    - SSRSMonitoring
    - SSRSDiscovery
    - SSRSSDK

2. Create a **SSRSMPLowPriv** domain group and add the following domain users:

   - SSRSMonitoring
   - SSRSDiscovery

## Agent Machines

To configure permissions on the agent machines, grant local administrator permissions to the **SSRSMPLowPriv** group.

## SQL Server Reporting Services Instance

To configure permissions on an instance of SQL Server Reporting Services, perform the following steps:

1. Open a web browser and connect to SSRS Report Manager.

2. Select **Site Settings** in the upper-right corner of the page to navigate to the **Site Settings** page.

3. Select **Security** on the left side of the **Site Settings** page.

4. Select **New Role Assignment**.

5. On **New Role Assignment**, enter the group name (**<Your Domain\>\\SSRSMPLowPriv**) and select the **System Administrator** checkbox.

6. Select **OK**.

## SQL Server Reporting Services Catalog Database

To configure permissions on SQL Server Reporting Services Catalog Database, perform the following steps:

1. In SQL Server Management Studio, for the instance of SQL Server Database Engine that hosts SSRS Catalog Database, create a sign-in for **SSRSMPLowPriv**.

2. Create a **SSRSMPLowPriv** user in both SSRS Catalog and Temporary databases.

3. Assign the **db\_datareader** role to **SSRSMPLowPriv** on both SSRS Catalog and Temporary databases.

## Configure System Center Operations Manager

To configure System Center Operations Manager, perform the following steps:

1. Import [Management Pack for SQL Server](sql-server-management-pack-management-pack-delivery.md) if it hasn't been imported.

2. Create **SSRSMonitoring**, **SSRSDiscovery** and **SSRSSDK**  Run As accounts with the **Windows** account type. For more information about how to create a Run As account, see [How to create a Run As account and associate with a Run As profile](manage-security-create-runas-link-profile.md). For more information about various Run As Account types, see [Manage Run As accounts and profiles](manage-security-maintain-runas-profiles.md).

3. On System Center Operations Manager console, configure the Run As profiles as follows:

    - Instruct the **Microsoft SQL Server Discovery Run As Profile** Run As profile to use the **SSRSDiscovery** Run As account.  

    - Instruct the **Microsoft SQL Server Monitoring Run As Profile** Run As profile to use the **SSRSMonitoring** Run As account.  

    - Instruct the **Microsoft SQL Server SDK Run As Profile** Run As profile to use the **SSRSSDK** Run As account.

>[!NOTE]
>**Microsoft SQL Server on Windows (Discovery)** uses the same Run As Profiles; ensure to adjust the low-privilege configuration for this pack as well.

### Permissions on System Center Operations Manager

To configure permissions on System Center Operations Manager Management Server, perform the following steps:

1. Grant Local Administrator permissions to the **SSRSSDK** account.

2. Open the System Center Operations Manager console and navigate to the **Administration** pane.

3. Open the **User Roles** view (located under the **Security** folder).

4. Right-click the **Operations Manager Operators** role and select **Properties**.

5. On the **General Properties** tab, select **Add**.

6. Find the **SSRSSDK** user and select **OK**.

7. Select **OK**.
