---
title: How to Change the Frequency of Synchronization for Integration with TFS in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5743f8fe-689b-47be-83d8-1cc357fe29a4
---
# How to Change the Frequency of Synchronization for Integration with TFS in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](./Token/sc2012sp1notetopic_md.md)]

In [!INCLUDE[sc2012sp1_short](./Token/sc2012sp1_short_md.md)], synchronizing [!INCLUDE[om12short](./Token/om12short_md.md)] alerts and work items is key to working effectively and efficiently with your development team. When you assign an alert to engineering, the matching work item in Team Foundation Server \(TFS\) will not be created immediately. The synchronization frequency is controlled by overrides in the Operations Manager TFS Work Item Synchronization management pack \(Microsoft.SystemCenter.TFSWISynchronization.mpb\). To change the synchronization frequency, you can change the overrides listed in the following table.

|Override description|Target object|Rule|Parameter|Default Value|
|------------------------|-----------------|--------|-------------|-----------------|
|How often new TFS work items are created from alerts assigned to Engineering|TFS Connector|TFS Work Items Creation Rule|Interval Seconds|300 seconds|
|How often alerts assigned to Engineering and their associated TFS work items are synchronized|TFS Collection|TFS Work Items Synchronization Rule|Interval Seconds|900 seconds|
|How often alert attachments are added from the network file share to TFS work items|TFS Collection|Attachments Synchronization Rule|Interval in Seconds|900 seconds|
|The time range of the TFS work item history that will be synchronized with the alerts. For example, the default value of 24 means that changes that are made to a TFS work item only during the past 24 hours will be synchronized. With that setting, this parameter is important if synchronization is turned off for more than 24 hours, which might create a gap in the alert history that reflects the associated TFS work item history after synchronization is turned back on. The synchronization cycle is always shorter than Delta in hours when synchronization constantly stays on. This guarantees that complete work item history is synchronized if at least one synchronization cycle has occurred during the past 24 hours.|TFS Collection|TFS Work Items Synchronization Rule|Delta in Hours|24 hours|
|How often the APM alerts will receive converted IntelliTrace logs. The value is defined in minutes.|IntelliTrace attachments for APM alerts singleton object|Add IntelliTrace as an APM attachment rule|IntelliTrace conversion data source polling interval|15 minutes|

> [!CAUTION]
> Setting the override frequencies too low might add substantial load to your management servers and TFS.

### To change the frequency of synchronization

1.  Using the table above, find the override parameter that you want to change.

2.  In the [!INCLUDE[om12short](./Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**. To set the scope of displayed rules, click **Scope**, and then select **View all targets**. Locate and select **TFS Collection** and **TFS Connector**. Click **OK**.

    > [!IMPORTANT]
    > If you are using IntelliTrace, you must also select **IntelliTrace attachments for APM alerts singleton object**.

3.  In the list of scoped rules, right\-click the rule with the parameter that you want to override. Click **Overrides**, click **Override the Rule**, and then click **For all objects of class**.

4.  Override the parameter to a new value, and save the settings to a management pack.

## See Also
[How to Override a Rule or Monitor](./How-to-Override-a-Rule-or-Monitor.md)


