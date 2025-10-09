---
ms.assetid: 
title: Include file
description: Include file to summarize the release notes for VMM 2019.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  08/07/2025
ms.topic:  include
ms.service: system-center
ms.subservice: virtual-machine-manager
---

## VMM 2022 release notes

The following sections summarize the release notes for VMM 2022 and include the known issues and workarounds.

- For issues fixed in 2022 UR1, [see the KB article for UR1](https://support.microsoft.com/kb/5019202).
- For issues fixed in 2022 UR2, [see the KB article for UR2](https://support.microsoft.com/kb/5032369).
- For issues fixed in 2022 UR3, [see the KB article for UR3](https://support.microsoft.com/kb/5055459).

## Known issues

### Chinese language support for SCVMM

Chinese characters that are part of GB18030 and appear in the names or properties of resources managed by SCVMM may not be recognized. To overcome this limitation, it is necessary to update the SQL database associated with SCVMM to [Cumulative Update 12](/troubleshoot/sql/releases/sqlserver-2022/cumulativeupdate12) and run this [SQL query](https://download.microsoft.com/download/aceff22d-08dc-44be-be76-24ff634fc405/GBIssueFixSQLQuery_new.sql) in the database.
