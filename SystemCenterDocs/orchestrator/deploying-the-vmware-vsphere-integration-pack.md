---
title: Deploy the VMware vSphere Integration Pack for System Center - Orchestrator
description: This article provides important information about downloading and deploying the VMware vSphere integration pack for System Center - Orchestrator.
ms.date: 03/27/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: install-set-up-deploy
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: intro-deployment
---

# Deploy the VMware vSphere integration pack

The VMware vSphere Integration Pack for System Center - Orchestrator enables seamless integration, allowing for efficient orchestration of tasks and processes across VMware vSphere servers. This article provides important information about downloading and deploying the VMware vSphere integration pack for System Center - Orchestrator.

## System requirements

The pack requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and the VMware vSphere application, refer to the respective product documentation.


- VMware vSphere 5, 6, 7, and 8
- System Center - Orchestrator

## Download the pack

::: moniker range="<=sc-orch-2019"

You can download the integration pack from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54099).

::: moniker-end

::: moniker range=">=sc-orch-2022"

You can download the integration pack from the Microsoft Download Center.

::: moniker-end

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to a runbook server.

### Register the integration pack file

To register the integration pack file, follow these steps:

1. Copy the VMware vSphere integration pack file to the management server. Confirm that the file isn't set to **Read Only**. This can prevent unregistering the integration pack later.

2. From the **Start** menu, right-click **Deployment Manager**, and then select **Run as administrator**.

3. In the left pane of the Deployment Manager, expand **Orchestrator Management Server**, right-click **Integration Packs**, and then select **Register IP with the Orchestrator Management Server**. The Integration Pack Registration Wizard opens.

4. Select **Next**.

5. In the **Integration Pack or Hotfix Selection** dialog box, select **Add**.

6. Locate and select the VMware vSphere file that you copied to the management server, select **Open**, and then select **Next**.

7. In the **Completing Integration Pack Registration Wizard** dialog box, select **Finish**. The **License Agreement** dialog box appears.

8. Select **Accept**. The **Log Entries** pane displays a confirmation message when the integration pack is successfully registered.

### Deploy the integration pack file

To deploy the integration pack file, follow these steps:

1. In the left pane of Deployment Manager, right-click **Integration Packs**, and then select **Deploy IP to Runbook Server or Runbook Designer**.

2. Select **System Center Integration Pack for VMWare vSphere** and then select **Next**.

3. Enter the name of the computer where you want to deploy the integration pack, select **Add**, and then select **Next**.

4. Select the **Installation Configuration** options that apply to this deployment, and then select **Next**.

5. Select **Finish**. The **Log Entries** pane displays a confirmation message that the integration pack is successfully deployed.

## Configure the connections

A connection establishes a reusable link between Orchestrator and a VMware vSphere server. You can create as many connections as you require to link to multiple servers running VMware vSphere. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

To configure the connections, follow these steps:

1. In Runbook Designer, select **Options**, and then select **VMware vSphere**. The VMware vSphere dialog appears.

2. On the **Add Configurations** tab, select **Add** to begin the connection setup. The **Configuration** dialog appears.

3. In the **Name** box, enter a name for the connection. This can be a descriptive name to distinguish the type of connection.

4. In the **Type** list box, select **vSphere Settings**.

5. In the **Properties** box, in the **Server** line, enter the computer name or IP address of the VMware vSphere computer. For the server name, you can enter the NetBIOS name or the Fully Qualified Domain Name (FQDN).

6. In the **User** and **Password** boxes, enter the Orchestrator credentials to connect to the VMware vSphere server.

7. In the **SSL** box, enter **True** if a secure connection is required to the VMware vSphere server. Enter **False** if this is not required.

8. In the **Port** box, enter the port number that the VMware vSphere server is listening on.

9. In the **Webservice Timeout** box, enter an integer value for the number of seconds that the activities will wait for a response from the VMware vSphere server before an error is flagged.

10. Select **OK** to close the **Add Configuration** dialog box.

11. Add additional connections, if applicable.

12. Select **Finish**.

## Next steps

- Add the VMware vSphere category to the Activities pane in the Runbook Designer with [VMware vSphere Activities](vsphere-activities.md) integration pack.
