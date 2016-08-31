---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Install a VMM Management Server on an Additional Node of a Cluster
ms.technology:  virtual-machine-manager
ms.assetid:  3961bdac-8b4c-42f9-a2ce-57025adce7f7
---

# How to Install a VMM Management Server on an Additional Node of a Cluster

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedure to install a highly available Virtual Machine Manager (VMM) management server on an additional node of a failover cluster. For installing on the first node of a cluster, see [How to Install a Highly Available VMM Management Server](How-to-Install-a-Highly-Available-VMM-Management-Server.md).

> [!NOTE]
> If there is a problem with setup completing successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** folder is a hidden folder.

Membership in the local **Administrators** group, or equivalent, on the computer that you are configuring is the minimum required to complete this procedure.

### To install a highly available VMM management server on an additional node of a cluster

1.  On an additional node of your cluster, start the Virtual Machine Manager Setup Wizard. To start the wizard, on your installation media, right-click **setup.exe**, and then click **Run as administrator**.

    > [!NOTE]
    > Before beginning the installation of VMM, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main setup page, click **Install**.

3.  On the **Select features to install** page, select the **VMM management server** check box.  The VMM console is automatically installed when you install a VMM management server.

4.  When you are prompted whether you want to add this VMM management server to the existing highly VMM management server installation, click **Yes**.

5.  On the **Select features to install** page, click **Next**.

6.  On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, VMM will be installed as an evaluation version that expires in 180 days after installation.

7.  On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.

8.  On the **Usage and Connectivity Data** page, select either option and then click **Next**.

9. On the **Microsoft Update** page, select whether or not you want to use Microsoft Update, and then click **Next**.

    > [!NOTE]
    > If you have previously chosen to use Microsoft Update on this computer, the **Microsoft Update** page does not appear.

10. On the **Installation location** page, use the default path or type a different installation path for the VMM program files, and then click **Next**.

    The computer on which you are installing the highly available VMM management server will be checked to ensure that the appropriate hardware and software requirements are met. If a prerequisite is not met, a page will appear with information about which prerequisite has not been met and how to resolve the issue. If all prerequisites have been met, the **Database configuration** page will appear.

    For information about hardware and software requirements for VMM, see System Requirements for System Center vNext.

11. On the **Database configuration** page, the database server is displayed as a read-only value in the **Server name** text box. If the account you are using does not have permissions for that database, select **Use the following credentials**, and then type credentials for the database. Click **Next** to continue.

12. On the **Configure service account and distributed key management** page, provide the password of the domain account that will be used by the Virtual Machine Manager service.

13. On the **Port configuration** page, click **Next**.

14. On the **Library configuration** page, click **Next**.

15. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to install the highly available VMM management server.

    After you click **Install**, the **Installing features** page appears and installation progress is displayed.

16. On the **Setup completed successfully** page, click **Close** to finish the installation.

    To open the VMM console, ensure that the **Open the VMM console when this wizard closes** check box is selected.

    For information about connecting to a highly available VMM management server by using the VMM console, see [How to Connect to a Highly Available VMM Management Server by Using the VMM Console](How-to-Connect-to-a-Highly-Available-VMM-Management-Server-by-Using-the-VMM-Console.md).



