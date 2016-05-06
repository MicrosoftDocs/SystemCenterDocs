---
title: How to Upgrade a High Availability VMM Management Server
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b507150-aaad-4883-a744-79ca6c8214a9
---
# How to Upgrade a High Availability VMM Management Server
If you are running [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] on two or more nodes of a cluster that are configured with high availability, you can use the information in this topic to upgrade the VMM management servers in the cluster to high availability VMM management servers for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]. You need to perform the following procedure on all the nodes that you want to upgrade.

Membership in the local Administrators group, or equivalent, on the computer that you are configuring is the minimum required to complete this procedure.

> [!CAUTION]
> To avoid any loss of important data, before you upgrade [!INCLUDE[vmm12short](Token/vmm12short_md.md)], we highly recommended that you perform a full backup of your VMM database.

### To prepare for a high availability upgrade

1.  Ensure that you have prepared for the upgrade as described in [Planning Considerations for Upgrading VMM](Planning-Considerations-for-Upgrading-VMM.md) and [Tasks to Perform Before Beginning the VMM Upgrade](Tasks-to-Perform-Before-Beginning-the-VMM-Upgrade.md).

2.  Uninstall [!INCLUDE[vmm12short](Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] from the nodes of the cluster that you want to upgrade, while choosing to retain the database.

3.  Upgrade the operating system to [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)] on the VMM management server. For more information, see [Planning Considerations for Upgrading VMM](Planning-Considerations-for-Upgrading-VMM.md).  Take the following steps:

    1.  Note the name of your cluster, and then destroy the cluster.

    2.  Upgrade the operating system on all the nodes that had been in the cluster. During the upgrade, choose the upgrade option, not a fresh installation, to retain data.

    3.  Recreate the cluster, using its previous name.

    For important information about hardware and software requirements, see System Requirements for System Center vNext and [Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

4.  Use the next procedure on each node that you want to upgrade, to install [!INCLUDE[vmm12short](Token/vmm12short_md.md)] for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] using the retained database.

### To upgrade to high availability VMM management server

1.  On the VMM management server, start the Virtual Machine Manager Setup Wizard for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] by double\-clicking **setup.exe** in your product media or on your network file share.

2.  On the main setup page, click **Install**.

3.  On the **Select features to install** page, select the **VMM management server** check box, and **Client** if you want to upgrade the client, and then click **Next**.

    > [!NOTE]
    > If you are installing the VMM management server on a computer that is a member of a cluster, you will be asked whether you want the VMM management server to be a high availability server. For more information about high availability VMM servers, see [Installing a Highly Available VMM Management Server](Installing-a-Highly-Available-VMM-Management-Server.md).

4.  On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] will be installed as an evaluation version that expires in 180 days after installation.

5.  On the **Please read this license agreement** page, review the license agreement, and if you agree with it, select **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

6.  On the **Join the Customer Experience Improvement Program \(CEIP\)** page, select the option of your choice, and then click **Next**.

7.  On the **Installation location** page, use the default path or type a different installation path for the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] program files, and then click **Next**.

    The computer that you are upgrading is checked to ensure that the appropriate hardware and software requirements are met. If a prerequisite is not met, a page appears with information about how to resolve the issue. If all prerequisites have been met, the **Database configuration** page appears.

    For information about hardware and software requirements, see System Requirements for System Center vNext and [Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

8.  On the **Database configuration** page, do the following:

    -   Specify the name of the computer that is running SQL Server. If you are installing the VMM management server on the same computer that is running SQL Server, in the **Server name** box, type the name of the computer \(for example, **vmmserver01**\), or type **localhost**.

        If you are upgrading a database that was configured with AlwaysOn Availability Groups, enter the name of the availability group listener.

    -   Specify the port to use for communication with the computer that is running SQL Server, if all of the following conditions are true:

        -   SQL Server is running on a remote computer.

        -   The SQL Server Browser service is not started on that remote computer.

        -   SQL Server is not using default port 1433.

        Otherwise, leave the **Port** box empty.

    -   Select or type the name of the instance of SQL Server to use. If you are upgrading a database that was configured with AlwaysOn Availability Groups, leave the text box for the instance of SQL Server empty.

    -   Select **Existing Database**, and then select the database that you backed up from your [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] installation.

    -   Check **Use the following credentials**, provide the user name and password of an account that has the appropriate permissions to access the database, and then click **Next**.

9. On the **Cluster configuration** page, do the following:

    -   In the **Name** box, type a name for this high availability VMM management server implementation. For example, type **havmmcontoso**. Do not enter the name of the failover cluster or the name of the computer on which the high availability VMM management server is installed.

        You will use this clustered service name when you connect to this high availability VMM management server implementation by using the VMM console. Because there will be multiple nodes on the failover cluster that have the VMM management server feature installed, you need a single name to use when you connect to your [!INCLUDE[vmm12short](Token/vmm12short_md.md)] environment by using the VMM console.

    -   If you are using static IPv4 addresses, you must specify the IP address to assign to the clustered service name. The clustered service name and its assigned IP address will be registered in DNS. If you are using IPv6 addresses or DHCP, no additional configuration is needed.

    After you have entered this information, click **Next**.

10. On the **Configure service account and distributed key management** page, specify the account that will be used by the System Center Virtual Machine Manager service. When you are installing a high availability VMM management server, choose a domain account.

    Under **Distributed Key Management**, select whether to store encryption keys in Active Directory Directory Services \(AD DS\). For a high availability VMM management server, choose the distributed key management option, and then click **Next**.

    > [!CAUTION]
    > Choose your service account and distributed key management settings carefully. For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).

11. On the **Port configuration** page, provide unique port numbers for each feature as appropriate for your environment, and then click **Next**.

12. On the **Library configuration** page, click **Next** to continue.

13. On the **Upgrade compatibility report**, review the information and do one of the following:

    -   Click **Cancel** to exit the upgrade and resolve the noted issues.

    -   Click **Next** to proceed with the upgrade.

14. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to upgrade the VMM management server.

    After you click **Install**, the **Installing features** page appears, and the upgrade progress is displayed.

15. On the **Setup completed successfully** page, click **Close** to finish the installation.

To open the VMM console, ensure that **Open the VMM console when this wizard closes** is selected. Alternatively, you can click the **Virtual Machine Manager Console** icon on the desktop. For information, see:

-   [How to Connect to a Highly Available VMM Management Server by Using the VMM Console](How-to-Connect-to-a-Highly-Available-VMM-Management-Server-by-Using-the-VMM-Console.md)

-   [How to Install a VMM Management Server on an Additional Node of a Cluster](How-to-Install-a-VMM-Management-Server-on-an-Additional-Node-of-a-Cluster.md)

After the upgrade, see [Performing Post-Upgrade Tasks in VMM](Performing-Post-Upgrade-Tasks-in-VMM.md).


