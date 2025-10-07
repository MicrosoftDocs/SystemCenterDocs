---
ms.assetid: 700dd1e3-9a40-42b9-a366-92592a6be96a
title: Upgrade a Gateway Server
description: This article describes how to upgrade a Gateway server to the latest release of System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.custom: UpdateFrequency.5, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade a gateway server



After you upgrade the management servers in your management group, you upgrade any gateway servers. The procedure to upgrade is performed locally on the gateway server. You can then verify whether the upgrade is successful. Before you begin the upgrade process, ensure that your gateway server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

To upgrade a gateway server, follow these steps:

1. Sign in to a computer that hosts the gateway server with an account that's a member of the  Operations Manager Administrators role for your Operations Manager management group.

2. On the Operations Manager media, run **Setup.exe**.

3. In the **Optional Installations** section, select **Gateway management server**.

4. On the **Welcome** page, select **Next**.

5. On the **Important Notice** page, read the Microsoft Software License Terms, and select **I Agree**.

6. On the **The wizard is ready to begin gateway upgrade** page, select **Upgrade**.

7. On the **Completing Setup wizard** page, select **Finish**.

## Upgrade a gateway server from the Command Prompt

1. Sign in to a computer that's hosting the gateway server with an account that's a member of the Operations Manager Administrators role for your Operations Manager management group.

2. Open a Command Prompt window using the **Run as Administrator** option.

3. Change the directory to the Operations Manager installation media and change the directory again to gateway\AMD64, where the MOMGateway.msi file is located.

4. Run the following command where D:\ is the location for the upgrade log file.

    ```
    msiexec /i MOMgateway.msi /qn /l*v D:\logs\GatewayUpgrade.log
    AcceptEndUserLicenseAgreement=1
    ```

## Verify the gateway server upgrade

1. In the Operations console, in the navigation pane, select **Administration**.

2. Under **Device Management**, select **Management Servers**.

3. In the **Management Servers** pane, verify the value listed in the **Version** column, as per the information available in [release build versions](release-build-versions.md).

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
