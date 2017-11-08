---
ms.assetid: 700dd1e3-9a40-42b9-a366-92592a6be96a
title: How to Upgrade a Gateway Server to System Center 2016 - Operations Manager
description: This article describes how to upgrade a Gateway server to Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade a gateway server to System Center 2016 - Operations Manager

After you upgrade the management servers in your management group, you upgrade any gateway servers.  The procedure to upgrade a gateway server to System Center 2016 - Operations Manager is performed locally on the gateway server. You can then verify whether the upgrade is successful. Before you begin the upgrade process, make sure that your gateway server meets the minimum supported configurations. For more information, see [System Requirements for System Center 2016 - Operations Manager](../orchestrator/system-requirements.md)

## To upgrade a gateway server

1.  Log on to a computer that hosts the gateway server with an account that is a member of the  Operations Manager Administrators role for your Operations Manager management group.

2.  On the Operations Manager media, run **Setup.exe**.

3.  In the **Optional Installations** area, click **Gateway management server**.

4.  On the **Welcome to the System Center 2016 Operations Manager Gateway Upgrade Wizard** page, click **Next**.

5.  On the **The wizard is ready to begin gateway upgrade** page, click **Upgrade**.

6.  On the **Completing the System Center 2016 - Operations Manager Gateway Setup wizard** page, click **Finish**.

## To upgrade a gateway server from the Command Prompt 

1.  Log on to a computer that is hosting the gateway server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Change the directory to the Operations Manager installation media and change directory again to gateway\AMD64, where the MOMGateway.msi file is located.

4.  Run the following command where D:\ is the location for the upgrade log file.

    ```
    msiexec /i MOMgateway.msi /qn /l*v D:\logs\GatewayUpgrade.log
    AcceptEndUserLicenseAgreement=1
    ```

## To verify the gateway server upgrade

1.  In the Operations console, in the navigation pane, click the **Administration** button.

2.  Under **Device Management**, click **Management Servers**.

3.  In the **Management Servers** pane, verify that the value listed in the **Version** column is 7.2.11469.0.


## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](deploy-upgrade-post-tasks.md).

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  

