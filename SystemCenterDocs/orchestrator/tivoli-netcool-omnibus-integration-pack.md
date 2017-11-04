---
title: IBM Tivoli Netcool OMNIbus Integration Pack for System Center 2016 - Orchestrator
description: The Integration Pack for IBM Tivoli Netcool/OMNIbus is an add-on for System Center 2016 - Orchestrator that enables you to automate responses to alerts raised within IBM Tivoli Netcool/OMNIbus.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dcdd6577-1783-4f61-9aae-dd4c590bb2e3
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# IBM Tivoli Netcool OMNIbus Integration Pack for System Center 2016 - Orchestrator

The Integration Pack for IBM Tivoli Netcool/OMNIbus is an add-on for System Center 2016 - Orchestrator that enables you to automate responses to alerts raised within IBM Tivoli Netcool/OMNIbus. You can combine these automated responses, or activities, with the standard activities found in Orchestrator.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more information, see [Privacy Statement for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## Downloading the Integration Pack

To download this integration pack, see [IBM Tivoli Netcool Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=54103).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Deploying the Integration Pack
See [Deploying IBM Tivoli Netcool Integration Pack](tivoli-netcool-omnibus-integration-pack.md)

## Known Issues

The following section contains additional information about this integration pack for IBM Tivoli Netcool/OMNIbus.

-   If the target Netcool server is not SSL-enabled, Orchestrator can stop responding when you attempt to test the connection using SSL.
    Once you make a connection attempt, either by clicking **Test Connection** or by opening the properties of a Netcool/Omnibus activity, the initial configuration settings are used and all subsequent changes have no effect. The JDBC drivers used to communicate with the Netcool/Omnibus ObjectServer do not recognize changes to SSL system properties once initialized.
    **Workaround:** In order to modify the **Trust store path** and **Trust store password** fields, restart the Runbook Designer.
-   When importing runbooks generated in Opalis, you need to open each Netcool activity in the Runbook Designer, and re-select the desired Connection. Enter the data again, and then click **OK** to update the published data for the activity. Note that the DateTime type properties return data with a long datestamp format.
