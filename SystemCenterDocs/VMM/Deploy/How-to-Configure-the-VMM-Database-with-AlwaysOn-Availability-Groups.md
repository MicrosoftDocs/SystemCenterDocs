---
title: How to Configure the VMM Database with AlwaysOn Availability Groups
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2c3d79d-2dc9-4a4e-a27d-1ecae7e2ce53
---
# How to Configure the VMM Database with AlwaysOn Availability Groups
In [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)], you can take advantage of AlwaysOn Availability Groups in Microsoft SQL Server 2012 or Microsoft SQL Server 2014 to ensure high availability of the VMM database. However, be sure to review the recommendations for Availability Groups in the “SQL Server and database” section of [Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

If you have not configured Availability Groups during the initial configuration, you can use the following procedure to perform that configuration.

Perform the following procedure on the SQL Server cluster that hosts the VMM database.

### To configure the VMM database with AlwaysOn Availability Groups

1.  If the VMM database is included in the availability group, remove it. You can use the Microsoft SQL Management Studio tool to perform this task.

2.  Initiate a failover to the computer that is running SQL Server and on which the VMM database is installed.

3.  On the VMM management server, start the Virtual Machine Manager Setup Wizard. To start the wizard, on your installation media, right\-click **setup.exe**, and then click **Run as administrator**.

4.  Skip the first five wizard pages, and then on the **Database configuration** page do as follows:

    1.  In the **Server name** box, type the name of the availability group listener.

    2.  Leave **Instance name** empty.

    3.  Select the existing VMM database.

    4.  Complete the setup wizard.

5.  On the secondary node computer in the cluster that is running SQL Server, create a new login with the following characteristics:

    -   The login name is identical to the VMM service account name.

    -   The login has the user mapping to the VMM database.

    -   The login is configured with the database owner credentials.

6.  Initiate a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service \(scvmmservice\).

7.  Repeat the last two steps for every secondary node in the cluster that is running SQL Server.

8.  If this is a high availability VMM setup, continue to install other high availability VMM nodes.


