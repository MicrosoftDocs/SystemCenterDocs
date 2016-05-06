---
title: Backup methods for the DPM server
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 360cc097-6b84-4558-89bc-6d188db61963
---
# Backup methods for the DPM server
In order to ensure that data can be recovered if the [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)] server fails you need to put together a backup and recovery strategy for your DPM servers. If the DPM server isn’t backed up you’ll need to rebuild it manually after a failure, and disk\-based recovery points won’t be recoverable. You can back up DPM servers using a couple of methods.

-   **[Back up DPM using a secondary server](./Back-up-DPM-using-a-secondary-server.md)**—You can back up a primary DPM server with a secondary DPM server. The secondary server will protect the primary server database and the data source replicas stored on the primary server. If the primary server fails, the secondary server can continue to protect workloads that are protected by the primary server, until the primary server is available again. If you need to rebuild the primary server you can restore the databases and replicas to it from the secondary server. You can also restore data to protected computers directly from the secondary server when the primary server isn’t available. You can set up two servers, one as primary and the another as secondary, or configure each server to act as the primary for the other. You can also configure a chain of DPM servers that protect each other according to the chain order.

-   **[Backup methods for the DPM database](./Backup-methods-for-the-DPM-database.md)**—You can configure a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server to back up its own databases to its tape library, or you can use non\-Microsoft software to back up the databases to tape or removable media.

-   **[Back up DPM using third-party software](./Back-up-DPM-using-third-party-software.md)**—You can back up DPM servers using third\-party software that supports DPM and VSS.


