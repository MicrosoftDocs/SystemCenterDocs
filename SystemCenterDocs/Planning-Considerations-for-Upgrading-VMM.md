---
title: Planning Considerations for Upgrading VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b263e7f-e768-42be-bdf4-994c5e918e39
---
# Planning Considerations for Upgrading VMM
The following tables contain important planning considerations for upgrading [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] from [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)] to [!INCLUDE[sc_threshold_1](../Token/sc_threshold_1_md.md)]. For system requirements, see:

-   System Requirements for System Center vNext

-   [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

## Common planning considerations

|Item|Planning considerations|
|--------|---------------------------|
|VMware ESX hosts and unsupported versions of VMware vCenter Server|-   If you include these hosts and their managed objects in the upgrade, they are removed from the VMM database.<br />-   If you do not want these hosts to be removed automatically, remove the hosts manually before upgrading.|
|Performance and Resource Optimization \(PRO\)|-   PRO configurations are not maintained during this upgrade.<br />-   If you have a connection to Operations Manager, and you do not remove it manually before upgrade, the connection is removed automatically during the upgrade process. After the upgrade process completes, you can reconfigure your connection to Operations Manager.<br />-   For information about using Operations Manager with VMM, see [Integrating VMM and System Center Operations Manager](../Topic/Integrating-VMM-and-System-Center-Operations-Manager.md).|
|WinRM optimization|-   The values of the MaxConcurrentOperationsPerUser and the MaxConnections properties of WSMAN \(which are used by WinRM\), are not reset during the upgrade. The values that existed prior to the upgrade persist after the upgrade, and if they are too low then the throughput of VMM might be limited.|
|VMM library server|-   Review the system requirements for the VMM library server, and ensure that this server is running a supported operating system.<br />-   For information about VMM library server requirements, see[Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).|
|Service account|See [Choosing Service Account and Distributed Key Management Settings During an Upgrade](../Topic/Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).|
|Distributed key management|See [Choosing Service Account and Distributed Key Management Settings During an Upgrade](../Topic/Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).|

## High availability planning considerations

|Item|Planning considerations|
|--------|---------------------------|
|Failover cluster|-   You must create and configure a failover cluster before the upgrade. For more information, see[Create a Failover Cluster](http://technet.microsoft.com/library/dn505754.aspx).|
|Windows Azure Hyper\-V Recovery Manager Provider|If Windows Azure Hyper\-V Recovery Manager is implemented in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] environment, then after the upgrade you will need to assign the active node role to the same node that had that role before the upgrade. This ensures that the Hyper\-V Recovery Manager registration information is properly restored.|
|VMM database|-   We recommend that the VMM database reside on a high availability installation of SQL Server. We also recommend that the high availability installation of SQL Server is installed on a separate failover cluster from the failover cluster on which you are installing the high availability VMM management server.<br />-   For information about moving a VMM database to another computer, see [How to Move a VMM Database to Another Computer](../Topic/How-to-Move-a-VMM-Database-to-Another-Computer.md).|
|Library server|-   We recommend that the library server is installed on a high availability file server.<br />-   After you upgrade to a high availability VMM management server, we recommended that you relocate your VMM library to a high availability file server.<br />-   For more information about relocating your VMM library after the upgrade, see [Relocating the VMM Library](../Topic/Performing-Post-Upgrade-Tasks-in-VMM.md#BKMK_ConfigVMMLibrary).|
|Service account|-   You must configure the System Center Virtual Machine Manager service to use a domain account for a high availability VMM management server.<br />-   For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](../Topic/Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).|
|Distributed key management|-   You must use distributed key management to store encryption keys in Active Directory Domain Services \(AD DS\) for a high availability VMM management server.<br />-   For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](../Topic/Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).|

For additional guidance about configuring a high availability VMM management server, see [Installing a Highly Available VMM Management Server](../Topic/Installing-a-Highly-Available-VMM-Management-Server.md).

> [!TIP]
> VMM provides automatic rollback functionality in the event of a failure during the upgrade process. When a failure is detected during the upgrade, the upgrade automatically reverts the environment to the original configuration.

## See Also
[Planning an Upgrade of Virtual Machine Manager](../Topic/Planning-an-Upgrade-of-Virtual-Machine-Manager.md)
[Performing a VMM Upgrade](../Topic/Performing-a-VMM-Upgrade.md)
[System Requirements for System Center 2012 R2](http://technet.microsoft.com/library/dn281925.aspx)
[Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

