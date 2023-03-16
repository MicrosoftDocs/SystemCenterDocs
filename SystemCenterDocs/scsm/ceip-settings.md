---
title: Configure your preference for sharing diagnostic and usage data
description: Learn about how to configure your preference for sharing Service Manager diagnostic and usage data.
manager: mkluck
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.prod: system-center
keywords:
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 4bb2487c-5a91-44d2-9a85-f4112aff40ac
ms.custom: UpdateFrequency2
---

# Configure your preference for sharing Service Manager diagnostic and usage data

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

During setup in Service Manager, on the **Diagnostic and usage data** page, for sharing your Service Manager diagnostic and usage data with Microsoft. This feature is on by default. Administrators can turn off this feature anytime by using the choice options in Service Manager Console and Self Service Portal’s Web.config file (may also require service restart)

## Configure your preference for sharing data from the Service Manager console

1. In the Service Manager console, in the toolbar, select **Help**.

2. In the **Help** menu, select **Send diagnostic and usage data to Microsoft**

3. **Select** your diagnostic and usage data sharing preference from the dialog and select **Ok**.

## Configure your preference for sharing data from the Service Manager management server or data warehouse management server

1. Use the Service Manager console installed on same machine as Service Manager Management Server or Data Warehouse Management Server (and connect the console to same server), depending on where you want to configure the preference for sharing Service Manager diagnostic and usage data.

2. In the Service Manager console, in the toolbar, select **Help**.

3. In the **Help** menu, select **Send diagnostic and usage data to Microsoft**

4. **Select** your diagnostic and usage data sharing preference from the dialog and select **Ok**.

5. In the **Run** dialog, in the Open text field, enter **services.msc**, and select **Ok**.

6. In the **Services** window, in the **Services (Local)** pane, locate the **System Center Data Access Service**, and select **Restart**.

## Configure your preference for sharing data from the Self Service portal

1. Sign in as an **administrator** on the **IIS server**, which is hosting the **Service Manager Self Service Portal** website.

2. Open the **Web.config** file in the directory where **Service Manager Self Service Portal** is installed.

3. In **Web.config** file, find the key named **EnableTelemetry** under the XML tag **appSettings**.

4. Configure the **value** of **EnableTelemetry** key depending on your preference to share Service Manager diagnostic and usage data for Service Manager Self Service Portal. The value set as **true** for this key **enables** the sharing of diagnostic and usage data with Microsoft, and setting the value of **EnableTelemetry** key as **false**, **disables** the sharing of diagnostic and usage data with Microsoft.

5. **Save** and **Close** the **Web.config** file.

6. **Restart** the **IIS service** after you make any changes to the Web.config file.
