---
title: How to Connect to a VMM Management Server by Using the VMM Console
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afe4c02a-6698-4cfb-9f2b-ec42adf70549
---
# How to Connect to a VMM Management Server by Using the VMM Console
You can use the following procedure to use the [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] console to connect to a VMM management server.

To use the VMM console, you must be a member of a user role in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

### To connect to a VMM management server by using the VMM console

1.  On a computer on which the VMM console is installed, on the desktop, click the **Virtual Machine Manager Console** icon.

2.  In the **Connect to Server** dialog box, do one of the following:

    -   If the VMM console is on the VMM management server that you want to connect to, and the **Server name** box contains **localhost** and the port of the VMM management server, leave these entries unchanged.

        The default port setting is 8100.

    -   To use the VMM console to connect to a VMM management server on a different computer, in the **Server name** box, type the name of that computer, followed by a colon and the connection port of that VMM management server, for example:

        **vmmserver01:8100**

3.  If you want to connect using an account other than the current account, select **Specify credentials** and then enter a **User name** and **Password**.

    > [!NOTE]
    > To connect to another VMM management server the next time that you open the VMM console, clear the **Automatically connect with these settings** check box.

4.  Click **Connect**.

5.  If the **Select User Role** dialog box appears, select a user role, and then click **OK**.

    This dialog box appears only if the current user belongs to more than one user role in VMM.

