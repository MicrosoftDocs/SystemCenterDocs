---
title: Set up secondary servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d59ad7c-5206-4cd8-878d-c0520ca96eae
---
# Set up secondary servers
The main [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server that protects data sources directly is known as the primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server. A primary server can be protected by another [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server known as the secondary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server. The secondary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server protects the databases and the replicas on the primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, and provides recovery if your primary DPM server fails. Note that a [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server can act as both a primary server protecting data sources, and as a secondary server providing protection to a primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

## Set up secondary protection
You can back up a primary DPM server using a secondary DPM server as follows:

1.  Install the DPM protection agent on each primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server that you want to protect. No restart is required.

2.  Add the primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server to an existing protection group, or create a new one.  You can select to protect the following data sources:

    -   The SQL Server databases configured for the primary server.

    -   All volumes on the primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server \(Shares will not be visible separately\)

    -   All replicas on the primary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

3.  At a minimum, you should select the databases, the \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Config folder, and the \\Program Files\\Microsoft System Center 2012\\DPM\\Scripting folder.

Note that:

-   You can’t exclude file name extensions from protection for a replica.

-   In all primary to secondary backup configurations \(chained or cyclic\) all DPM servers must be running the same operation system version, service packs, updates, DPM version, and update rollup.

-   You can select short\-term disk\-based protection and long\-term tape\-based protection, or short\-term disk\-based protection only. If you protect a replica and use short\-term disk protection only, you’ll need to specify a synchronization frequency and the option to synchronize just before a recovery point will be unavailable. We recommend you synchronize every 24 hours.

## Move protected servers
Moving protected servers between DPM servers that are under secondary protection isn’t supported. To illustrate this we have the following:

-   Server1

-   Server2

-   DPM1 acting as primary DPM server

-   DPM2 acting as another primary DPM server

-   DPM3 acting as secondary server for DPM1 and DPM2

Where:

-   Server1 is protected by DPM1

-   Server2 is protected by DPM2

-   DPM3 is a secondary server for DPM1 and DPM2 \(and thus protects Server1 and Server2.

The following occurs:

-   **Scenario 1**

    -   DPM1 fails or is removed from the infrastructure.

    -   You now want to protect Server1 with DPM2 \(with DPM3 acting as the secondary server\).

-   **Scenario 2**

    -   DPM1 fails or is removed from the infrastructure.

    -   You now want to protect Server1 with DPM3.

Both of these scenarios are unsupported. You can only select one of the following options:

-   **Option 1**—Use the “Switch Protection” option on DPM3 for Server1, and leave DPM3 in this mode going forward. Note that in this scenario you can’t add secondary protection for Server1 on another DPM server when you’re using switched protection mode.

-   **Option 2**—Rebuild DPM1 with the same name and restore the DPM database. This allows DPM to resume primary protection.

-   **Option 3**—Move protection for Server1 to a new DPM server \(DPM4\) that DPM3 doesn’t know about.

