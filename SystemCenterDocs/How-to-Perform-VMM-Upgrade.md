---
title: How to Perform VMM Upgrade
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 961fde38-eec5-43f5-976c-69d9f95780f2
---
# How to Perform VMM Upgrade
Use the following procedure to upgrade a [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] management server to [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]. During this procedure, you retain the data from the [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] database.

Membership in the local Administrators group, or equivalent, on the computer that you are configuring is the minimum required to complete this procedure.

> [!CAUTION]
> To avoid any loss of important data, before you upgrade [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], we highly recommend that you perform a full backup of your VMM database.

### To upgrade a VMM management server

1.  Ensure that you have prepared for the upgrade as described in [Planning Considerations for Upgrading VMM](./Planning-Considerations-for-Upgrading-VMM.md) and [Tasks to Perform Before Beginning the VMM Upgrade](./Tasks-to-Perform-Before-Beginning-the-VMM-Upgrade.md).

2.  On the current VMM management server in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)], start the Microsoft [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)] Virtual Machine Manager Setup Wizard by double\-clicking **setup.exe** in your product media or on your network file share.

3.  On the main setup page, click **Install**.

4.  On the **Select features to install** page, select the **VMM management server** check box, and **Client** if you want to upgrade the client, and then click **Next**.

    > [!NOTE]
    > If you are installing the VMM management server on a computer that is a member of a cluster, you will be asked whether you want the VMM management server to be a high availability server. For background information, see [Installing a Highly Available VMM Management Server](./Installing-a-Highly-Available-VMM-Management-Server.md).

5.  On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] will be installed as an evaluation version that expires in 180 days after installation.

6.  On the **Please read this license agreement** page, review the license agreement, and if you agree with it, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.

7.  On the **Join the Customer Experience Improvement Program \(CEIP\)** page, select the option of your choice, and then click **Next**.

8.  On the **Installation location** page, use the default path or type a different installation path for the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] program files, and then click **Next**.

    The computer that you are upgrading is checked to ensure that the appropriate hardware and software requirements are met. If a prerequisite is not met, a page appears with information about which prerequisite has not been met and how to resolve the issue. If all prerequisites have been met, the **Database configuration** page appears.

    For information about hardware and software requirements for [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], see System Requirements for System Center vNext and see[Preparing your environment for System Center 2016 - Virtual Machine Manager](./Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

9. On the **Database configuration** page, do the following:

    -   Specify the name of the computer that is running SQL Server. If you are installing the VMM management server on the same computer that is running SQL Server, in the **Server name** box, type the name of the computer \(for example, **vmmserver01**\), or type **localhost**.

        If you are upgrading a database that was configured with AlwaysOn Availability Groups, enter the name of the availability group listener.

    -   Specify the port to use for communication with the computer that is running SQL Server, if all of the following conditions are true:

        -   SQL Server is running on a remote computer.

        -   The SQL Server Browser service is not started on that remote computer.

        -   SQL Server is not using default port 1433.

        Otherwise, leave the **Port** box empty.

    -   Select or type the name of the instance of SQL Server to use. If you are upgrading a database that was configured with AlwaysOn Availability Groups, leave the text box for the instance of SQL Server empty.

    -   Select **Existing Database**, and then select the database that you backed up from your [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] installation.

    -   Check **Use the following credentials**, provide the user name and password of an account that has the appropriate permissions to access the database, and then click **Next**.

10. When you are prompted whether to upgrade the database that you specified, click **Yes**.

11. On the **Configure service account and distributed key management** page, specify the account that will be used by the System Center Virtual Machine Manager service.

    Under **Distributed Key Management**, select whether to store encryption keys in Active Directory Domain Services, and then click **Next**.

    > [!CAUTION]
    > Choose your service account and distributed key management settings carefully. Depending on what you choose, encrypted data, like passwords in templates and profiles, may not be available after the upgrade, and you will have to re\-enter them manually. For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](./Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).

12. On the **Port configuration** page, provide unique port numbers for each feature as appropriate for your environment, and then click **Next**.

13. On the **Library configuration** page, chose whether to use an existing library share, or to create a new one, and then enter the library configuration information.

14. On the **Upgrade compatibility report**, review the information and do one of the following:

    -   Click **Cancel** to exit the upgrade and resolve the noted issues.

    -   Click **Next** to proceed with upgrade.

15. On the **Installation summary** page, review your selections and do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to upgrade the VMM management server.

    After you click **Install**, the **Installing features** page appears and the upgrade progress is displayed.

16. On the **Setup completed successfully** page, click **Close** to finish the installation.

    To open the VMM console, ensure that the **Open the VMM console when this wizard closes** check box is selected. Alternatively, you can click the **Virtual Machine Manager Console** icon on the desktop.

After the upgrade, see [Performing Post-Upgrade Tasks in VMM](./Performing-Post-Upgrade-Tasks-in-VMM.md).

## See Also
[Performing a VMM Upgrade](./Performing-a-VMM-Upgrade.md)


