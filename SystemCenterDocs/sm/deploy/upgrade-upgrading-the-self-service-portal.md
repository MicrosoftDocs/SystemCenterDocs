---
title: Upgrade the Self-Service portal
description: Use the upgrade configurations in this article to upgrade the Service Manager Self-Service portal.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e31341b7-64ec-4f93-8b89-08f48fac128f
---

# Upgrade configurations for the Service Manager Self-Service portal

>Applies To: System Center 2016 - Service Manager

The Service Manager Self-Service portal was updated for Service Manager 2012 R2 and Service Manager 2016. The new HTML 5-based version replaces the Sliverlight-based version. Use the following section that applies to the version that you want to replace.

## Upgrade the Self Service portal from a standalone installation of the Service Manager 2012 R2 Silverlight-based Self Service portal
Use the following steps to upgrade your Self Service portal and Service Manager management servers when they are **installed on different computers**.

On the Service Manager 2012 R2 Silverlight Self Service Portal:
1. Uninstall the Silverlight-based Self Service portal. Support for Silverlight was removed with Service Manager 2016.
2. Install the new HTML5-based Self Service Portal, using the information at [Deploy the Self-Service Portal for Service Manager](deploy-deploy-the-Self-Service-Portal-for-Service-Manager.md)

## Upgrade the Self Service Portal from a standalone installation of the Service Manager 2012 R2 HTML5-based Self Service portal
Use the following step to upgrade your Self Service portal and Service Manger management servers when they are **installed on different computers**.

- Upgrade the Self Service portal directly from Service Manager 2012 R2 to Service Manager 2016.

## Upgrade the Silverlight-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **secondary** management server
1.  Uninstall Service Manager 2012 R2. This step uninstalls the management server role from the computer.
2.  Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3.  Install the secondary Management Server 2016 role on new computer.
4.  Install the Service Manager 2016 version of the Self Service Portal (HTML5) on same computer as the secondary management server.

## Upgrade the Silverlight-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **primary** management server
Installing the Self Service portal on the same computer as the primary management server is not recommended. However, in the event that you are using this combination, then use the following steps to upgrade to Service Manager 2016. Enabling the upgrade is the first step to move the primary Management Server to a Secondary management server by using the following steps

1.	Add new the Service Manager 2012 R2 secondary management server to a management group.
2.	Promote the secondary management server to a primary management server role, which will move the current primary management server to a secondary role.
3.	Follow the steps mentioned in the "Upgrading the Silverlight-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **secondary** management server"  section of this document, or in the "Upgrading the HTML5-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **secondary** management server" section of this document, to upgrade your management server and Self Service portal to Service Manager 2016.


## Upgrade the HTML5-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **secondary** management server
1.	**Do not uninstall the Self Service Portal or Management Server, attempting uninstallation might create an unstable state**
2.	Download the patch "SM2016SSP_UpgradeFix_20160601.exe" from [here](http://go.microsoft.com/fwlink/?LinkID=798214), and install it on the server where the 2012 R2 Self Service Portal is installed.
3.	Upgrade both primary and secondary Management Servers from Service Manager 2012 R2 to Service Manager 2016.
4.	Self Service Portal will also get upgraded along with the secondary management server.

## Upgrade the HTML5-based Self Service Portal from Service Manager 2012 R2, which is installed on same computer as the Service Manager **primary** management server
*Installing the Self Service portal on the same computer as the primary management server is not recommended.* However, in the event that you are using this combination, then use the following steps to upgrade to Service Manager 2016.

1.	Do not uninstall the Self Service Portal or Management Server, attempting uninstallation might create an unstable state
2.	Download the patch "SM2016SSP_UpgradeFix_20160601.exe" from [here](http://go.microsoft.com/fwlink/?LinkID=798214), and install it on the server where the 2012 R2 Self Service Portal is installed.
3.	Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
4.	Self Service Portal will also get upgraded along with the primary management server.


## Upgrade the Self Service Portal from Service Manager 2016 Technical Preview 5 Self Service portal (stand alone or with a management server)
  You can upgrade the Self Service portal directly from Service Manager 2016 Technical Preview 5 to Service Manager 2016.

## Next steps

- Review [Set up a Service Manager 2016 lab environment with production data to prepare for upgrade](upgrade-setting-up-a-service-manager-2016-lab-environment-with-production-data.md).
