---
title: System Center 2022 - Operations Manager Release Build Versions
description: Include file that shows the list of release builds for System Center 2022 - Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 08/18/2025
ms.service: system-center
ms.assetid: de403c5d-a2c6-4a8f-ba90-c9cf2086fe26
ms.subservice: operations-manager
ms.topic: include
---

## Operations Manager 2022 build versions

> [!NOTE]
> All System Center Operations Manager update rollups are cumulative. This means you don't need to apply them in order; you can always apply the latest update. If you've deployed System Center 2022 - Operations Manager and never applied an update rollup, you can proceed to install the latest one available.

The following tables list the release history for Operations Manager 2022.

### Management Server (and other components*)
|Build Number |KB |Release Date |Description |
|-------------|---|-------------|------------|
|10.22.10118.0||March 2022 |General Availability |
|10.22.10337.0|[5020318](https://support.microsoft.com/kb/5020318) | December 2022 | Update Rollup 1 |
|10.22.10337.0|[5022455](https://support.microsoft.com/kb/5022455) | December 2022 | Update Rollup 1 - Console Hotfix |
|10.22.10448.0|[5024286](https://support.microsoft.com/kb/5024286) | March 2023 | Update Rollup 1 - OpenSSL3.0 integration Hotfix |
|10.22.10565.0|[5029512](https://support.microsoft.com/kb/5029512) | July 2023 | Discover Azure Migrate in Operations Manager |
|10.22.10575.0|[5029601](https://support.microsoft.com/kb/5029601) | July 2023 | GB compliance |
|10.22.10560.0|[5028684](https://support.microsoft.com/kb/5028684) | August 2023 | SCX Compiler Mitigated Packages <br/> <br/> **This package is not cumulative; apply [KB5024286](https://support.microsoft.com/topic/system-center-operations-manager-2022-now-has-openssl3-0-integration-kb-5024286-331bd221-10f9-42d5-bc06-775eaabe3081) as a prerequisite**. |
|10.22.10610.0|[5031649](https://support.microsoft.com/kb/5031649) | November 2023 | Update Rollup 2 |
|10.22.10618.0|[5033752](https://support.microsoft.com/kb/5033752) | December 2023 | Update Rollup 2 Hotfix - Addresses Linux monitoring issues. |
|10.22.10684.0|[5037360](https://support.microsoft.com/kb/5037360) | April 2024 | Update Rollup 2 Hotfix - Introduces support for crypto policies in FIPS mode, specifically tailored for users monitoring Linux workloads. |
|10.22.11642.0|[5059070](https://support.microsoft.com/kb/5059070) | August 2025 | Update Rollup 3 |

### Agent and Gateway
|Build Number |KB |Release Date |Description |
|-------------|---|-------------|------------|
|10.22.10056.0||March 2022 |General Availability |
|10.22.10110.0|[5020318](https://support.microsoft.com/kb/5020318) | December 2022 | Update Rollup 1|
|10.22.10208.0|[5031649](https://support.microsoft.com/kb/5031649) | November 2023 | Update Rollup 2 |
|10.22.10215.0|[5033752](https://support.microsoft.com/kb/5033752) | November 2023 | Update Rollup 2 hotfix |
|10.22.10870.0|[5059070](https://support.microsoft.com/kb/5059070) | August 2025 | Update Rollup 3 |

### SCX Agent
|Build Number |KB |Release Date |Agent Version |Description |
|-------------|---|-------------|--------------|------------|
|10.22.1019.0|[v1.6.9-0](https://github.com/microsoft/SCXcore/releases/tag/v1.6.9-0) |March 2022 |1.6.9-0 |General Availability |
|10.22.1024.0|[v1.6.9-2](https://github.com/microsoft/SCXcore/releases/tag/v1.6.9-2) |May 2022 |1.6.9-2 |OMI Vulnerability Fix |
|10.22.1032.0|[v1.6.10-2](https://github.com/microsoft/SCXcore/releases/tag/v1.6.10-2) |August 2022 |1.6.10-2 |OMI Vulnerability Fix |
|10.22.1039.0|[v1.6.11-0](https://github.com/microsoft/SCXcore/releases/tag/v1.6.11-0) |December 2022 |1.6.11-0 |Update Rollup 1 |
|10.22.1042.0|[v1.6.12-1](https://github.com/microsoft/SCXcore/releases/tag/v1.6.12-1) |February 2023 |1.6.12-1 |Update Rollup 1 - Hotfix |
|10.22.1044.0|[v1.7.0-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.0-0) |March 2023 |1.7.0-0 |Update Rollup 1 - OpenSSL 3.0 |
|10.22.1052.0|[v1.7.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.1-0) |August 2023 |1.7.1-0 |Update Rollup 1 - Hotfix |
|10.22.1055.0|[v1.7.3-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.3-0) |November 2023 |1.7.3-0 |UR2 refresh/Deactivate OMI HTTP tracing|
|10.22.1070.0|[v1.8.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.8.1-0) |March 2024 |1.8.1-0 |Update Rollup 2 - Hotfix |
|10.22.1072.0|[v1.9.0-0](https://github.com/microsoft/SCXcore/releases/tag/v1.9.0-0) |April 2024 |1.9.0-0 |FIPS Crypto Policy Support |
|10.22.1175.0|[v1.9.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.9.1-0)|September 2024 |1.9.1-0 |OpenSSL version 3.x Support|
|10.22.1330.0| - | August 2025 | Update Rollup 3 |

 \* *The other components include: Databases, Operations Consoles, Reporting, and Web Consoles.*
