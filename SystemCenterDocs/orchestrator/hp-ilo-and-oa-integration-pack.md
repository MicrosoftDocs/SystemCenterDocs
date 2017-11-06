---
title: HP iLO and OA Integration Pack for System Center 2016 - Orchestrator
description: The Integration Pack for HP iLO and OA is an add-on for System Center 2016 - Orchestrator that enables you to automate HP iLO and OA commands.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 79e741ff-5d02-4255-8efc-19926247c1c0
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# HP iLO and OA Integration Pack for System Center 2016 - Orchestrator

The Integration Pack for HP iLO and OA is an add-on for System Center 2016 - Orchestrator that enables you to automate HP iLO and OA commands.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more information, see the [System Center Orchestrator 2016 Privacy Statement](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

The Integration Pack for HP iLO and OA requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and HP iLO and OA, refer to the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   HP iLO 2
-   HP iLO 3
-   HP OA firmware 3.31

## Downloading the Integration Pack

To download this integration pack, see [HP iLO and OA Integration Pack for System Center 2016 - Orchestrator.](https://www.microsoft.com/en-us/download/details.aspx?id=54102).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](how-to-add-an-integration-pack.md).

## Default Credentials

Default credentials are used to store a common set of credentials that can be selected when configuring a HP iLO and OA connection.

### To set up default credentials

1.  In the Runbook Designer, click the **Options** menu, and select HP iLO and OA. The HP iLO and OA dialog box appears.
2.  On the **Connections** tab, click **Default credentials** to begin the setup. The **Default credentials** dialog box appears.
3.  In the **User name** box, enter a default user name.
4.  In the **Password** box, enter a default password.
5.  In the **Key** box, enter a default key Or click the ellipsis (...) button to browse and select a Key.
6.  Click **OK** to close the default credentials dialog box.

## Configuring the HP iLO and OA Connections

A connection establishes a reusable link between Orchestrator and a HP iLO and OA system. You can create as many connections as you require to specify links to multiple systems running HP iLO and OA. You can also create multiple connections to the same system to allow for differences in security permissions for different user accounts.

### To set up a HP iLO and OA connection

1.  In the Runbook Designer, click **Options**, and then click **HP iLO and OA**. The HP iLO and OA dialog box appears.
2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Connection** dialog box appears.
3.  In the **Name** box, enter a name for the connection. This could be the name of the HP iLO and OA system or a descriptive name to distinguish the type of connection.
4.  In the **Address** box, type the name or IP address of the HP iLO and OA system. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).
5.  In the **Port** box, type the number of the HP iLO and OA system.
6.  Select **Use default credentials** to apply the default credentials to this connection. If you do this, then you can skip the next two steps.
7.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the HP iLO and OA system.
8.  In the **Private Key** box, optionally specify the SSH key used to connect to the HP iLO and OA system.
9.  In the **Attempts** box, enter the number or times a command will attempt before failing.
10. In the **Time between attempts** box, enter the number in seconds between each attempt.
11. Click **OK** to close the configuration dialog box.
12. Select the connection and click the **Test** button. **Test connection succeeded** will appear when the connection is valid. Click **Finish**.

## Exporting and Importing Connections

Connections can be exported and imported into the connections list.

### To export a connection

1.  In the Runbook Designer, click the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog box appears.
2.  On the **Connections** tab, click **Export** to begin the export. The **Save As** dialog box appears.
3.  In the **File name** box, enter a name for the export file.
4.  Click **Save** to export.
5.  Click **OK** to close the configuration dialog box and then click **Finish**.

### To import a connection

1.  In the Runbook Designer, click the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog box appears.
2.  On the **Connections** tab, click **Import** to begin the import. The **Open** dialog box appears.
3.  In the **File name** box, enter a name for the import file.
4.  Click **Open** to import.
5.  Click **OK** to close the configuration dialog box and then click **Finish**.

## Configuring the HP iLO and OA Groups

A group establishes a reusable list of connections between Orchestrator and a HP iLO and OA systems. You can create as many groups as you require to specify lists to multiple systems running HP iLO and OA.

### To set up a HP iLO and OA group

1.  In the Runbook Designer, click the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog box appears.
2.  On the **Groups** tab, click **Add** to begin the group setup. The **Managed group** dialog box appears.
3.  In the **Group name** box, enter a name for the group. This could be a descriptive name to distinguish the type of group.
4.  In the **Available** list, press the Ctrl button while clicking on the connections to select multiple connections. Press the **&gt;&gt;** button to move the connections to the **Selected** list.
5.  Click **OK** to close the configuration dialog box, and then click **Finish**.

### To batch update credentials on a group

1.  In the Runbook Designer, click the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog box appears.
2.  On the **Groups** tab, select a group and click **Batch credential update**.
3.  In the **User name** box, enter a new user name or leave blank to keep original.
4.  In the **Password** box, enter a new password or leave blank to keep original.
5.  In the **Key** box, enter a new key or leave blank to keep original.
6.  In the **Port** box, enter a new port or leave blank to keep original.
7.  Click **OK** to close the configuration dialog box, and then click **Finish**.
