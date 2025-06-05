---
title: System Center 2019 - Operations Manager Release Build Versions
description: Include file that shows the list of release builds for System Center 2019 - Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 10/02/2024
ms.service: system-center
ms.assetid: de403c5d-a2c6-4a8f-ba90-c9cf2086fe26
ms.subservice: operations-manager
ms.topic: include
---

## Operations Manager 2019 build versions

> [!NOTE]
> All System Center Operations Manager update rollups are cumulative. This means you don't need to apply them in order; you can always apply the latest update. If you've deployed System Center 2019 - Operations Manager and never applied an update rollup, you can proceed to install the latest one available.

The following tables list the release history for Operations Manager 2019.

### Management Server (and other components*)
|Build Number |KB |Release Date |Description |
|-------------|---|-------------|------------|
|10.19.10050.0||March 2019 |General Availability release |
|10.19.10311.0|[4533415](https://support.microsoft.com/kb/4533415) |February 2020 |Update Rollup 1 |
|10.19.10349.0|[4551468](https://support.microsoft.com/kb/4551468) |April 2020 |Update Rollup 1 - Hotfix for Alert Management |
|10.19.10407.0|[4558752](https://support.microsoft.com/kb/4558752) |August 2020 |Update Rollup 2 |
|10.19.10475.0|[4601269](https://support.microsoft.com/kb/4601269) |February 2021 |Update Rollup 2 - Hotfix for Event Log Channel |
|10.19.10505.0|[4594078](https://support.microsoft.com/kb/4594078) |March 2021 |Update Rollup 3 |
|10.19.10550.0|[5006871](https://support.microsoft.com/kb/5006871) |October 2021 |Update Rollup 3 - Web Console IDOR Vulnerability Fix |
|10.19.10552.0|[5005527](https://support.microsoft.com/kb/5005527) |October 2021 |Update Rollup 3 - Hotfix Oct 2021 |
|10.19.10569.0|[5013427](https://support.microsoft.com/kb/5013427) |June 2022 |Update Rollup 4 |
|10.19.10576.0|[5016576](https://support.microsoft.com/kb/5016576) |July 2022 |Update Rollup 4 - Hotfix for Operations Console Performance issue |
|10.19.10606.0|[5025123](https://support.microsoft.com/kb/5025123) |April 2023 |Update Rollup 5 |
|10.19.10616.0|[5029512](https://support.microsoft.com/kb/5029512) |July 2023|Discover Azure Migrate in Operations Manager|
|10.19.10615.0|[5029601](https://support.microsoft.com/kb/5029601) |July 2023|GB compliance|
|10.19.10618.0|[5028684](https://support.microsoft.com/kb/5028684) |August 2023|SCX Compiler Mitigated Packages|
|10.19.10649.0|[5035285](https://support.microsoft.com/kb/5035285) |March 2024|Update Rollup 6|
|10.19.10652.0|[5037360](https://support.microsoft.com/kb/5037360) | April 2024 | Update Rollup 6 Hotfix - Introduces support for crypto policies in FIPS mode, specifically tailored for users monitoring Linux workloads. |

### Agent and Gateway
|Build Number |KB |Release Date |Description |
|-------------|---|-------------|------------|
|10.19.10014.0||March 2019 |General Availability release |
|10.19.10140.0|[4533415](https://support.microsoft.com/kb/4533415) |February 2020 |Update Rollup 1 |
|10.19.10153.0|[4558752](https://support.microsoft.com/kb/4558752) |August 2020 |Update Rollup 2 |
|10.19.10177.0|[4594078](https://support.microsoft.com/kb/4594078) |March 2021 |Update Rollup 3 |
|10.19.10185.0|[5005527](https://support.microsoft.com/kb/5005527) |October 2021 |Update Rollup 3 - Hotfix Oct 2021 |
|10.19.10200.0|[5013427](https://support.microsoft.com/kb/5013427) |June 2022 |Update Rollup 4 |
|10.19.10211.0|[5025123](https://support.microsoft.com/kb/5025123) |April 2023 |Update Rollup 5 |
|10.19.10253.0|[5035285](https://support.microsoft.com/kb/5035285) |March 2024|Update Rollup 6|

### SCX Agent
|Build Number |KB |Release Date |Agent Version |Description |
|-------------|---|-------------|--------------|------------|
|10.19.1008.0||March 2019 |1.6.3-793 |General Availability release |
|10.19.1082.0|[v1.6.4-7](https://github.com/microsoft/SCXcore/releases/tag/scx-1.6.4-7) |February 2020 |1.6.4-7 |Update Rollup 1 |
|10.19.1123.0|[v1.6.6-0](https://github.com/microsoft/SCXcore/releases/tag/v1.6.6-0) |August 2020 |1.6.6-0 |Update Rollup 2 |
|10.19.1138.0|[v1.6.8-0](https://github.com/microsoft/SCXcore/releases/tag/v1.6.8-0) |March 2021 |1.6.8-0 |Update Rollup 3 |
|10.19.1147.0|[v1.6.8-1](https://github.com/microsoft/SCXcore/releases/tag/v1.6.8-1) |October 2021 |1.6.8-1 |Update Rollup 3 - OMI Vulnerability Fix |
|10.19.1150.0|[v1.6.10-1](https://github.com/microsoft/SCXcore/releases/tag/v1.6.10-1) |June 2022 |1.6.10-1 |Update Rollup 4 |
|10.19.1158.0|[v1.6.10-2](https://github.com/microsoft/SCXcore/releases/tag/v1.6.10-2) |August 2022 |1.6.10-2 |Update Rollup 4 - OMI Vulnerability Fix |
|10.19.1167.0|[v1.6.11-0](https://github.com/microsoft/SCXcore/releases/tag/v1.6.11-0) |December 2022 |1.6.11-0 |Update Rollup 4 - Hotfix |
|10.19.1195.0|[v1.6.12-1](https://github.com/microsoft/SCXcore/releases/tag/v1.6.12-1) |February 2023 |1.6.12-1 |Update Rollup 4 - Hotfix |
|10.19.1214.0|[v1.7.0-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.0-0) |March 2023 |1.7.0-0 |Update Rollup 4 - OpenSSL 3.0 |
|10.19.1226.0|[v1.7.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.1-0) |August 2023 |1.7.1-0 |Update Rollup 5 - Hotfix |
|10.19.1234.0|[v1.7.3-0](https://github.com/microsoft/SCXcore/releases/tag/v1.7.3-0) |November 2023 |1.7.3-0 |OMI Vulnerability Fix |
|10.19.1248.0| [v1.8.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.8.1-0) |March 2024|1.8.1-0|Update Rollup 6 |
|10.19.1254.0|[v1.9.0-0](https://github.com/microsoft/SCXcore/releases/tag/v1.9.0-0) |April 2024 |1.9.0-0 |FIPS Crypto Policy Support |
|10.19.1258.0|[v1.9.1-0](https://github.com/microsoft/SCXcore/releases/tag/v1.9.1-0) |September 2024 |1.9.1-0 |OpenSSL version 3.x Support |

 \* *The other components include: Databases, Operations Consoles, Reporting, and Web Consoles.*
