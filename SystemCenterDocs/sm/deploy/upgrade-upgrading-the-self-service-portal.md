---
title: Upgrading the Self-Service Portal
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e31341b7-64ec-4f93-8b89-08f48fac128f
---

# Upgrading the Service Manager Self-Service Portal

>Applies To: System Center 2016 - Service Manager

The Service Manager Self-Service Portal was updated for Service Manager 2012 R2 and Service Manager 2016. The new HTML 5-based version replaces the Sliverlight-based version. Use the following section that applies to the version that you want to replace.

## Upgrading a standalone installation of the Service Manager 2012 R2 Silverlight-based Self Service portal
Use the following steps to upgrade your Self Service portal and Service Manager management servers where they are installed on different computers.

On the Service Manager 2012 R2 Silverlight Self Service Portal:
1. Uninstall the Silverlight-based Self Service portal. Support for Silverlight was removed with Service Manager 2016.
2. Install the new HTML5-based Self Service Portal, using the information at [Deploy the Self-Service Portal for Service Manager](deploy-deploy-the-self-service-portal-for-service-manager.md).

## Upgrading a standalone installation of the Service Manager 2012 R2 HTML5-based Self Service portal
Use the following step to upgrade your Self Service portal and Service Manger management servers where they are installed on different computers.

- Upgrade the Self Service portal directly from Service Manager 2012 R2 to Service Manager 2016.

## Upgrading from Service Manager 2012 R2 installed on a secondary management server with a Silverlight-based Self Service Portal
1.  Uninstall Service Manager 2012 R2. This step uninstalls the management server role from the computer.
2.  Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3.  Install the secondary Management Server 2016 role on new computer.
4.  Install the Service Manager 2016 version of the Self Service Portal (HTML5) on same computer as the secondary management server.

## Upgrading from Service Manager 2012 R2 installed on a secondary management server with a HTML-based Self Service Portal

1.  Decommission the computer - neither the Self Service portal nor Service Manager 2012 R2 can be uninstalled. Create backups of the Self Service portal configuration files - web.config (inside the website folder), custom.css (inside the website folder \Content\CSS) and sidebar.cshtml (inside the website folder \Views\Shared) because they are required later.
2.  Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3.  Install the secondary Management Server 2016 role on new computer.
4.  Install the Service Manager 2016 version of the Self Service Portal (HTML5) on the same computer as the secondary management server.
5.  Overwrite the current configuration files with those backed-up in step 1 to restore any customizations.

## Upgrading from Service Manager 2012 R2 installed on a primary Management Server with the Self Service portal (Silverlight/HTML5):
*Installing the Self Service portal on the same computer as the primary management server is not recommended.* However, in the event that you are using this combination, then use the following steps to upgrade to Service Manager 2016. Enabling the upgrade is the first step to move the primary Management Server to a Secondary management server by using the following steps.

1. Add new the Service Manager 2012 R2 secondary management server to a management group.
2. Promote the secondary management server to a primary management server role, which will move the current primary management server to a secondary role.
3. Follow the steps mentioned in the *Upgrading from Service Manager 2012 R2 installed on a secondary management server with a Silverlight-based Self Service Portal* or in the *Upgrading from Service Manager 2012 R2 installed on a secondary management server with a HTML-based Self Service Portal* sections to upgrade your management server and Self Service portal to Service Manager 2016.

## Upgrading from Service Manager 2016 TP5 Self Service portal (stand alone or with a management server)
  - You can upgrade the Self Service portal directly from Service Manager 2012 R2 to Service Manager 2016.
