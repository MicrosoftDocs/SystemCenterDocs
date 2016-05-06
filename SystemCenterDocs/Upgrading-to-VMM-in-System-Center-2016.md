---
title: Upgrading to VMM in System Center 2016
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b78e57a0-9890-44b6-8590-f21a9b701713
---
# Upgrading to VMM in System Center 2016
If you have an existing deployment of [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)], you can upgrade [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] to [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]. This upgrade is basically a fresh installation of [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)], but it retains the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database from the [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] deployment.

> [!CAUTION]
> If you are upgrading two or more System Center components, you must follow the procedures that are documented in the topic[Upgrade Sequencing for System Center 2012 R2](http://technet.microsoft.com/library/dn521010.aspx).

The order in which you perform component upgrades is very important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:

1.  [!INCLUDE[orchshort](./Token/orchshort_md.md)]

2.  [!INCLUDE[smshort12](./Token/smshort12_md.md)]

3.  [!INCLUDE[dpm2012sp1long](./Token/dpm2012sp1long_md.md)]

4.  [!INCLUDE[om12short](./Token/om12short_md.md)]

5.  [!INCLUDE[cmshort](./Token/cmshort_md.md)]

6.  [!INCLUDE[vmm12sp1_med](./Token/vmm12sp1_med_md.md)]

7.  [!INCLUDE[conceroshort](./Token/conceroshort_md.md)]

**Retaining encrypted data**

Some data in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database, such as the Run As account credentials and passwords in guest operating system profiles, are encrypted by using Windows Data Protection API \(DPAPI\). To retain encrypted data when you perform your upgrade, review the following:

-   **Management server** The [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server must be installed on the same computer where [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] was previously installed, unless distributed key management was used.

-   **Service account** You must use the same System Center Virtual Machine Manager service account that you used in your previous installation of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

-   **Installation server** You can install [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)] on the same server where [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] is currently installed, or on a different server. However, if you install [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] on a different computer, or if you use a different service account, the encrypted data is not retained unless you configured distributed key management.

> [!NOTE]
> Distributed key management stores the encryption keys in Active Directory Domain Services \(AD DS\). Later, when you move your [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] installation to another computer, the new computer has access to the encryption keys in AD DS.

The following topics provide information to help you with this upgrade:

-   [Planning an Upgrade of Virtual Machine Manager](./Planning-an-Upgrade-of-Virtual-Machine-Manager.md)

-   [Performing a VMM Upgrade](./Performing-a-VMM-Upgrade.md)

-   [Performing Post-Upgrade Tasks in VMM](./Performing-Post-Upgrade-Tasks-in-VMM.md)

-   [Troubleshooting a VMM Upgrade](./Troubleshooting-a-VMM-Upgrade.md)

For information about performing a new [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] installation rather than an upgrade, see [Deploying System Center 2016 - Virtual Machine Manager](./Deploying-System-Center-2016---Virtual-Machine-Manager.md).

## Known issues with this upgrade
The following issues have been identified when upgrading [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] to [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]:

### Upgrading on a remote computer
Upgrading from [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] on one computer to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)] on a different computer is not supported when data is retained from the original installation, and the following configurations apply:

-   The original installation uses Windows DPAPI. This is the default setting if you did not configure distributed key management during setup.

-   The [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server is configured to use any of the following encrypted values or settings:

    -   Application settings \(encrypted value\)

    -   Service setting \(encrypted value\)

    -   SQL Server deployment \(product key\)

    -   Web deploy package \(encryption password\)

### VMM library name and path
To ensure that data retained from [!INCLUDE[sc2012r2_1](./Token/sc2012r2_1_md.md)] upgrades as expected, and to avoid an error message about the name and path of the shared library, do one of the following on the Library configuration page of the Setup Wizard when you install [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]:

-   Select the default shared library.

-   Create a new library share.

### WSMAN property values are not reset
The values of the MaxConcurrentOperationsPerUser and the MaxConnections properties of WSMAN \(which are used by WinRM\) are not reset during the upgrade. The values that existed before the upgrade persist after the upgrade, and they might be lower than the default values that are set by the operating system.

If you observe limited VMM throughput, it might be helpful to check these values and to reset them if needed.


