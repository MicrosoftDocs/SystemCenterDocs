---
title: How to Complete the Configuration of AlwaysOn Availability Groups for the Database
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88cfa28a-4ce7-4117-a2f4-1ed5de689dc6
---
# How to Complete the Configuration of AlwaysOn Availability Groups for the Database
If the [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] database was configured with AlwaysOn Availability Groups, after you upgrade [!INCLUDE[vmm12short](Token/vmm12short_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], you need to complete the configuration of AlwaysOn Availability Groups.

For important recommendations about AlwaysOn, see the “SQL Server and database” section of[Preparing your environment for System Center 2016 - Virtual Machine Manager](Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

### To complete the configuration of AlwaysOn Availability Groups

1.  Add the VMM database to the availability group. You can use Microsoft SQL Server Management Studio to perform this task.

2.  On the secondary node computer in the cluster that is running SQL Server, create new sign\-in account as follows:

    -   Configure the sign\-in name so that it is identical to the VMM service account name.

    -   Include user mapping to the VMM database.

    -   Configure the database owner credentials.

3.  Initiate a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service \(scvmmservice\).

4.  Repeat the last two steps for every secondary node in the cluster that is running SQL Server.

5.  If this is a high availability VMM setup, continue to install other high availability VMM nodes.

## See Also
[Performing Post-Upgrade Tasks in VMM](Performing-Post-Upgrade-Tasks-in-VMM.md)


