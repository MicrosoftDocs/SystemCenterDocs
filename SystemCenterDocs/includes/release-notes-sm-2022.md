---
description: include file to detail the release notes for Service Manager 2022
ms.topic: include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service:  system-center
ms.subservice: service-manager
keywords:
ms.date: 03/07/2024
title: include file
ms.update-cycle: 1095-days
ms.assetid:
---

## Service Manager 2022 release notes
The following sections detail the release notes for Service Manager 2022 and include the known issues and workarounds.

### Known issues and workarounds

#### Manual steps to activate Data Warehouse Server

**Description**: Service Manager Data Warehouse isn't activated as part of the Management Server license activation. You must manually activate the Data Warehouse.

**Workaround**:
Follow these steps to manually activate the Data Warehouse server:  
1. Open Windows PowerShell.
2. Change directory to Installation folder/Powershell.
3. Run the following command to import PowerShell module;
   `– Import-Module .\System.Center.Service.Manager.psm1`
4. Run `Set-SCSMLicense powershell` cmdlet to activate the license.

   > [!NOTE]
   > DW server is the management server input to this command.


#### Installation of SM 2022 on TLS 1.2 machine fails

**Description**:
Fresh Installation of System Center Service Manager 2022 or an upgrade from a previous version to SM 2022 fails if the computer is TLS 1.2 hardened.

**Workaround**:
Disable TLS 1.2 before the installation/upgrade and re-enable it after the upgrade is complete.


#### Connector for Orchestrator 2022 fails

**Description**:
Connector for Orchestrator 2022 might not work due to changes in Orchestrator Web service.

**Workaround**:
Continue using System Center 2019 Web API until we fix this. System Center 2022 supports running 2019 Web console/API side-by-side.

#### Report management pack deployments might fail

**Description**: After a successful Data Warehouse installation, deployments of Report management packs might fail if SQL Server Reporting Services (SSRS) is running locally on the Data Warehouse management Server and SSRS is 2017 or later. 

This issue is observed in Service Manager 2016 and later.

**Workaround**: Perform the steps [detailed here](../scsm/config-remote-ssrs.md).

## Service Manager 2022 UR2 release notes

No known issues in Service Manager 2022 UR2.

For the problems fixed in UR2 and the installation instructions for UR2, see the [KB article](https://support.microsoft.com/topic/hotfix-for-system-center-2022-service-manager-june-2023-kb5021792-8f17ff60-eafc-4c43-8399-85beebc1065f).