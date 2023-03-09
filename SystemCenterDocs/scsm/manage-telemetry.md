---
ms.assetid: 3040bfd2-3b31-40e4-94f9-911641e4b8c4
title: Manage telemetry settings in Service Manager
description: This article provides information about how to manage the telemetry settings in System Center Service Manager
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 05/15/2018
ms.topic: article
ms.prod: system-center
ms.technology: service-manager
ms.custom: UpdateFrequency2
---

# Manage telemetry settings in Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

This article provides information about how to manage the telemetry (Diagnostics and utility data) settings in System Center - Service Manager (SM).

By default, SM sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time by using the Service Manager Console or self-service portal’s *Web.config file*.


> [!NOTE]
> Microsoft does not collect any personal data from the customers. We only listen to events that would help diagnostics in SM. [Learn more](#telemetry-data-collected).


## Manage telemetry settings using SM console

Use the following procedure:

1. In the SM console > toolbar, click **Help**.

2. In the **Help** menu, click **Send diagnostic and usage data to Microsoft**.

   ![console telemetry option](./media/telemetry/sm-telemetry-console.png)
3. Select the  diagnostic and usage data sharing preference from the options displayed, and click  **OK**.

   ![console telemetry selection](./media/telemetry/console-telemetry-selection.png)

## Manage telemetry settings from SM management server or data warehouse management server

> [!NOTE]
> - Use the SM console that is installed on the same computer  where the SM management server or data warehouse management server is installed.
> - You must restart the computer after you set the telemetry preference.

1. Connect the console to the server from where you want to manage the telemetry settings.

2. Follow the steps as detailed in the [above procedure](#manage-telemetry-settings-using-sm-console).

3. Once you are done with the settings, in the *Run* dialog box, type *services.msc*, and then click **OK**.
6.	In the Services window,  Services (Local) pane, locate the *System Center Data Access Service*, and click **Restart**.

## Manage telemetry settings from the self-service portal

1. Log in as administrator into the IIS server, which is hosting the SM self-service portal.
2. Open the *Web.config* file in the directory where SM self-service portal is installed.

   ![telemetry settings from self service portal](./media/telemetry/sm-telemetry-web-configfile.png)

3. In *Web.config* file, find the key  *EnableTelemetry* under the XML tag *appSettings*.

   ![edit telemetry setting](./media/telemetry/sm-telemetry-webfile-edits.png)

4. Configure the value of *EnableTelemetry* key depending on your preference.

   - To share the diagnostics and utility data with Microsoft, set the value as **true**.
   -  Set the value as **false** if you do not wish to send the data.

5. Save and close the *Web.config* file.

6. Restart the IIS service after you make any changes to the *Web.config* file.

   ![IIS service restart](./media/telemetry/telemetry-restart-iis-service.png)

## Telemetry data collected

 | Data related To | Data collected |
 | --- | --- |
 | **Censes and other settings** | Unique ID generated for the SM deployment <br /><br /> SM version <br /><br /> ID used for correlation with other System Center products <br /><br /> Default language for the installation<br /><br />Data warehouse management group ID <br /><br /> Identify that telemetry has been disabled <br /><br />Width and height of the screen|
 | **Usage** | Name of tasks used <br /><br /> Type of form used <br /><br /> Time taken to load forms <br /><br /> Name of views used <br /><br /> No. of rows fetched and loaded for each view <br /><br /> Time taken to load view <br /><br /> Cmdlets used <br /><br /> Parameters used in cmdlets <br /><br /> Time taken for execution<br /><br />Exception generated <br /><br />Reports being used<br /><br />Parameters used <br /><brTime to load reports<br /><br /> Time to load reports<br /><br />Total no. of clicks on a report<br /><br />Whether connected to the SDK service<br /><br />Whether Lync and (or) Skype is being used<br /><br />Whether Connector ECL Log is enabled or not<br /><br />Whether concurrent transactions setting is enabled or not|


## Next steps
[Manage incidents and problems](incidents-problems.md)
