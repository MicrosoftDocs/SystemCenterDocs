---
title: How to Install a VMM Management Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7dd194e2-6ad7-4cea-9221-3eb3f028aa26
---
# How to Install a VMM Management Server
You can use the following procedure to install a [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] management server. For similar topics, see [Installing VMM from a Command Prompt](../Topic/Installing-VMM-from-a-Command-Prompt.md) and [Installing a Highly Available VMM Management Server](../Topic/Installing-a-Highly-Available-VMM-Management-Server.md).

Before you begin the installation of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, review the system requirements. As part of this, ensure that you have a computer that is running a supported version of Microsoft SQL Server software. Setup will not automatically install an Express edition of SQL Server. For information, see:

-   [System Requirements for System Center Technical Preview](../Topic/System-Requirements-for-System-Center-Technical-Preview.md)

-   [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

In some organizations it might be necessary to pre\-create the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database before installing [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. For more information, see [Pre-Creating the VMM Database](../Topic/Pre-Creating-the-VMM-Database.md).

To complete the installation procedures, you need, at a minimum, membership in the local Administrators group \(or equivalent\) on the computer that you are configuring.

### To install a VMM management server

1.  To start the Virtual Machine Manager Setup wizard, on your installation media, right\-click **setup.exe**, and then click **Run as administrator**.

    > [!NOTE]
    > Before you begin the installation of [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], close any open programs and ensure that no restarts are pending on the computer. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer and then log on to the computer by using the same user account to finish the installation of the server role or the security update.

2.  On the main setup page, click **Install**.

    If you have not installed the Microsoft .NET Framework, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will prompt you to install it now.

3.  On the **Select features to install** page, select the **VMM management server** check box, and then click **Next**.

    > [!NOTE]
    > The [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console is automatically installed when you install a [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server.
    > 
    > If you are installing the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server on a computer that is a member of a cluster, the wizard will ask whether you want to make the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server highly available. For more information about installing a highly available [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, see [Installing a Highly Available VMM Management Server](../Topic/Installing-a-Highly-Available-VMM-Management-Server.md).

4.  On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will be installed as an evaluation version that expires in 180 days after installation.

5.  On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.

6.  On the **Usage and Connectivity Data** page, select either option, and then click **Next**.

7.  If the **Microsoft Update** page appears, select whether you want to use Microsoft Update, and then click **Next**.

    > [!NOTE]
    > If you previously chose to use Microsoft Update on this computer, the **Microsoft Update** page does not appear.

8.  On the **Installation location** page, use the default path or type a different installation path for the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] program files, and then click **Next**.

    The setup program checks the computer on which you are installing the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server to ensure that the computer meets the appropriate hardware and software requirements. If the computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears. For information about hardware and software requirements for [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], see [System Requirements for System Center Technical Preview](../Topic/System-Requirements-for-System-Center-Technical-Preview.md).

    If the computer meets all prerequisites, the **Database configuration** page appears.

9. On the **Database configuration** page, perform one of the following sets of steps:

    -   If you are using AlwaysOn Availability Groups in SQL Server, complete the following steps:

        1.  On the **Database configuration** page, in the **Server name** box, type the name of the availability group listener.

        2.  Leave **Instance name** empty.

        3.  Create a new database.

    -   If your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database is not clustered, or is clustered but does not use AlwaysOn Availability Groups, complete the following steps:

        1.  On the **Database configuration** page, specify the name of the computer that is running SQL Server. If you are installing the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server on the same computer that is running SQL Server, then in the **Server name** box, either type the name of the computer \(for example, **vmmserver01**\) or type **localhost**. If the SQL Server is in a cluster, type the cluster name.

        2.  Ensure that the port on the computer that is running SQL Server is open. Then, specify the port that you want to use to communicate with the computer that is running SQL Server. Do not do this unless all of the following conditions are true:

            -   SQL Server is running on a remote computer.

            -   The SQL Server Browser service is not started on that remote computer.

            -   SQL Server is not using the default port of 1433.

            Otherwise, leave the **Port** box empty.

        3.  Select or type the name of the instance of SQL Server that you want to use.

        4.  Specify whether to create a new database or to use an existing database. If the account to which you are installing the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server does not have the appropriate permissions to create a new SQL Server database, select the **Use the following credentials** check box, and then provide the user name and password of an account that has the appropriate permissions.

10. Click **Next**.

11. On the **Configure service account and distributed key management** page, specify the account that the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] service will use. Realize that you cannot change the identity of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] service account after installation. For more information about which type of account to use, see [Specifying a Service Account for VMM](../Topic/Specifying-a-Service-Account-for-VMM.md).

    Under **Distributed Key Management**, select whether to store encryption keys in Active Directory Domain Services \(AD DS\). For more information about key management, see [Configuring Distributed Key Management in VMM](../Topic/Configuring-Distributed-Key-Management-in-VMM.md).

    After you select an account and, if necessary, enter AD DS information, click **Next**.

12. On the **Port configuration** page, use the default port number for each feature or provide a unique port number that is appropriate in your environment, and then click **Next**.

    > [!IMPORTANT]
    > You cannot change the ports that you assign during the installation of a [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server unless you uninstall and then reinstall the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server. Also, do not configure any feature to use port 5986, because that port number is preassigned.

13. On the **Library configuration** page, select whether to create a new library share or to use an existing library share on the computer.

    > [!NOTE]
    > The default library share that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\\ProgramData\\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it.
    > 
    > After the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server is installed, you can add library shares and library servers by using the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console or by using the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] command shell.

    After you specify a library share, click **Next**.

14. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to install the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server.

    After you click **Install**, the **Installing features** page appears and displays the installation progress.

15. On the **Setup completed successfully** page, click **Close** to finish the installation.

    To open the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, you can ensure that **Open the VMM console when this wizard closes** is checked, or you can click the **Virtual Machine Manager Console** icon on the desktop.

During Setup, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] enables the following firewall rules. These rules remain in effect even if you later uninstall [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

-   Windows Remote Management

-   Windows Standards\-Based Storage Management

> [!NOTE]
> If Setup does not finish successfully, consult the log files in the **%SYSTEMDRIVE%\\ProgramData\\VMMLogs** folder. **ProgramData** is a hidden folder.

### To configure SQL Server to use AlwaysOn Availability Groups

1.  Perform this procedure only if you are using AlwaysOn Availability Groups in SQL Server, and only after completing the previous procedure.

2.  Add the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database to the availability group.

3.  On the secondary SQL Server node, create a new logon that has the following characteristics:

    -   The login name is identical to the name of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] service account.

    -   The login has the user mapping to the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database.

    -   The login is configured with the credentials of the database owner.

4.  Initiate a failover to the secondary SQL Server node, and verify that you can restart the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] service \(scvmmservice\).

5.  Repeat the previous two steps for every secondary SQL Server node in the cluster.

6.  If this is a high\-availability [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] setup, continue to install other high\-availability [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] nodes.

