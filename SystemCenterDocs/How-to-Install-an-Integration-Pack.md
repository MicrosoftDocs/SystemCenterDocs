---
title: How to Install an Integration Pack
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da3cecbb-ec12-487c-9378-db8b22193f54
---
# How to Install an Integration Pack
[!INCLUDE[orchlong](./Token/orchlong_md.md)] includes a set of standard activities that are automatically installed with [!INCLUDE[orchshort](./Token/orchshort_md.md)]. You can expand functionality and ability of [!INCLUDE[orchshort](./Token/orchshort_md.md)] to integrate platforms and products by Microsoft and other companies by installing integration packs. Each integration pack contains activities that provide unique functions. Microsoft provides integration packs for all of the System Center products, a number of other Microsoft products, and technologies and products from other companies.

Integration packs are available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkID=225843). Each integration pack has a guide that provides installation instructions, known issues, and reference information for the activities in that integration pack. To review the current integration pack guides, see [Integration Packs for System Center 2012 – Orchestrator](http://go.microsoft.com/fwlink/p/?LinkID=220929) in the TechNet Library.

The following procedures contain general instructions that apply to most integration packs. See the relevant integration pack guide for system requirements and any special installation instructions for that integration pack.

> [!IMPORTANT]
> [!INCLUDE[orchlong](./Token/orchlong_md.md)] supports integration packs designed for [!INCLUDE[orchlong](./Token/orchlong_md.md)]. Integrations packs for Opalis or pre\-release versions of [!INCLUDE[orchlong](./Token/orchlong_md.md)] are not supported.

> [!IMPORTANT]
> [!INCLUDE[orchshort](./Token/orchshort_md.md)] does not support a downgrade of integration packs. If you have an integration pack that is currently registered or previously registered in [!INCLUDE[orchshort](./Token/orchshort_md.md)], installation fails if you attempt to install an earlier version of the same integration pack. You should test integration packs and upgraded integration packs in a test environment before you implement them in a production environment. If you require a downgrade of an integration pack in a production environment, contact Microsoft Customer Support for assistance.

## Registering and deploying an integration pack
After you download the integration pack, you register the integration pack file with the [!INCLUDE[orchshort](./Token/orchshort_md.md)] management server, and then deploy it to runbook servers and computers that have the Runbook Designer installed. [!INCLUDE[crabout](./Token/crabout_md.md)] how to install a specific integration pack, see the guide for that integration pack.

When you install an upgrade of an integration pack, you must first uninstall any earlier version of the integration pack from all runbook servers and Runbook Designers. You then register and deploy the upgrade of the integration pack. If you do not uninstall the previous version of the integration pack prior to registering and deploying the upgrade version, the upgrade version will fail.

### <a name="BMK_registerintegrationpack"></a>To register an integration pack

1.  On the management server, copy the **.OIP** file for the integration pack to a local hard drive or network share.

    > [!TIP]
    > Confirm that the file is not set to **Read Only** to prevent unregistering the integration pack at a later date.

2.  Start the **Deployment Manager**.

3.  In the navigation pane of the Deployment Manager, expand **Orchestrator Management Server**, right\-click **Integration Packs** to select **Register IP with the Management Server**. The **Integration Pack Registration Wizard** opens.

4.  Click **Next**.

5.  In the **Select Integration Packs or Hotfixes** dialog box, click **Add**.

6.  Locate the **.OIP** file that you copied locally from step 1, click **Open**, and then click **Next**.

7.  In the **Completing the Integration Pack Wizard** dialog box, click **Finish**.

8.  On the **End User Agreement** dialog box, read the Microsoft Software License Terms, and then click **Accept**.

    The **Log Entries** pane displays a confirmation message when the integration pack is successfully registered.

### <a name="BMK_deployintegrationpack"></a>To deploy an integration pack

1.  In the navigation pane of **Deployment Manager**, right\-click **Integration Packs**, click **Deploy IP to Action Server or Client**.

2.  Select the integration pack that you want to deploy, and then click **Next**.

3.  Enter the name of the runbook server or computers with the Runbook Designer installed, on which you want to deploy the integration pack, click **Add**, and then click **Next**.

4.  Continue to add additional runbook servers and computers running the Runbook Designer, on which you want to deploy the integration pack. Click **Next**.

5.  In the **Installation Options** dialog box, configure the following settings.

6.  To choose a time to deploy the integration pack, select the **Schedule installation** check box, and then select the time and date from the **Perform installation** list.

7.  Click one of the following:

    -   **Stop all running runbooks before installing the integration pack**  to stop all running runbooks before deploying the integration pack.

    -   **Install the Integration Packs without stopping the running Runbooks** to install the integration pack without stopping any running runbooks.

8.  Click **Next**.

9. In the **Completing Integration Pack Deployment Wizard** dialog box, click **Finish**.

10. When the integration pack is deployed, the **Log Entries** dialog box displays a confirmation message.

    > [!WARNING]
    > If you did not configure a deployment schedule, the integration pack deploys immediately to the computers that you specified. If you configured a deployment schedule, verify that the deployment occurred by verifying the event logs after the scheduled time has passed.

#### To upgrade an integration pack

1.  On all computers that have a runbook server or Runbook Designer installed, uninstall any earlier version of the integration pack. You can achieve this by doing any one of the following:

    -   Remove it by following the instructions in [How to Uninstall and Unregister an Integration Pack](./How-to-Uninstall-and-Unregister-an-Integration-Pack.md).

    -   Log on into each computer and uninstall the integration pack from **Programs and Features** in Control Panel.

    -   On the management server, start the Deployment Manager, and then right click on the deployed integration pack for each Runbook Server or Runbook Designer computer and click **Uninstall Integration Pack or Hotfix**.

2.  Register and deploy the upgraded integration pack as described in [To register an integration pack](assetId:///722d2c22-1ea4-4dd0-be22-c662bb0d1473#BMK_registerintegrationpack) and [To deploy an integration pack](assetId:///722d2c22-1ea4-4dd0-be22-c662bb0d1473#BMK_deployintegrationpack).

## See Also
[Perform Post-Installation Tasks](./Perform-Post-Installation-Tasks.md)


