---
description: include file to detail the release notes for Service Manager 2022
manager:  evansma
ms.topic: include
author:  v-pgaddala
ms.author: v-pgaddala
ms.prod:  system-center
ms.technology: service-manager
keywords:
ms.date: 12/29/2021
title: include file
ms.assetid: 
---

## Release Notes for System Center 2022 - Service Manager
The following sections detail the release notes for Service Manager 2022 and include the known issues and workarounds.

## Known issues and workarounds

### Manual steps to activate Data Warehouse Server

**Description**: Service Manager Data Warehouse is not activated as part of the Management Server license activation. You must manually activate the Data Warehouse.

**Workaround**:
Follow these steps to manually activate the Data Warehouse server:  
1. Open Windows PowerShell.
2. Change directory to Installation folder/Powershell.
3. Run the following command to import PowerShell module;
   `– Import-Module .\System.Center.Service.Manager.psm1`
4. Run `Set-SCSMLicense powershell` cmdlet to activate the license.

   > [!NOTE]
   > DW server is the management server input to this command.


### Installation of SM 2022 on TLS 1.2 machine fails

**Description**: 
Fresh Installation of System Center Service Manager 2022 or an upgrade from a previous version to SM 2022 fails if the computer is TLS 1.2 hardened.

**Workaround**: 
Disable TLS 1.2 before the installation/upgrade and re-enable it after the upgrade is complete.