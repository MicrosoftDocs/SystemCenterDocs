---
title: How to Install a Highly Available VMM Management Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dbc92290-e10b-4a9b-9794-3dc4bc71ca25
---
# How to Install a Highly Available VMM Management Server
You can use the following procedure to install a highly available VMM management server on the first node of a cluster. To install on the other nodes of the cluster, see [How to Install a VMM Management Server on an Additional Node of a Cluster](How-to-Install-a-VMM-Management-Server-on-an-Additional-Node-of-a-Cluster.md).

Before you begin the installation of the VMM management server, review the system requirements. As part of this, ensure that you have a computer that is running a supported version of Microsoft SQL Server software. Setup will not automatically install an Express edition of SQL Server. For information on system requirements, including supported versions of SQL Server, see the following:

-   [System Requirements for System Center Technical Preview](../../system-requirements/System-Requirements-for-System-Center-Technical-Preview.md)

-   [Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

Membership in the local **Administrators** group, or equivalent, on the computer that you are configuring is the minimum required to complete this procedure.

### To install a highly available VMM management server on the first node of a cluster

1.  On the first node of your cluster, start the Virtual Machine Manager Setup Wizard for System Center 2016 Technical Preview. To start the wizard, on your installation media, right-click **setup.exe**, and then click **Run as administrator**.

    > [!NOTE]
    > Before beginning the installation of VMM, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main setup page, click **Install**.

3.  On the **Select features to install** page, select the **VMM management server** check box. The VMM console is automatically installed when you install a VMM management server.

4.  When you are prompted whether you want to make the VMM management server highly available, click **Yes**.

5.  On the **Select features to install** page, click **Next**.

6.  On the **Product registration information** page, provide the appropriate information, and then click **Next**.  If you do not enter a product key, VMM will be installed as an evaluation version that expires in 180 days after installation.

7.  On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.

8.  On the **Usage and Connectivity Data** page, select either option, and then click **Next**.

9. On the **Microsoft Update** page, select whether or not you want to use Microsoft Update, and then click **Next**.

    > [!NOTE]
    > If you have previously chosen to use Microsoft Update on this computer, the **Microsoft Update** page does not appear.

10. On the **Installation location** page, use the default path or type a different installation path for the VMM program files, and then click **Next**.

    The computer on which you are installing the highly available VMM management server will be checked to ensure that the appropriate hardware and software requirements are met. If a prerequisite is not met, a page will appear with information about which prerequisite has not been met and how to resolve the issue. If all prerequisites have been met, the **Database configuration** page will appear.

    For information about hardware and software requirements for VMM, see SQL Server Requirements for System Center vNext.

11. On the **Database configuration** page, do the following:

    -   Specify the name of the computer that is running Microsoft SQL Server. If you are installing the highly available VMM management server on the same computer that is running SQL Server (which is not recommended), in the **Server name** box, either type the name of the computer (for example, vmmserver01) or type **localhost**.

    -   Specify the port to use for communication with the computer that is running SQL Server, if all of the following conditions are true:

        -   SQL Server is running on a remote computer.

        -   The SQL Server Browser service is not started on that remote computer.

        -   SQL Server is not using the default port of 1433.

        Otherwise, leave the **Port** box empty.

    -   Select or type the name of the instance of SQL Server to use.

    -   Specify whether to create a new database or to use an existing database. If the account with which you are installing the VMM management server does not have the appropriate permissions to create a new SQL Server database, select the **Use the following credentials** check box and provide the user name and password of an account that does have the appropriate permissions.

    After you have entered this information, click **Next**.

12. On the **Cluster configuration** page, do the following:

    -   In the **Name** box, type the name you want to give to this highly available VMM management server implementation. For example, type **havmmcontoso**. Do not enter the name of the failover cluster or the name of the computer on which the highly available VMM management server is installed.

        You will use this clustered service name when you connect to this highly available VMM management server implementation by using the VMM console. Because there will be multiple nodes on the failover cluster that have the VMM management server feature installed, you need a single name to use when you connect to your VMM environment by using the VMM console.

    -   If you are using static IPv4 addresses, you must specify the IP address to assign to the clustered service name. The clustered service name and its assigned IP address will be registered in DNS. If you are using IPv6 addresses or you are using DHCP, no additional configuration is needed.

    After you have entered this information, click **Next**.

13. On the **Configure service account and distributed key management** page, do the following:

    -   Under **Virtual Machine Manager Service Account**, select **Domain account**, and then provide the name and password of the domain account that will be used by the Virtual Machine Manager service. You must use a domain account for a highly available VMM management server. For more information about using a domain account, see [Specifying a Service Account for VMM](Specifying-a-Service-Account-for-VMM.md).

    -   Under **Distributed Key Management**, specify the location in Active Directory to store encryption keys. For example, type **CN=VMMDKM,DC=contoso,DC=com**.

        You must use distributed key management to store the encryption keys in Active Directory for a highly available VMM management server. For more information about distributed key management, see [Configuring Distributed Key Management in VMM](Configuring-Distributed-Key-Management-in-VMM.md).

        After you have specified the necessary information on the **Configure service account and distributed key management** page, click **Next**.

14. On the **Port configuration** page, provide unique port numbers for each feature and that are appropriate for your environment, and then click **Next**.

    > [!IMPORTANT]
    > The ports that you assign during the VMM management server installation cannot be changed without uninstalling and reinstalling the VMM management server.

15. On the **Library configuration** page, click **Next**.

    > [!NOTE]
    > After you install VMM, you will need to add a library share. Be sure to use the **Add Default Resources** option to add Application Frameworks resources. For more information on adding a library share, see [How to add a VMM library server or VMM library share](../Manage/How-to-add-a-VMM-library-server-or-VMM-library-share.md).

16. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to install the highly available VMM management server.

    After you click **Install**, the **Installing features** page appears and installation progress is displayed.

17. On the **Setup completed successfully** page, click **Close** to finish the installation.

    To open the VMM console, ensure that the **Open the VMM console when this wizard closes** check box is selected.

    For information about connecting to a highly available VMM management server by using the VMM console, see [How to Connect to a Highly Available VMM Management Server by Using the VMM Console](How-to-Connect-to-a-Highly-Available-VMM-Management-Server-by-Using-the-VMM-Console.md).

    To install on the other nodes of the cluster, see [How to Install a VMM Management Server on an Additional Node of a Cluster](How-to-Install-a-VMM-Management-Server-on-an-Additional-Node-of-a-Cluster.md).

> [!NOTE]
> If there is a problem with setup completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.


