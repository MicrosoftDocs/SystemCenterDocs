---
ms.assetid: 7e8f2af3-397d-41c3-a1d7-62c2c15fef7e
title: Monitoring Operations Manager from a Second Management Group
description: This article provides an overview of monitoring Operations Manager from a second management group
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 09/04/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Monitoring Operations Manager from a second management group

Businesses using System Center – Operations Manager in multiple management groups might monitor one management group from another management group. This topic provides the steps for monitoring one management group (management group A) from a second management group (management group B).

## Steps to monitor from second management group

- Install an agent on management servers in management group A from management group B. If you install the agent manually, configure the agent to report to a management server in management group B.
- Disable Active Directory integration for the agent you install on the management server in management group A.
- To upgrade the management server in management group A, you must remove the management group B agent first.
- After the agent is installed, ensure that you do not configure the agent to also report to management group A ("multihome" the agent).
- Ensure that the Run As accounts for the Default Action Account and Privileged Monitoring Account profiles for the management server in management group B are using credentials that can remotely authenticate and that have sufficient permissions on the management servers in management group A.

## Next steps

- [Operations Manager Monitoring Scenarios](manage-monitoring-scenarios.md)
- [Connecting Operations Manager With Other Management Systems](manage-integration-thirdparty-overview.md)
