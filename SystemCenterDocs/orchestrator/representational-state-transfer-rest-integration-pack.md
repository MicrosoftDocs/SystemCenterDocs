---
title: Representational State Transfer (REST) Integration Pack Guide for Orchestrator in System Center 2016
description: The integration pack for Representational State Transfer (REST) is an add-on for Orchestrator in System Center 2016 that enables you to create activities within runbooks that make requests to REST web services to get data or perform functions.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 69144c68-e635-408f-897f-6530e04bcd2a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Representational State Transfer (REST) Integration Pack guide for Orchestrator in System Center 2016

> Applies To: System Center 2016 - Orchestrator

The integration pack for Representational State Transfer (REST) is an add-on for Orchestrator in System Center 2016 that enables you to create activities within runbooks that make requests to REST web services to get data or perform functions.

Microsoft is committed to protecting your privacy. For more information, see the [Privacy Statement for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System requirements

The integration pack for REST requires that the following software is installed and configured before implementing the integration. For more information about installing and configuring Orchestrator, refer to the respective product documentation.

-   Orchestrator in System Center 2016

>[!WARNING]
>Depending on the communication protocol used, data that is passed to 3rd party systems could be intercepted from the wire and tampered with; for example, when the protocol between the Policy Module and the 3rd party product is HTTP. The user is responsible for choosing a secure protocol, such as HTTPS, for all data transmissions between Orchestrator and any other product.

## Downloading the integration pack

To download this integration pack, see [System Center Integration Packs](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and deploying the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and installed Runbook Designers. For the procedures on installing integration packs, see [How to add an Integration Pack](how-to-add-an-integration-pack.md).
