---
title: Representational State Transfer (REST) integration pack for System Center - Orchestrator
description: This article describes the REST integration pack for System Center - Orchestrator.
ms.date: 11/19/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: engagement-fy24
---

# REST integration pack guide

The integration pack for Representational State Transfer (REST) is an add-on for System Center - Orchestrator that enables you to create activities within runbooks that make requests to REST web services to get data or perform functions.

- Microsoft is committed to protecting your privacy. See our [privacy statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).
- Depending on the communication protocol used, data that's passed to third party systems could be intercepted from the wire and tampered with; for example, when the protocol between the Policy Module and the third party product is HTTP. The user is responsible for choosing a secure protocol, such as HTTPS, for all data transmissions between Orchestrator and any other product.

## Download the integration pack

::: moniker range="<=sc-orch-2019"
- To download this integration pack for Orchestrator 2016, see [System Center 2016  Integration Packs](https://www.microsoft.com/download/details.aspx?id=54098).
- To download this integration pack Orchestrator 2019, see [System Center 2019 Integration Packs](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).
::: moniker-end

::: moniker range="sc-orch-2022"

- To download this integration pack Orchestrator 2022, see [System Center 2022 Integration Packs](https://www.microsoft.com/download/details.aspx?id=104337).

::: moniker-end

::: moniker range="sc-orch-2025"

REST Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the REST Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=104337).

::: moniker-end

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to runbook servers and installed Runbook Designers. Learn more about [adding an integration pack](how-to-add-an-integration-pack.md).
