---
title: VMware vSphere integration pack for System Center - Orchestrator
description: This article describes the integration pack for VMware vSphere in System Center - Orchestrator.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.date: 11/19/2024
---
# VMware vSphere integration pack

The integration pack for VMware vSphere is an add-on for System Center - Orchestrator. It assists you in automating actions in VMware vSphere, enabling full management of your virtualized computing infrastructure.

[Learn more](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx) about privacy in Orchestrator.

## Download the pack

::: moniker range="<=sc-orch-2019"
- Download the pack for Orchestrator 2016 from [here, on the download center](https://www.microsoft.com//download/details.aspx?id=54099).

- Download the pack for Orchestrator 2019 from [here, on the download center](https://www.microsoft.com/download/details.aspx?id=58112&WT.mc_id=rss_alldownloads_all).
::: moniker-end

::: moniker range="sc-orch-2022"

- Download the pack for Orchestrator 2022 from [here, on the download center](https://www.microsoft.com/download/details.aspx?id=106163).

::: moniker-end

::: moniker range="sc-orch-2025"

VMware vSphere Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the VMware vSphere Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=106163).

::: moniker-end

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to Runbook servers and Runbook Designers. For procedures on installing integration packs, see [How To Add an Integration Pack](how-to-add-an-integration-pack.md).

## Deploy the Integration Pack

Learn about [deploying the VMware VSphere Integration Pack](/system-center/orchestrator/deploying-the-vmware-vsphere-integration-pack).

## Known issues

You might see the following issues when using this VMware vSphere integration pack.

- The Set VM Networks activity supports VMs with a maximum of four network adapters. If you use this activity on a VM with more than four adapters, you see an **Index was out of range** error.
- The Reconfigure VM activity provides an options list for the number of CPUs ranging from 1 to 4, even if the vSphere server supports VMs with more than 4 CPUs. To work around this limitation, you can enter a valid number in the field manually.
- In the Add Network Adapter activity, you can manually enter any **Network** label for the adapter. This network will be applied to the adapter in vSphere even if it's unavailable or doesn't exist.
- The Create VM activity doesn't provide an option to browse for valid networks for each of the NIC properties.
- In the Reconfigure VM activity, the return values of **After Power On Script**, **After Resume Script**, **Before Guest Standby Script**, and **Before Guest Standby Script** don't match the input values supplied.
- The Add VM Disk activity doesn't provide the option to browse for available data stores.
- The Set VM CD/DVD to ISO Image activity can be supplied with a **Relative File Path** to a nonexistent file. The activity completes successfully rather than producing an error message.
- The Clone Windows VM and Clone Linux VM activities don't filter unavailable resource pools from the **Resource Pool Path** browser.
- The Clone Windows VM and Clone Linux VM activities don't filter source VMs based on their guest operating system.
- If you inadvertently import the Opalis global configurations, you might see the following errors:
  -   When adding or editing configurations:

      Failed to load the assembly containing the service class

  -   When editing the properties of any vSphere activity:

      Failed to load the assembly containing the service class

      Runtime Error! ...
      This application has requested the Runtime to terminate it in an unusual way. Contact the application's support team for more information.

- If you attempt to start a VM that is already powered on by using the Start VM activity, supplying a Timeout value of greater than 2,147,483 will cause the integration pack to report success even though the vSphere server indicates that the VM can't be started.
- Exporting workflows that contain vSphere activities from Opalis Integration Server 6.3 and importing them into Orchestrator corrupts vSphere configurations stored in Orchestrator. To address this issue, omit the global configurations from the import process, and then manually create the matching configurations in Orchestrator.
  **Workaround:** Use the following steps when exporting and importing Opalis workflows.

  >[!WARNING]
  >It's highly recommended that you perform a full backup of the Orchestrator database before importing runbooks. Importing global configurations from another system can overwrite local changes or leave the Orchestrator database in an unstable state. If the Runbook Designer or runbook server exhibit problems after performing a runbook import, restore the Orchestrator database from the backup.

  **Stage 1: Export the Opalis workflows and import them into Orchestrator.**

  1.  Export the workflows from Opalis Integration Server Client using the conventional method. No changes to this process are required.
  2.  In the Orchestrator Runbook Designer, import the runbooks to the appropriate location using the **Import** option from the folder context menu or the **Actions** item from the main menu.
  3.  In the **Import** dialog, select the file the location of the .ois\_export file.
  4.  Configure the options under **Import the following global settings** as necessary for your runbooks.
  5.  Ensure that the **Import global configurations** checkbox isn't checked. This prevents Opalis global configurations from being imported into Orchestrator.
  6.  Select **Finish**.

  **Stage 2: After the workflows are imported, create new vSphere configurations:**

  1.  Record the details of the vSphere configuration settings used by the exported workflows from the source Opalis 6.3 system. These can be found in the **Options -&gt; VMware vSphere** item in the main menu of the Opalis Integration server client.
      Note the **Name**, **Server**, **User**, **Password**, and **SSL** property values for each vSphere configuration. The **Name** of the configuration is case-sensitive.
  2.  In the Orchestrator Runbook Designer, create a new vSphere configuration for each configuration used by the imported runbooks.
      1.  Select **Options**, and select **VMware vSphere** to open the **Prerequisite Configuration** window.
      2.  Select **Add** to add a new configuration.
      3.  Enter the name for the configuration as it appeared in the Opalis 6.3 system. The **Name** field is case-sensitive.
      4.  Select the configuration **Type** of **vSphere Setting**.
      5.  Enter the **Server**, **User**, **Password**, and **SSL** property values as recorded from the Opalis 6.3 system.
          The **Port** and **Webservice Timeout** settings can be left blank at this stage.
      6.  Select **OK** to save your changes and create a new configuration.

  3.  Repeat step 2 for all the configurations used by the imported runbooks.
  4.  When you've created all the configurations used by the imported runbooks, select **Finish** on the **Prerequisite Configurations** window.
  5.  Test that the imported runbooks run successfully.
- The activity Get Resource Pool Runtime Info fails with an empty Resource Pool (without any VMs under it). The error summary is **StartIndex cannot be less than zero. Parameter name: startIndex.**
- When selecting a vSphere activity in the Runbook Tester, the following error may appear:
  "Error
  Details: password
  Exception: IntegrationPackException
  Target site: ServiceBase.Design"
  This message can be safely ignored; however, the options list of various properties won't be automatically populated in the Runbook Tester. If required, the value of these properties may be edited manually.
