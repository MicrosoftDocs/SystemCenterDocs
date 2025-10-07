---
title: HP iLO and OA Integration Pack for System Center - Orchestrator
description: The Integration Pack for HP iLO and OA is an add-on for System Center - Orchestrator that enables you to automate HP iLO and OA commands.
ms.custom: na
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 79e741ff-5d02-4255-8efc-19926247c1c0
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 04/09/2025
---

# HP iLO and OA Integration Pack for System Center - Orchestrator


::: moniker range="sc-orch-2019"

>[!NOTE]
>HP iLO and OA Integration pack has been discontinued from System Center Orchestrator 2022 and later.

::: moniker-end

The Integration Pack for HP iLO and OA is an add-on for System Center - Orchestrator that enables you to automate HP iLO and OA commands.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

The Integration Pack for HP iLO and OA requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and HP iLO and OA, see the respective product documentation.

::: moniker range="<=sc-orch-2019"
- System Center 2016 integration packs require System Center 2016 - Orchestrator
- System Center 2019 integration packs require System Center 2019 - Orchestrator
- HP iLO 2
- HP iLO 3
- HP OA firmware 3.31
::: moniker-end

## Download the Integration Pack

::: moniker range="<=sc-orch-2019"

- To download this integration pack for Orchestrator 2016, see [HP iLO and OA Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=54102).

- To download this integration pack for Orchestrator 2019, see [HP iLO and OA Integration Pack for System Center 2019 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=58107&WT.mc_id=rss_alldownloads_all).

::: moniker-end

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](how-to-add-an-integration-pack.md).

## Default Credentials

Default credentials are used to store a common set of credentials that can be selected when configuring an HP iLO and OA connection.

### Set up default credentials

To set up default credentials, follow these steps:

1. In the Runbook Designer, select the **Options** menu, and select HP iLO and OA. The HP iLO and OA dialog appears.
2. On the **Connections** tab, select **Default credentials** to begin the setup. The **Default credentials** dialog appears.
3. In the **User name** box, enter a default user name.
4. In the **Password** box, enter a default password.
5. In the **Key** box, enter a default key or select the ellipsis (...) button to browse and select a Key.
6. Select **OK** to close the default credentials dialog.

## Configure the HP iLO and OA Connections

A connection establishes a reusable link between Orchestrator and an HP iLO and OA system. You can create as many connections as you require to specify links to multiple systems running HP iLO and OA. You can also create multiple connections to the same system to allow for differences in security permissions for different user accounts.

### Set up an HP iLO and OA connection

To set up an HP iLO and OA connection, follow these steps:

1. In the Runbook Designer, select **Options**, and select **HP iLO and OA**. The HP iLO and OA dialog appears.
2. On the **Connections** tab, select **Add** to begin the connection setup. The **Connection** dialog appears.
3. In the **Name** box, enter a name for the connection. This could be the name of the HP iLO and OA system or a descriptive name to distinguish the type of connection.
4. In the **Address** box, enter the name or IP address of the HP iLO and OA system. If you're using the computer name, you can enter the NetBIOS name or the fully qualified domain name (FQDN).
5. In the **Port** box, enter the number of the HP iLO and OA system.
6. Select **Use default credentials** to apply the default credentials to this connection. If you do this, then you can skip the next two steps.
7. In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the HP iLO and OA system.
8. In the **Private Key** box, optionally specify the SSH key used to connect to the HP iLO and OA system.
9. In the **Attempts** box, enter the number or times a command will attempt before failing.
10. In the **Time between attempts** box, enter the number in seconds between each attempt.
11. Select **OK** to close the configuration dialog.
12. Select the connection and select the **Test** button. **Test connection succeeded** will appear when the connection is valid. Select **Finish**.

## Export and Import Connections

Connections can be exported and imported into the connections list.

### Export a connection

To export a connection, follow these steps:

1. In the Runbook Designer, select the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog appears.
2. On the **Connections** tab, select **Export** to begin the export. The **Save As** dialog appears.
3. In the **File name** box, enter a name for the export file.
4. Select **Save** to export.
5. Select **OK** to close the configuration dialog and select **Finish**.

### Import a connection

To import a connection, follow these steps:

1. In the Runbook Designer, select the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog appears.
2. On the **Connections** tab, select **Import** to begin the import. The **Open** dialog appears.
3. In the **File name** box, enter a name for the import file.
4. Select **Open** to import.
5. Select **OK** to close the configuration dialog and select **Finish**.

## Configure the HP iLO and OA Groups

A group establishes a reusable list of connections between Orchestrator and an HP iLO and OA systems. You can create as many groups as you require to specify lists to multiple systems running HP iLO and OA.

### Set up an HP iLO and OA group

To set up an HP iLO and OA group, follow these steps:

1. In the Runbook Designer, select the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog appears.
2. On the **Groups** tab, select **Add** to begin the group setup. The **Managed group** dialog appears.
3. In the **Group name** box, enter a name for the group. This could be a descriptive name to distinguish the type of group.
4. In the **Available** list, press the Ctrl button while clicking on the connections to select multiple connections. Press the **&gt;&gt;** button to move the connections to the **Selected** list.
5. Select **OK** to close the configuration dialog, and select **Finish**.

### Batch update credentials on a group

To batch update credentials on a group, follow these steps:

1. In the Runbook Designer, select the **Options** menu, and select **HP iLO and OA**. The **HP iLO and OA** dialog appears.
2. On the **Groups** tab, select a group and select **Batch credential update**.
3. In the **User name** box, enter a new user name or leave blank to keep the original.
4. In the **Password** box, enter a new password or leave blank to keep the original.
5. In the **Key** box, enter a new key or leave blank to keep the original.
6. In the **Port** box, enter a new port or leave blank to keep the original.
7. Select **OK** to close the configuration dialog, and select **Finish**.