---
ms.assetid: 0bbddc74-0324-4cf5-8613-ab7e85c3d0d3
title: Post-Upgrade Tasks When Upgrading to System Center Operations Manager
description: This guide provides the post-upgrade tasks you must perform after upgrading to Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
ms.update-cycle: 1095-days
---

# Post-Upgrade tasks when upgrading to System Center Operations Manager

After you've completed the upgrade process, you must perform many post-upgrade tasks.

## Post-upgrade tasks

Perform the following tasks when you've completed the upgrade process.

1. Re-enable the Notification Subscriptions

2. Restart or re-enable the Connector Services (if needed)

3. Re-enable Audit Collection Services (ACS) on agents that were upgraded

4. Reset agent HealthService Cache size

5. Verify the upgrade was successful

### Re-enable the notification subscriptions

After the upgrade has finished, use the following procedure to re-enable subscriptions.

1. Open the Operations console with an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.
2. In the Operations console, in the navigation pane, select the **Administration** button.

    > [!NOTE]
    > When you run the Operations console on a computer that isn't a management server, the **Connect To Server** dialog appears. In the **Server name** text box, enter the name of the Operations Manager management server to which you want to connect.

3. In the **Administration** pane, under **Notifications**, select **Subscriptions**.
4. In the **Actions** pane, select **Enable** for each subscription listed that was enabled prior to performing the upgrade.

### Restart or re-enable the connector services

Refer to third-party documentation for any installed connectors to determine if the connectors are supported for System Center Operations Manager. If you stopped a connector for any reason during upgrade, restart the service.

Follow these steps to restart a connector service:

1. Open the Services MMC snap-in. Select **Start**, and then enter **services.msc** in the **Start Search** box.
2. In the **Name** column, right-click the connector that you want to restart, and select **Start**.

### Re-enable Audit Collection Services

If you had Audit Collection Services (ACS) enabled for an agent prior to upgrade, it was disabled as part of the agent upgrade process. Re-enable ACS as appropriate.

### Reset agent HealthService cache size

Restore the default setting for the agent HealthService cache size by updating the following registry setting on the agents manually or automated with your configuration management or orchestration solution:
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlsSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName\>\maximumQueueSizeKb

The default decimal value of DWORD type is 15360 (15 MB).

### Verify that the upgrade was successful

Perform the following tasks to verify that the upgrade was successful.

- Check the health state of the management and gateway servers, and agents in the Health Service Watcher state view. In the **Administration** workspace of the Operations console, ensure that the management and gateway servers and agents are healthy. In the **Monitoring** workspace, check if there are any alerts related to the management group health.
- Review the event logs of all the management servers for new errors. Sort alerts by the last-modified column to review the new alerts.
- Monitor CPU and memory utilization and disk I/O on your database servers to ensure that they're functioning normally.
- If the Reporting feature is installed, select Reporting, and then run a generic performance report to ensure that Reporting is functioning correctly.

### Apply the workaround to make the AD rules work

::: moniker range="<=sc-om-2022"

Previous AD rules don't work after upgrading to Operations Manager 2019. After you upgrade to Operations Manager 2019 from Operations Manager 2016 (or 2016 URs earlier to UR7), previous AD rules don't work due to the change in Active Directory rules' format. Upgrade to Operations Manager 2019 from Operations Manager 2016 UR7 and UR8 doesn't have this issue.

::: moniker-end

::: moniker range="sc-om-2025"

Previous AD rules don't work after upgrading to Operations Manager 2025. After you upgrade to Operations Manager 2025 from Operations Manager 2022, previous AD rules don't work due to the change in Active Directory rules' format.

::: moniker-end

Use the following steps to fix this issue:

::: moniker range="<=sc-om-2022"

1. After you upgrade to 2022, export the default management pack to a folder.

::: moniker-end

::: moniker range="sc-om-2025"

1. After you upgrade to 2025, export the default management pack to a folder.

::: moniker-end

2. Open **Microsoft.SystemCenter.OperationsManager.DefaultUser.xml** from the exported folder.
3. Rename all the AD rules to use \<NetBIOS Domain Name of Management Server\> instead of \<FQDN of Management Server\>, example below.

    >[!NOTE]
    > Domain name is case-sensitive.

    **Example:**

    Before: Rule ID="_smx.net_MS1_contoso.com" Enabled="true"

    After: Rule ID="_SMX_MS1_contoso.com" Enabled="true"

4. Import the updated management pack.

    The rules are now visible on the console.

    For detailed information about this issue, see [update an active directory integration with Operations Manager](https://techcommunity.microsoft.com/t5/system-center-blog/update-on-active-directory-integration-with-scom/ba-p/1226768).

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).  
