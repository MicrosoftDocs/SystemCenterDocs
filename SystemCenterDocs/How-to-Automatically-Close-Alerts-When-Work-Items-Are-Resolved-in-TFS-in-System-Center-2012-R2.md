---
title: How to Automatically Close Alerts When Work Items Are Resolved in TFS in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 170d53b9-14c4-41b6-b207-a4b2760f3830
---
# How to Automatically Close Alerts When Work Items Are Resolved in TFS in System Center 2012 R2
Typically, when developers implement and verify a solution for a problem, they resolve and close the related work items in Team Foundation Server \(TFS\). However, the problem is not fully resolved on the servers until the build containing the solution is actually deployed. Information technology \(IT\) operators can close the alert in [!INCLUDE[omblue_1](Token/omblue_1_md.md)] only when the solution is deployed on the server and the system no longer generates the same type of alert. Because of this, when a work item is closed by a developer, TFS synchronization automatically marks alerts as resolved, not closed. However, you can override the default and have TFS synchronization automatically close alerts when the associated TFS work items are closed.

### To automatically close alerts when associated work items are closed

1.  In the [!INCLUDE[om12short](Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**.

2.  To set the scope of displayed rules, click **Scope** select **View all targets**, locate and select **TFS Collection**, and then click **OK**.

3.  In the list of scoped rules, right\-click **TFS Work Items Synchronization Rule**, click **Overrides**, click **Override the Rule**, and then click **For all objects of class: TFS Collection**.

4.  Add an override for parameter **Auto Close Alerts**, and set its value to **True**.

    > [!NOTE]
    > You can override this rule on a team project collection basis. To do so, when you click **Override the Rule**, override **For a specific object of class: TFS Collection**, and then select the configured TFS collections for which the associated alerts should be closed. For more information, see [How to Override a Rule or Monitor](How-to-Override-a-Rule-or-Monitor.md).

5.  Save the settings to a management pack.

## See Also
[How to Configure Integration with TFS in System Center 2012 R2](How-to-Configure-Integration-with-TFS-in-System-Center-2012-R2.md)


