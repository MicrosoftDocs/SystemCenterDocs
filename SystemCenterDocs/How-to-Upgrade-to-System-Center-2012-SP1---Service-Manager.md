---
title: How to Upgrade to System Center 2012 SP1 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2d73d07-01a5-4de5-9bdf-bf8c478a4298
---
# How to Upgrade to System Center 2012 SP1 - Service Manager
You can use the following procedures to upgrade your [!INCLUDE[smshort](Token/smshort_md.md)] environment to [!INCLUDE[smlong12](Token/smlong12_md.md)] SP1. These procedures include steps for upgrading the data warehouse management server, the [!INCLUDE[smshort](Token/smshort_md.md)] management server, and the [!INCLUDE[smcons](Token/smcons_md.md)].

## Data Warehouse Management Server
Use the following procedure to upgrade the data warehouse management server.

> [!IMPORTANT]
> Make sure that you have stopped the data warehouse jobs before you continue. For more information, see [How to Prepare Service Manager 2012 for Upgrade to SP1](How-to-Prepare-Service-Manager-2012-for-Upgrade-to-SP1.md).

#### To upgrade the data warehouse management server

1.  Log on to the computer that will host the data warehouse management server by using an account that is a member of the Administrators group. This account must also be a local administrator.

2.  On the [!INCLUDE[smshort](Token/smshort_md.md)] installation media, double\-click the **Setup.exe** to start the Service Manager Setup Wizard.

3.  On the **Microsoft System Center 2012** page, click **Upgrade Service Manager data warehouse management server**.

4.  On the **Prepare for upgrade** page, select the two items indicating that you have read the appropriate sections in the [!INCLUDE[smlong12](Token/smlong12_md.md)] Upgrade Guide, and then click **Next**.

5.  On the **Product registration** page, type the appropriate information in the boxes. Read the Microsoft Software License Terms; if applicable, click **I have read, understood, and agree with the terms of the license agreement**; and then click **Next**.

6.  On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configure Analysis Service for OLAP cubes** page, in the **Database server** box, type the computer name of the server that will host the SQL Server Analysis Services \(SSAS\) database, and then press the Tab key. When **Default** appears in the **SQL Server instance** box, click **Next**.

    > [!IMPORTANT]
    > If you are installing SSAS on a computer other than the computer that hosts the data warehouse management server and there is a firewall in your environment, you must make sure that the proper firewall ports are opened. For more information, see “Port Assignments for System Center 2012 \- Service Manager” in the [Planning Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672).

8.  On the **Configure Analysis Services credential** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a message saying “The credentials were accepted,” click **Next**.

9. On the **Help improve System Center** page, indicate your preference for participation in the Customer Experience Improvement Program and in Error Reporting. As an option, click **Tell me more about the program**, and then click **Next**.

10. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort](Token/smshort_md.md)] updates, and then click **Next**.

11. On the **Configuration Summary** page, read the information that is provided, and, if it is accurate, click **Install**.

12. On **The upgrade was completed successfully** page, if you have already backed up the encryption key, clear the **Open the Encryption Backup or Restore Wizard** check box, and then click **Close**.

## Service Manager Management Server
Use the following procedure to upgrade the [!INCLUDE[smshort](Token/smshort_md.md)] management server.

#### To upgrade the Service Manager management server

1.  Log on to the computer that will host the [!INCLUDE[smshort](Token/smshort_md.md)] management server by using an account that is a member of the Administrators group.

2.  On the [!INCLUDE[smshort](Token/smshort_md.md)] installation media, double\-click the **Setup.exe** to start the Service Manager Setup Wizard.

3.  On the **Microsoft System Center 2012** page, click **Upgrade Service Manager management server**.

4.  On the **Prepare for upgrade** page, select the two items indicating that you have read the appropriate sections in the Upgrade Guide for [!INCLUDE[smlong12](Token/smlong12_md.md)], and then click **Next**.

5.  On the **Product registration** page, type the appropriate information in the boxes. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

6.  On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configuration Summary** page, read the information that is provided, and, if it is accurate, click **Install**.

8.  On the **The upgrade was completed successfully** page, if you have already backed up the encryption key, clear the **Open the Encryption Backup or Restore Wizard** check box, and then click **Close**.

## Service Manager Console
Use the following procedure to upgrade the [!INCLUDE[smcons](Token/smcons_md.md)].

#### To upgrade the Service Manager Console

1.  Log on to the computer that will host the [!INCLUDE[smcons](Token/smcons_md.md)] by using an account that is a member of the Administrators group.

2.  On the [!INCLUDE[smshort](Token/smshort_md.md)] installation media, double\-click the **Setup.exe** to start the Service Manager Setup Wizard.

3.  On the **Microsoft System Center 2012** page, click **Upgrade Service Manager console**.

4.  On the **Prepare for upgrade** page, select the two items indicating that you have read the appropriate sections in the Upgrade Guide for [!INCLUDE[smlong12](Token/smlong12_md.md)], and then click **Next**.

5.  On the **Product registration** page, read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

6.  On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configuration Summary** page, read the information that is provided, and, if it is accurate, click **Install**.

8.  On **The upgrade was completed successfully** page, click **Close**.


