---
title: Post-Upgrade Tasks When Upgrading to System Center 2012  R2 Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbd5dddd-b002-45fa-999a-3e751309ee93
author:mgoedtel
manager:cfreemanwa
---
# Post-Upgrade Tasks When Upgrading to System Center 2012  R2 Operations Manager
After you have completed the upgrade process to [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)], you must perform a number of post\-upgrade tasks.  
  
## Post\-Upgrade Tasks  
Perform the following tasks when you have completed the upgrade process.  
  
1.  Re\-enable the Notification Subscriptions.  
  
2.  Restart or Re\-enable the Connector Services \(if needed\)  
  
3.  Re\-enable Audit Collection Services \(ACS\) on agents that were upgraded  
  
4.  Verify That the Upgrade Was Successful  
  
## Re\-enable the Notification Subscriptions  
After the upgrade has finished, use the following procedure to re\-enable subscriptions.  
  
#### To re\-enable the subscriptions  
  
1.  Open the Operations console by using an account that is a member of the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] Administrators role for the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] management group.  
  
2.  In the Operations console, in the navigation pane, click the **Administration** button.  
  
    > [!NOTE]  
    > When you run the Operations console on a computer that is not a management server, the **Connect To Server** dialog box appears. In the **Server name** text box, type the name of the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] management server to which you want to connect.  
  
3.  In the **Administration** pane, under **Notifications**, click **Subscriptions**.  
  
4.  In the **Actions** pane, click **Enable** for each subscription listed.  
  
## Restart or Re\-enable the Connector Services  
Refer to the third\-party documentation for any installed connectors to determine if the connectors are supported for [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)].  If you stopped a connector for any reason during upgrade, restart the service.  
  
#### To restart a connector service  
  
1.  On the taskbar, click **Start**, click **Administrative Tools**, and then click **Services**.  
  
2.  In the **Name** column, right\-click the connector that you want to restart, and then click **Start**.  
  
## Re\-Enable Audit Collection Services  
If you had Audit Collection Services \(ACS\) enabled for an agent prior to upgrade, it was disabled as part of the agent upgrade process. Re\-enable ACS as appropriate.  
  
## Verify That the Upgrade Was Successful  
Perform the following tasks to verify that the upgrade was successful.  
  
-   Check the health state of the management servers and agents in the Health Service Watcher state view. In the **Administration** workspace of the Operations console, ensure that the management servers and agents are healthy. In the **Monitoring** workspace, check if there are any alerts related to the management group health.  
  
-   Review the event logs of all the management servers for new errors.  
  
-   Sort alerts by the last\-modified column to review the new alerts.  
  
-   Check the CPU utilization and disk I\/O on your database servers to ensure that they are functioning normally.  
  
-   If the Reporting feature is installed, click **Reporting**, and then run a generic performance report to ensure that Reporting is functioning correctly.  
  
-   Re\-deploy any agents that you uninstalled during the upgrade process.  
  
