---
ms.assetid: 4cdcce73-c9a2-4795-89bc-6d51ee04cd3c
title: Configuring Run As profiles in Management Pack for SQL Server Dashboards
description: This article explains how to configure run as profiles
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Configuring Run As Profiles

When the management pack is imported for the first time, it creates a new Microsoft SQL Server visualization library Run As Profile. This profile allows creating low privilege environments for System Center Operations Manager.

To configure permissions on the System Center Operations Manager management server, perform the following steps:

1. Create a **SSVISLIB** account on the domain controller.

2. Grant Local Administrator permissions to the **SSVISLIB** account.

To configure permissions on System Center Operations Manager, perform the following steps:

1. Open the System Center Operations Manager console.

2. Open the **Administration** view.

3. In the navigation pane, select **User Roles** under the **Security** folder.

4. Right-click the **Operations Manager Operators** role and select **Properties**.

    ![Screenshot showing User role properties.](./media/sql-server-dashboards-management-pack/properties.png)

5. On the **General Properties** tab, select **Add**.

    ![Screenshot showing Adding profile.](./media/sql-server-dashboards-management-pack/adding-user.png)

6. Find the **SSVISLIB** user and select **OK**.

7. Select **OK** to save the changes, and close the **User Role Properties** dialog.

    ![Screenshot showing Saving changes.](./media/sql-server-dashboards-management-pack/saving-changes.png)
