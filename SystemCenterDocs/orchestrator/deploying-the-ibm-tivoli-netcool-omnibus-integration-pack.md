---
title: Deploy the IBM Tivoli Netcool OMNIbus integration pack for System Center - Orchestrator
description: This article provides information about deploying the IBM Tivoli Netcool/OMNIbus integration pack for System Center - Orchestrator.
ms.date: 01/17/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.custom: intro-deployment
---

# Deploy the IBM Tivoli Netcool OMNIbus integration pack for System Center - Orchestrator

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

This article provides information about deploying the IBM Tivoli Netcool/OMNIbus integration pack for System Center - Orchestrator.

## System Requirements

The integration pack for IBM Tivoli Netcool/OMNIbus requires the following software to be installed and configured before to implementing the integration.

-   IBM Tivoli Netcool/OMNIbus 7.3 or 8.1 or 8.3
-   32-bit Java Standard Edition 7 on each runbook server and Runbook Designer using the integration pack.
    You must manually add the location of the JVM.DLL file to the PATH environment variable.
-   Sybase JConnect 6 JDBC drivers on each runbook server and Runbook Designer using the integration pack.
    You must manually copy the Jconn3.jar file to C:\\Program Files (x86)\\Common Files\\Microsoft System Center <version>\\Orchestrator\\Extensions\\Support\\NetcoolOMNIbus.


## Download the integration pack

You can download the integration pack for IBM Tivoli Netcool/OMNIbus from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54103).

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to a runbook server.

###  Register the  pack

1.  Copy the Netcool/OMNIbus integration pack file to the management server. Confirm that the file is not set to **Read Only**. This can prevent unregistering the integration pack later.

2.  From the **Start** menu, right-click **Deployment Manager**, and then click **Run as Administrator**.

3.  In the left pane of the Deployment Manager, expand **Orchestrator Management Server**, right-click **Integration Packs**, and then click **Register IP with the Orchestrator Management Server**. The Integration Pack Registration Wizard opens.

4.  Click **Next**.

5.  In the **Integration Pack or Hotfix Selection** dialog box, click **Add**.

6.  Locate and select the Netcool/OMNIbus file that you copied to the management server and click **Open**. Click **Next**.

7.  Click **Finish**. The **End User License Agreement** dialog box appears.

8.  Click **Accept**. The **Log Entries** pane displays a confirmation message when the integration pack is successfully registered.

### Deploy the pack

1.  In the left pane of Deployment Manager, right-click **Integration Packs**, and then click **Deploy IP to Runbook Server or Runbook Designer**. The Integration Pack Deployment Wizard opens.

2.  Click **Next**.

3.  Select **System Center Integration Pack for IBM Tivoli Netcool/OMNIbus** and then click **Next**.

4.  Enter the name of the computer where you want to deploy the integration pack and then click **Add**. Click **Next**.

5.  Select the **Installation Configuration** options that apply to this deployment, and then click **Next**.

6.  Click **Finish**. The **Log Entries** pane displays a confirmation message that the integration pack is successfully deployed.

## Configure the IBM Tivoli Netcool/OMNIbus connections

A connection establishes a reusable link between Orchestrator and an IBM Tivoli Netcool/OMNIbus server. You can create as many connections as you require to link to multiple servers running IBM Tivoli Netcool/OMNIbus. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.


1. In Runbook Designer, click **Options**, and then click **IBM Netcool/OMNIbus**. The **IBM Netcool/OMNIbus** dialog box appears.

2. On the **Connections** tab, click **Add** to begin the connection setup. The **Netcool/OMNIbus Connection** dialog box appears.

3. In the **Name** box, enter a name for the connection. This can be a descriptive name to distinguish the type of connection.

4. In the **Host name** box, enter the computer name or IP address of the IBM Tivoli Netcool/OMNIbus computer. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).

5. In the **Port number** box, enter the port number that you want to use. By default, this is 0. The default port used by IBM Tivoli Netcool/OMNIbus is 4100.

6. In the **User id** and **Password** boxes, enter the Orchestrator credentials to connect to the IBM Tivoli Netcool/OMNIbus server.   
   >[!NOTE]
   >The user needs to be assigned to the 'System' group to generate alerts within Netcool.

   Optionally, you can make the connection to the IBM Tivoli Netcool/OMNIbus server using a secure socket connection (SSL). To use a secure socket connection:

   1.  Select the **Use Secure Socket Layer** checkbox.
   2.  In the **Trust Store** box, enter the location of the trust store where the certificates are located.
       Enter a file name or browse for the file.
   3.  In the **Trust Store Password** box, enter the password for the protected trust store.

7. Click **Test Connection**. When the success message appears, click **OK**.

8. Add additional connections if applicable.

9. Click **OK** to close the configuration dialog box, and then click **Finish**.
