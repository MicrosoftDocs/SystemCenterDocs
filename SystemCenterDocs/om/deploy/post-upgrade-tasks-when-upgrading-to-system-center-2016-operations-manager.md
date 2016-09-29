---
title:  Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

After you have completed the upgrade process to System Center 2016 - Operations Manager, you must perform a number of post-upgrade tasks.

## Post-upgrade tasks

Perform the following tasks when you have completed the upgrade process.

1. Re-enable the Notification Subscriptions

2. Restart or re-enable the Connector Services (if needed)

3. Re-enable Audit Collection Services (ACS) on agents that were upgraded

4. Verify the upgrade was successful

### Re-enable the notification subscriptions

After the upgrade has finished, use the following procedure to re-enable subscriptions.

#### To re-enable the subscriptions

1. Open the Operations console with an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.
2. In the Operations console, in the navigation pane, click the **Administration** button.

    > [!NOTE]
    > When you run the Operations console on a computer that is not a management server, the Connect To Server dialog box appears. In the Server name text box, type the name of the Operations Manager management server to which you want to connect.


3. In the **Administration** pane, under **Notifications**, click **Subscriptions**.
4. n the **Actions** pane, click **Enable** for each subscription listed that was enabled prior to performing the upgrade.

### Restart or re-enable the connector services

Refer to third-party documentation for any installed connectors to determine if the connectors are supported for System Center 2016 - Operations Manager. If you stopped a connector for any reason during upgrade, restart the service.

#### To restart a connector service

1. Open the Services MMC snap-in. Click **Start**, and then type **services.msc** in the **Start Search** box.
2. In the **Name** column, right-click the connector that you want to restart, and then click **Start**.

### Re-Enable Audit Collection Services

If you had Audit Collection Services (ACS) enabled for an agent prior to upgrade, it was disabled as part of the agent upgrade process. Re-enable ACS as appropriate.

### Verify That the upgrade was successful

Perform the following tasks to verify that the upgrade was successful.

- Check the health state of the management and gateway servers, and agents in the Health Service Watcher state view. In the **Administration** workspace of the Operations console, ensure that the management and gateway servers, and agents are healthy. In the **Monitoring** workspace, check if there are any alerts related to the management group health.
- Review the event logs of all the management servers for new errors.
Sort alerts by the last-modified column to review the new alerts.
- Monitor CPU and memory utilization, and disk I/O on your database servers to ensure that they are functioning normally.
- If the Reporting feature is installed, click Reporting, and then run a generic performance report to ensure that Reporting is functioning correctly.

## Next steps

- See [Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  