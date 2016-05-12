---
title: How to Stop and Resume Synchronization with TFS in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81bed899-8a60-45ff-b2b8-d6d9f0daf3ff
---
# How to Stop and Resume Synchronization with TFS in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](Token/sc2012sp1notetopic_md.md)]

Sometimes you might need to temporarily stop synchronization in [!INCLUDE[om12short](Token/om12short_md.md)] in [!INCLUDE[sc2012sp1_long](Token/sc2012sp1_long_md.md)] with Team Foundation Server \(TFS\). For example, this may be necessary when a team project collection is unavailable because of maintenance, during maintenance of management servers in the synchronization management pool, or when you are changing synchronization settings to prevent inconsistent synchronization while new settings are applied. When you know synchronization is not working, turning off synchronization keeps unnecessary alerts about synchronization not working from being generated.

If you need to stop synchronization permanently, you can delete the TFS Work Item Synchronization template for the team project collection that you no longer want to use.

Use the following procedure to temporarily stop synchronization without deleting configuration settings. Use the next procedure to resume synchronization.

> [!TIP]
> To restart synchronization, you can restart System Center Management service on all management servers in the synchronization pool.

### To temporarily stop synchronization without deleting configuration settings

1.  To control synchronization, the system uses three independent rules:

    -   The TFS Work Items Synchronization Rule

    -   The Attachments Synchronization Rule

    -   The TFS Work Items Creation Rule

    To temporarily stop synchronization, you must disable all three of these rules. For more information, see [How to Override a Rule or Monitor](How-to-Override-a-Rule-or-Monitor.md).

    In the [!INCLUDE[om12short](Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**. To scope the displayed rules, click **Scope**, and then click **View all targets**. Look for and then select the **TFS Collection** and **TFS Connector** targets. Click **OK**.

2.  To disable the TFS Work Items Synchronization Rule:

    1.  In the list of scoped rules, expand **TFS Collection**, right\-click **TFS Work Items Synchronization Rule**, click **Overrides**, click **Disable the Rule**, and then click **For all objects of class: TFS Collection**.

    2.  On the **Override Properties** page, override the **Enabled** parameter to **False**, and then save your settings to a management pack.

3.  To disable the Attachment Synchronization Rule:

    1.  In the list of scoped rules, expand **TFS Collection**, right\-click **Attachments Synchronization Rule**, click **Overrides**, click **Disable the Rule**, and then click **For all objects of class: TFS Collection**.

    2.  On the **Override Properties** page, override the **Enabled** parameter to **False**, and then save your settings to a management pack.

4.  To disable the TFS Work Items Creation Rule:

    1.  In the list of scoped rules, expand **TFS Connector**, right\-click **TFS Work Items Creation Rule**, click **Overrides**, click **Disable the Rule**, and then click **For all objects of class: TFS Connector**.

    2.  On the **Overrides Properties** page, override the **Enabled** parameter to **False**, and then save your settings to a management pack.

### To resume synchronization

1.  To control synchronization, the system uses three independent rules:

    -   The TFS Work Items Synchronization Rule

    -   The Attachments Synchronization Rule

    -   The TFS Work Items Creation Rule

    To resume synchronization, you must re\-enable all three of these rules. For more information about override settings, see [How to Override a Rule or Monitor](How-to-Override-a-Rule-or-Monitor.md).

2.  In the [!INCLUDE[om12short](Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**. To scope the displayed rules, click **Scope**, and then select **View all targets**. Look for and then select the **TFS Collection** and **TFS Connector** targets. Click **OK**.

3.  To enable the TFS Work Items Synchronization Rule:

    In the list of scoped rules, expand **TFS Collection**, right\-click **TFS Work Items Synchronization Rule**, click **Override Summary**, click the **Enabled** parameter for class TFS Collection, and then click **Delete**. Click **Close**.

4.  To enable the Attachments Synchronization Rule:

    In the list of scoped rules, expand **TFS Collection**, right\-click **Attachments Synchronization Rule**, click **Override Summary**, click the **Enabled** parameter for class TFS Collection, and then click **Delete**. Click **Close**.

5.  To enable the TFS Work Items Creation Rule:

    In the list of scoped rules, expand **TFS Connector**, right\-click **TFS Work Items Creation Rule**, click **Override Summary**, click the **Enabled** parameter for class TFS Connector, and then click **Delete**. Click **Close**.

## See Also
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[How to Change the Frequency of Synchronization for Integration with TFS in System Center 2012 SP1](How-to-Change-the-Frequency-of-Synchronization-for-Integration-with-TFS-in-System-Center-2012-SP1.md)


