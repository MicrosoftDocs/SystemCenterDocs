---
title: Upgrading from System Center Operations Manager 2007 R2
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7595df2-2d3f-44bd-8aa3-a1a298cbb79f
---
# Upgrading from System Center Operations Manager 2007 R2
This section of the Deployment Guide provides information about how to upgrade from [!INCLUDE[om2007r2long](Token/om2007r2long_md.md)] to [!INCLUDE[om12long](Token/om12long_md.md)]. This section of the guide is not intended to be read in order, from start to finish, because your upgrade path will depend on your current configurations. You should use the [Upgrade Process Flow Diagrams](assetId:///ba32807a-01eb-472c-8e0a-f0ec5e2e30d1) or [Operations Manager for System Center 2012 Upgrade Path Checklists](assetId:///94423f24-f37e-4080-9e8a-f37f8a20d501) to help guide you through the upgrade process.

Upgrading to [!INCLUDE[om12long](Token/om12long_md.md)] is supported from [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] CU4, or from the latest available CU. Before you begin the upgrade process, make sure that all the servers in the management group meet the minimum supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)]. For more information, see [Supported Configurations for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650). If a server does not meet the minimum supported configurations, you might have to introduce new servers into your management group before you upgrade. For more information, see [Upgrading Hardware and Software to Meet System Requirements](assetId:///de668fc4-ae74-4de5-8279-7d688e43c01c).

When you run upgrade on an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group, the Upgrade wizard automatically detects the [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] features that are installed, and it lists the features that will be upgraded. For example, on an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] single\-server management group with all the features installed, the Upgrade wizard lists the operational database, management server, data warehouse, operations console, web console, and reporting. The [!INCLUDE[om12long](Token/om12long_md.md)] Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues. If any of the mandatory [!INCLUDE[om12short](Token/om12short_md.md)] features were not previously installed in the [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group, such as the data warehouse, the Upgrade wizard automatically detects the feature and adds it to the list of features to be added during the upgrade process.

In [!INCLUDE[om12long](Token/om12long_md.md)], all management servers are peers; there is no root management server \(RMS\). Therefore, the RMS is no longer a single point of failure as all management servers host the services previously hosted only by the RMS. Roles are distributed to all the management servers. If one management server becomes unavailable, its responsibilities are automatically redistributed.

If you are upgrading a distributed management group, you must upgrade certain features, such as the secondary management servers, gateways, and agents before you upgrade the management group. You run the management group upgrade from the server that hosts the RMS, unless it does not meet the minimum supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)]. For example, if the RMS is installed on a 32\-bit operating system or if it is a clustered RMS, you cannot run upgrade from the RMS. Instead, you must upgrade the management group from a secondary management server. If you follow this upgrade path, this secondary management server is marked as the RMS emulator, and the unsupported RMS is removed from the management group. The RMS emulator enables legacy management packs that rely on the RMS to continue to function in [!INCLUDE[om12long](Token/om12long_md.md)]. For more information about the supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)], see [Supported Configurations for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650).

> [!NOTE]
> If you upgrade from the secondary management server, you can build a new management server with the same Windows computer name as the old RMS, rather than change the configuration settings to point to the new management server.

There are four upgrade paths. The path you choose depends on your current topology and system configurations. The following table describes the upgrade paths in more detail.

|Upgrade Paths|Description|
|-----------------|---------------|
|Single\-server Upgrade \(Simple\)|Use this upgrade path when you have an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group where all features are installed on the same server, and the hardware and software meets the minimum supported configuration for [!INCLUDE[om12long](Token/om12long_md.md)].|
|Single\-server Upgrade \(Complex\)|Use this upgrade path when you have an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group where all features are installed on the same server, and the hardware and software do not meet the minimum supported configuration for [!INCLUDE[om12long](Token/om12long_md.md)]. If the operating system on the server is 32\-bit, a new, 64\-bit server is required.|
|Distributed Upgrade \(Simple\)|Use this path when you have an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group where various features are installed on separate servers, all of which meet the minimum supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)].|
|Distributed Upgrade \(Complex\)|Use this path when you have an [!INCLUDE[om2007r2short](Token/om2007r2short_md.md)] management group where various features are installed on separate servers, and where one or more servers do not meet the minimum supported configuration for [!INCLUDE[om12long](Token/om12long_md.md)]. For example, if the RMS is clustered, you must follow this path. If the operating system on any of the server is 32\-bit, new 64\-bit replacement servers are required.|

This guide also contains the specific pre\-upgrade and post\-upgrade procedures and checklists to help you through the upgrade process. The following content will help you upgrade to [!INCLUDE[om12long](Token/om12long_md.md)].

-   [Operations Manager for System Center 2012 Upgrade Path Checklists](assetId:///94423f24-f37e-4080-9e8a-f37f8a20d501)

-   [Upgrading Hardware and Software to Meet System Requirements](assetId:///de668fc4-ae74-4de5-8279-7d688e43c01c)

-   [Operations Manager for System Center 2012 Pre\-Upgrade Tasks](assetId:///ec2baf5f-f729-4473-873e-f40440707e48)

-   [Operations Manager for System Center 2012 Upgrade Tasks](assetId:///f31ad444-5ee5-4331-bae2-ce96daa74197)

-   [Improving Upgrade Performance](assetId:///8ca9915f-12da-4a6e-a4b7-75a38573a7a6)

-   [Upgrading a Single Server Operations Manager 2007 R2 Environment to Operations Manager for System Center 2012](assetId:///6f7406bd-8ed4-4638-94af-b2f221906aa8)

-   [Upgrading a Distributed Operations Manager 2007 R2 Environment to Operations Manager for System Center 2012](assetId:///a978b052-cd5a-4022-a688-3dd9a2635761)

-   [Completing the Post\-Upgrade Tasks](assetId:///8c2dbaf4-2966-45e3-a72d-5de90ff4f495)

## See Also
[Upgrading to Operations Manager for System Center 2012](assetId:///2c9094d2-a57f-4d77-b430-f7ee2cbede6f)


