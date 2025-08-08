---
title: Upgrade the Self-Service portal in System Center 2016 - Service Manager
description: Use information in this article to upgrade the Service Manager Self-Service portal.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.subservice: service-manager
ms.topic: upgrade-and-migration-article
monikerRange: 'sc-sm-2016'
ms.custom: UpdateFrequency.5
---

# Upgrade the Service Manager Self-Service portal

There are a couple of versions of the Self-Service portal:

- The Service Manager 2012 R2 Silverlight-based version.
- The new HTML5-based version. This replaces the Silverlight version.

Follow the upgrade instructions based on the version you're running:

## Upgrade from Silverlight portal

The upgrade steps depend whether you're running the Self-Service Portal on a standalone machine or colocated with Service Manager.

## Upgrade from Silverlight on a standalone computer

1. On the Service Manager 2012 R2 Silverlight Self-Service Portal, uninstall the Silverlight-based Self-Service portal. Support for Silverlight was removed with Service Manager 2016.
2. Install the new HTML5-based Self-Service Portal with [these instructions](~/scsm/deploy-self-service-portal.md).

## Upgrade from Silverlight installed on the primary management server

Installing the Self-Service Portal on the same computer as the primary management server isn't recommended. However, if you've done this, use the following steps to upgrade to Service Manager 2016.

1. Add the secondary Service Manager 2012 R2 management server to a management group.
2. Promote the secondary management server to a primary management server role, which will move the current primary management server to a secondary role.
3. Uninstall Service Manager 2012 R2. This step uninstalls the management server role from the computer.
4. Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
5. Install the secondary Management Server 2016 role on the new computer.
6. Install the Service Manager 2016 version of the Self-Service Portal (HTML5) on the same computer as the secondary management server.

## Upgrade from Silverlight installed on the secondary management server

1. Uninstall Service Manager 2012 R2. This step uninstalls the management server role from the computer.
2. Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3. Install the secondary Management Server 2016 role on the new computer.
4. Install the Service Manager 2016 version of the Self-Service Portal (HTML5) on the same computer as the secondary management server.

## Upgrade from HTML5 portal

The upgrade steps depend whether you're running the Self-Service Portal on a standalone machine or colocated with Service Manager.

## Upgrade from HTML5 on a standalone computer

Upgrade the Self-Service Portal directly from Service Manager 2012 R2 to Service Manager 2016.

## Upgrade from HTML5 installed on the management server

Installing the Self-Service portal on the same computer as the primary management server isn't recommended. However, if you've done this, use the following steps to upgrade to Service Manager 2016.

1. Don't uninstall the Self-Service Portal or Management Server; attempting uninstallation might create an unstable state.
2. [Download](https://go.microsoft.com/fwlink/?LinkID=798214) the patch "SM2016SSP_UpgradeFix_20160601.exe", and install it on the server where the 2012 R2 Self-Service Portal is installed.
3. Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
4. Self-Service Portal will also get upgraded along with the primary management server.

## Upgrade from HTML5 installed on the secondary management server

1. Don't uninstall the Self-Service Portal or Management Server; attempting uninstallation might create an unstable state.
2. [Download](https://go.microsoft.com/fwlink/?LinkID=798214) the patch "SM2016SSP_UpgradeFix_20160601.exe".
3. Install it on the server where the 2012 R2 Self Service Portal is installed.
4. Upgrade both primary and secondary Management Servers from Service Manager 2012 R2 to Service Manager 2016. The Self Service Portal will also get upgraded along with the secondary management server.

## Next steps

- [Set up a lab environment with production data to prepare for upgrade](set-up-lab-with-production-data.md).
