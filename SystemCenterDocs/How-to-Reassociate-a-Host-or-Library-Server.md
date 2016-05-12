---
title: How to Reassociate a Host or Library Server
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49d7421f-39fd-4e3e-9b83-532a6594a4d7
---
# How to Reassociate a Host or Library Server
After you upgrade [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], use the following procedure to reassociate a virtual machine host with the VMM management server.

### To reassociate a host

1.  In the VMM console, open the **Fabric** workspace, expand **Servers**, and then click **All Hosts**.

2.  In the **Hosts** pane, ensure that the **Agent Status** column is displayed. If the **Agent Status** column is not displayed, right\-click a column heading, and then click **Agent Status**.

3.  Select the host that you need to reassociate with the VMM management server.

    > [!TIP]
    > You can use the SHIFT key or the CTRL key to select multiple hosts.

4.  On the **Hosts** tab, in the **Host** group, click **Refresh**.

    If a host needs to be reassociated, the **Host Status** column for the host will display a value of **Needs Attention**, and the **Agent Status** column will display a value of **Access Denied**.

5.  Right\-click the host that you want to reassociate, and then click **Reassociate**.

6.  In the **Reassociate Agent** dialog box, provide the necessary credentials, and then click **OK**.

    The **Agent Status** column will display a value of **Reassociating**. After the host has been reassociated successfully, the **Agent Status** column will display a value of **Responding**. And after you refresh the host again, the **Host Status** column for the host will display a value of **OK**.

    > [!TIP]
    > You can see a **Reassociate agent** job in the **Jobs** workspace.

7.  After you have reassociated the host, you will most likely have to update the VMM agent on the host. For more information, see [How to Update the VMM Agent](How-to-Update-the-VMM-Agent.md).

    > [!NOTE]
    > You can reassociate a VMM library server in a similar manner. To view a list of VMM library servers, open the **Fabric** workspace, expand **Servers**, and then click **Library Servers**.

## See Also
[Performing Post-Upgrade Tasks in VMM](Performing-Post-Upgrade-Tasks-in-VMM.md)


