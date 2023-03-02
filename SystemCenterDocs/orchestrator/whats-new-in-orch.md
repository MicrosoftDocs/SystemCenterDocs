---
title: What's new in System Center Orchestrator
description: This article describes the new features and other changes in System Center Orchestrator.
manager: mkluck
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.prod: system-center
ms.date: 02/22/2023
ms.technology: orchestrator
ms.assetid: 6e89c2ee-583a-41df-a94c-47f349f954ef
monikerRange: '>sc-orch-2016'
ms.custom: UpdateFrequency1, engagement-fy23
---

# What's new in System Center Orchestrator

::: moniker range="sc-orch-2022"

This article details the new features supported in System Center 2022 - Orchestrator and Orchestrator 2022 UR1.

::: moniker-end

::: moniker range="sc-orch-2019"

This article details the new features supported in System Center 2019 - Orchestrator.

::: moniker-end

::: moniker range="sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

No new features are introduced with System Center 1807 - Orchestrator.

::: moniker-end

::: moniker range="sc-orch-1801"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

This article details the new features supported in System Center 1801 - Orchestrator.

::: moniker-end

::: moniker range="sc-orch-1801"

## Support for TLS 1.2

This release of System Center Orchestrator (SCO) contains all the bug fixes shipped until the [Update Rollup 4 of SCO 2016](https://support.microsoft.com/help/4047355/update-rollup-4-for-system-center-2016-orchestrator), along with the added support of TLS 1.2 Protocol.

For more information about how to set up, configure, and run your environment to use TLS 1.2, [read this article](https://support.microsoft.com/help/4051111/tls-1-2-protocol-support-deployment-guide-for-system-center-2016).

::: moniker-end

::: moniker range="sc-orch-2019"

## OAuth support for Exchange Online
System Center 2019 provides OAuth support for Exchange Online in System Center Orchestrator 2019 Exchange Admin and Exchange User Integration Packs.

## Support for PowerShell 4.0+
Earlier versions of System Center Orchestrator supported PowerShell V2.0. PowerShell V2.0 didn't support some scripts and users had to apply workarounds. System Center Orchestrator 2019 supports PowerShell V4.0 to resolve this issue.

## Support for SQL 2017
System Center Orchestrator 2019 supports SQL 2017 for fresh installation.

## Support for SQL Server 2022

Orchestrator 2019 support SQL Server 2022.

## Other Improvements
-  Latest Putty: No workaround needed to SSH to the latest Linux/Unix machines.
-  SM/SCOM integration is cleaner and now has respective console dependency only.

## Bug fixes
This release of System Center Orchestrator (SCO) contains all the bug fixes shipped until the [Update Rollup 6 of SCO 2016](https://support.microsoft.com/help/4465567/update-rollup-6-for-system-center-2016-orchestrator), along with the added support of TLS 1.2 Protocol.

For more information about how to set up, configure, and run your environment to use TLS 1.2, [read this article](https://support.microsoft.com/help/4051111/tls-1-2-protocol-support-deployment-guide-for-system-center-2016).

> [!NOTE]
> No features were introduced in System Center Orchestrator 1807.

> [!NOTE]
> The following features/feature updates were introduced in System Center Orchestrator 1801.

## Support for TLS 1.2

This release of System Center Orchestrator (SCO) contains all the bug fixes shipped until the [Update Rollup 4 of SCO 2016](https://support.microsoft.com/help/4047355/update-rollup-4-for-system-center-2016-orchestrator), along with the added support of TLS 1.2 Protocol.

For more information about how to set up, configure, and run your environment to use TLS 1.2, [read this article](https://support.microsoft.com/help/4051111/tls-1-2-protocol-support-deployment-guide-for-system-center-2016).

::: moniker-end

::: moniker range="sc-orch-2022"

## New features in Orchestrator 2022

See the following sections for detailed information about the new features/feature updates supported in Orchestrator 2022.

### SCO 2022 Integration packs

The following SCO 2022 Integration packs are available for download from Download Center:

 - [System Center 2022 Configuration Manager Integration Pack](https://www.microsoft.com/download/details.aspx?id=104338)
 - [System Center 2022 Operations Manager Integration Pack](https://www.microsoft.com/download/details.aspx?id=104339)
 - [System Center 2022 Virtual Machine Manager Integration Pack](https://www.microsoft.com/download/details.aspx?id=104340)
 - [System Center 2022 Service Manager Integration Pack](https://www.microsoft.com/download/details.aspx?id=104341)
 - [System Center 2022 Data Protection Manager Integration Pack](https://www.microsoft.com/download/details.aspx?id=104334)
 - [Active Directory Integration Pack](https://www.microsoft.com/download/details.aspx?id=104333)
 - [Exchange Admin Integration Pack](https://www.microsoft.com/download/details.aspx?id=104335)
 - [Exchange User Integration Pack](https://www.microsoft.com/download/details.aspx?id=104336)
 - [REST Integration Pack](https://www.microsoft.com/download/details.aspx?id=104337)
 - [SharePoint Integration Pack](https://www.microsoft.com/download/details.aspx?id=104332)

### New web console and web API

A new web console and web API are introduced in System Center Orchestrator 2022.

The new web API is JSON based and makes it easier to use than the older XML-based counterpart. Particularly, the job creation with parameters API has been greatly simplified.

>[!NOTE]
>The new Web console is a complete redesign and works only on modern browsers like Microsoft Edge without Silverlight.

### Orchestrator is now a 64-bit application

Support for 64 bit enables the use of 64-bit assemblies, Integration Packs, and PowerShell cmdlets.

## New features in Orchestrator 2022 UR1

The following sections introduce the new features and feature updates supported in Orchestrator 2022 Update Rollup 1 (UR1).

### Issues fixed and Improvements in SCO 2022 Update Rollup 1

For issues fixed in Orchestrator 2022 UR1, and installation instructions for UR1, see the [KB article](https://support.microsoft.com/KB/5021420).

#### Support for SQL Server 2022

Orchestrator 2022 supports SQL Server 2022. [Learn more](/system-center/orchestrator/system-requirements-orch#sql-server).

#### Support for .NET Core 6

Orchestrator 2022 UR1 depends on .NET Core 6. 

Ensure .NET Core 6 and Hosting Bundle are installed when you upgrade from RTM. [Learn more](/system-center/orchestrator/system-requirements-orch#net-requirements).

::: moniker-end

## Next steps
[Know the fixed issues](release-notes-orch.md).

