---
ms.assetid: 700dd1e3-9a40-42b9-a366-92592a6be96a
title: How to Upgrade a Gateway Server
description: This article describes how to upgrade a Gateway server to System Center 1801.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/11/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1801'
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade a gateway server 

After you upgrade the management servers in your management group, you upgrade any gateway servers.  The procedure to upgrade a gateway server to the latest release of System Center Operations Manager is performed locally on the gateway server. You can then verify whether the upgrade is successful. Before you begin the upgrade process, make sure that your gateway server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](plan-system-requirements.md)

## To upgrade a gateway server

1.  Log on to a computer that hosts the gateway server with an account that is a member of the  Operations Manager Administrators role for your Operations Manager management group.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **System Center Operations Manager Upgrade** page, verify **Gateway management server** is listed as a feature requiring an upgrade, and then click **Next**.

4.  On the **Getting Started**, **Please read the license terms page** page, click **I have read, understood, and agree with license terms** and then click **Next**.

5. On the **Getting Started**, **Select installation location** page, accept the default location, or type a new location or browse to one, and then click **Next**.

6.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again**.

5.  On the **Configuration**, **Ready To Upgrade** page, click **Upgrade**.

6.  On the **Complete**, **Setup is complete** page, click **Close**.

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

3.  In the **Management Servers** pane, verify that the value listed in the **Version** column is 7.3.13142.0.


## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  

