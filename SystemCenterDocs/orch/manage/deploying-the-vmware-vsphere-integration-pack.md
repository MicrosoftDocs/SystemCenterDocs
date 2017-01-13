---
title: Deploying the VMware vSphere Integration Pack for System Center 2016 - Orchestrator
description: The following sections provide important information about downloading and deploying the VMware vSphere integration pack for System Center 2016 - Orchestrator.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19b40fdf-c370-4534-8073-79e9b73ede6e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Deploying the VMware vSphere Integration Pack for System Center 2016 - Orchestrator

Applies To: System Center 2016 - Orchestrator

The following sections provide important information about downloading and deploying the VMware vSphere integration pack for System Center 2016 - Orchestrator.

## System Requirements

The Integration Pack for VMware vSphere requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and the VMware vSphere application, refer to the respective product documentation.

-   VMware vSphere 4.1 or 5.0
-   System Center 2016 integration packs require Orchestrator in System Center 2016

## Downloading the Integration Pack

You can download the integration pack from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=223169) (http://go.microsoft.com/fwlink/?LinkId=223169).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to a runbook server.

#### To register the integration pack

1.  Copy the VMware vSphere integration pack file to the management server. Confirm that the file is not set to **Read Only**. This can prevent unregistering the integration pack later.

2.  From the **Start** menu, right-click **Deployment Manager**, and then click **Run as administrator**.

3.  In the left pane of the Deployment Manager, expand **Orchestrator Management Server**, right-click **Integration Packs**, and then click **Register IP with the Orchestrator Management Server**. The Integration Pack Registration Wizard opens.

4.  Click **Next**.

5.  In the **Integration Pack or Hotfix Selection** dialog box, click **Add**.

6.  Locate and select the VMware vSphere file that you copied to the management server and click **Open**. Then click **Next**.

7.  In the **Completing Integration Pack Registration Wizard** dialog box, click **Finish**. The **License Agreement** dialog box appears.

8.  Click **Accept**. The **Log Entries** pane displays a confirmation message when the integration pack is successfully registered.

#### To deploy the integration pack

1.  In the left pane of Deployment Manager, right-click **Integration Packs**, and then click **Deploy IP to Runbook Server or Runbook Designer**.

2.  Select **System Center Integration Pack for VMWare vSphere** and then click **Next**.

3.  Enter the name of the computer where you want to deploy the integration pack, click **Add**, and then click **Next**.

4.  Select the **Installation Configuration** options that apply to this deployment, and then click **Next**.

5.  Click **Finish**. The **Log Entries** pane displays a confirmation message that the integration pack is successfully deployed.

## Configuring the VMware vSphere connections

A connection establishes a reusable link between Orchestrator and a VMware vSphere server. You can create as many connections as you require to link to multiple servers running VMware vSphere. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

#### To set up a VMware vSphere connection

1.  In Runbook Designer, click **Options**, and then click **VMware vSphere**. The VMware vSphere dialog appears.

2.  On the **Add Configurations** tab, click **Add** to begin the connection setup. The **Configuration** dialog appears.

3.  In the **Name** box, enter a name for the connection. This can be a descriptive name to distinguish the type of connection.

4.  In the **Type** list box, select **vSphere Settings**.

5.  In the **Properties** box, in the **Server** line, enter the computer name or IP address of the VMware vSphere computer. For the server name, you can enter the NetBIOS name or the fully qualified domain name (FQDN).

6.  In the **User** and **Password** boxes, enter the Orchestrator credentials to connect to the VMware vSphere server.

7.  In the **SSL** box, enter **True** if a secure connection is required to the VMware vSphere server. Enter **False** if this is not required.

8.  In the **Port** box, enter the port number that the VMware vSphere server is listening on.

9.  In the **Webservice Timeout** box, enter an integer value for the number of seconds that the activities will wait for a response from the VMware vSphere server before an error is flagged.

10. Click **OK** to close the **Add Configuration** dialog box.

11. Add additional connections if applicable.

12. Click **Finish**.


