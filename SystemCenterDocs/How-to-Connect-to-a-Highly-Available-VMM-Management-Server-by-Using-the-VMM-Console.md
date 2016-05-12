---
title: How to Connect to a Highly Available VMM Management Server by Using the VMM Console
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dcf955f-551d-4b9b-bc35-11c82e42d841
---
# How to Connect to a Highly Available VMM Management Server by Using the VMM Console
You can use the following procedure to connect to a highly available [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] management server by using the VMM console.

To use the VMM console, you must be a member of a user role in [!INCLUDE[vmm12short](Token/vmm12short_md.md)].

### To connect to a highly available VMM management server by using the VMM console

1.  On a computer on which the VMM console is installed, on the desktop, click the **Virtual Machine Manager Console** icon.

    > [!NOTE]
    > We recommend that you install the VMM console on a different computer from the highly available VMM management server, and connect by using that VMM console. For information about installing, see [How to Install the VMM Console](How-to-Install-the-VMM-Console.md).

2.  In the **Connect to Server** dialog box, in the **Server name** box, type the clustered service name for your highly available VMM management server, followed by a colon and the connection port of your highly available VMM management server. For example, type **havmmcontoso:8100**.

    > [!IMPORTANT]
    > The clustered service name is the name entered on the **Cluster configuration** page during the installation of the highly available VMM management server. Do not enter the name of the failover cluster or the name of the computer on which the highly available VMM management server is installed.
    > 
    > When you connect by using the clustered service name, after a failover, the VMM console can reconnect automatically to the highly available VMM management server.

3.  If you want to connect using an account other than the current account, select **Specify credentials** and then enter a **User name** and **Password**.

    > [!NOTE]
    > To connect to another VMM management server the next time that you open the VMM console, clear the **Automatically connect with these settings** check box.

4.  Click **Connect**.

5.  If the **Select User Role** dialog box appears, select a user role, and then click **OK**.

    This dialog box appears only if the current user belongs to more than one user role in VMM.


