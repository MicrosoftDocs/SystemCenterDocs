---
title: How to Synchronize Alerts with TFS in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 608cd7da-a35b-4e20-befa-7f3af55c8654
---
# How to Synchronize Alerts with TFS in System Center 2012 R2
In [!INCLUDE[omblue_1](./Token/omblue_1_md.md)], you can synchronize [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] alerts and Team Foundation Server \(TFS\) work items. When synchronization is enabled, IT operations can then assign alerts to the engineering team. Assigning an alert to engineering creates a new work item in TFS. The workflow will track and synchronize any changes that are made to TFS work items and any associated Operations Manager alerts. In order to synchronize alerts with TFS, you must first configure alert synchronization. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](./How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md).

> [!NOTE]
> Integration between [!INCLUDE[sc2012sp1_short](./Token/sc2012sp1_short_md.md)] and TFS used the Ticket ID and Owner fields of the [!INCLUDE[om12short](./Token/om12short_md.md)] alert to store and display which work item is associated with an alert and who it is assigned to. Beginning in [!INCLUDE[omblue_1](./Token/omblue_1_md.md)], two new alert fields, TFS Work Item ID and TFS Work Item Owner, hold these values. These fields are read\-only in the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] console to prevent accidental changes of the values that are controlled in TFS.
> 
> If you previously personalized any standard alert views or created your own alert views in [!INCLUDE[sc2012sp1_short](./Token/sc2012sp1_short_md.md)] using Ticket ID and Owner fields to display TFS information, you must replace those fields with the TFS Work Item ID and TFS Work Item Owner fields to continue displaying the same information. The previous Ticket ID and Owner fields are still used for synchronization of alerts with incidents in Service Manager Alert Connector.

### To assign alerts to engineering

1.  In the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[omblue_2](./Token/omblue_2_md.md)], in the navigation pane, click **Monitoring**, and then click **Active Alerts**.

2.  To assign an alert to engineering, right\-click the alert, select **Set Resolution State**, and select **Assigned to Engineering**. This action creates a TFS work item and adds the TFS work item ID to the alert.

3.  The system synchronizes all changes to the alert inside [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] and all changes to the work item in TFS.

    > [!TIP]
    > Any comments that you add to an [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] alert on the alert **History** tab are automatically added to the corresponding TFS work items. You can use this function to provide additional information to engineering.

### To review alerts that are awaiting evidence from engineering

1.  In the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[omblue_2](./Token/omblue_2_md.md)], in the navigation pane, click **Monitoring**, expand **Team Foundation Server Synchronization**, expand **Alerts**, and then click **Awaiting Evidence**.

### To review and close alerts that have been resolved by engineering

1.  In the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] console, you can view all application problems that have been collected. To view alerts in [!INCLUDE[omblue_2](./Token/omblue_2_md.md)], in the navigation pane, click **Monitoring**, expand **Team Foundation Server Synchronization**, expand **Alerts**, and then click **Resolved**.

2.  When you want to close the resolved alerts, you can right\-click an alert, select **Set Resolution State**, and then set the resolution state to **Closed**.


