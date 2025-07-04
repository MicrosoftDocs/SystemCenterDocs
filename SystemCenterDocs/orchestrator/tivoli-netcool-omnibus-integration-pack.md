---
title: IBM Tivoli Netcool OMNIbus Integration Pack for System Center - Orchestrator
description: The Integration Pack for IBM Tivoli Netcool/OMNIbus is an add-on for System Center - Orchestrator that enables you to automate responses to alerts raised within IBM Tivoli Netcool/OMNIbus.
ms.custom: na
ms.date: 11/20/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: dcdd6577-1783-4f61-9aae-dd4c590bb2e3
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# IBM Tivoli Netcool OMNIbus Integration Pack for System Center  - Orchestrator

::: moniker range="sc-orch-2019"

>[!Note]
>IBM Tivoli Netcool OMNIbus Integration pack has been discontinued from System Center Orchestrator 2022 and later.

::: moniker-end

The Integration Pack for IBM Tivoli Netcool/OMNIbus is an add-on for System Center - Orchestrator that enables you to automate responses to alerts raised within IBM Tivoli Netcool/OMNIbus. You can combine these automated responses, or activities, with the standard activities found in Orchestrator.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information, see [Privacy Statement for System Center - Orchestrator](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## Download the Integration Pack

::: moniker range="<=sc-orch-2019"
- To download this integration pack for Orchestrator 2016, see [IBM Tivoli Netcool Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=54103).
- To download this integration pack for Orchestrator 2019, see [IBM Tivoli Netcool Integration Pack for System Center 2019 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=58110&WT.mc_id=rss_alldownloads_all).
::: moniker-end

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Add an Integration Pack](how-to-add-an-integration-pack.md).

## Deploy the Integration Pack

See [Deploying IBM Tivoli Netcool Integration Pack](tivoli-netcool-omnibus-integration-pack.md).

## Known Issues

The following section contains additional information about this integration pack for IBM Tivoli Netcool/OMNIbus.

-   If the target Netcool server isn't SSL-enabled, Orchestrator can stop responding when you attempt to test the connection using SSL.
    Once you make a connection attempt, either by selecting **Test Connection** or by opening the properties of a Netcool/Omnibus activity, the initial configuration settings are used and all the subsequent changes have no effect. The JDBC drivers used to communicate with the Netcool/Omnibus ObjectServer don't recognize changes to SSL system properties once initialized.
    **Workaround:** In order to modify the **Trust store path** and **Trust store password** fields, restart the Runbook Designer.
-   When importing runbooks generated in Opalis, you need to open each Netcool activity in the Runbook Designer, and re-select the desired Connection. Enter the data again, and select **OK** to update the published data for the activity. 

> [!NOTE]
> The DateTime type properties return data with a long datestamp format.
