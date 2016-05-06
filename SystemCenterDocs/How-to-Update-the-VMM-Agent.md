---
title: How to Update the VMM Agent
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7c7266-e9f5-485c-be58-d852d543711f
---
# How to Update the VMM Agent
After you upgrade [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], use the following procedure to update the VMM agent on a virtual machine host.

### To update the VMM agent

1.  In the VMM console, open the **Fabric** workspace, expand **Servers**, and then click **All Hosts**.

2.  In the **Hosts** pane, right\-click a column heading, and then click **Agent Version Status**. This adds the **Agent Version Status** column to the **Hosts** pane.

3.  Select the host with the VMM agent that you want to update.

    > [!TIP]
    > You can use the SHIFT key or the CTRL key to select multiple hosts.

4.  On the **Hosts** tab, in the **Host** group, click **Refresh**.

    If a host needs to have its VMM agent updated, the **Host Status** column for the host will display a value of **Needs Attention**, and the **Agent Version Status** column will display a value of **Upgrade Available**.

5.  Right\-click the host with the VMM agent that you want to update, and then click **Update Agent**.

6.  In the **Update Agent** dialog box, provide the necessary credentials, and then click **OK**.

    The **Agent Version Status** column will display a value of **Upgrading**. After the VMM agent is updated successfully on the host, the **Agent Version Status** column will display a value of **Up\-to\-date**, and the **Agent Version** column will display the updated version of the agent. After you refresh the host again, the **Host Status** column for the host will display a value of **OK**.

    > [!TIP]
    > You will see **Refresh host** and **Update agent** jobs in the **Jobs** workspace.

    > [!NOTE]
    > You can update the VMM agent on a VMM library server in a similar manner. To view a list of VMM library servers, open the **Fabric** workspace, expand **Servers**, and then click **Library Servers**.

## See Also
[Performing Post-Upgrade Tasks in VMM](Performing-Post-Upgrade-Tasks-in-VMM.md)


