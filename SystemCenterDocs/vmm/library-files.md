---
ms.assetid: 1ec9b2c2-5045-4605-8331-711ed30163d0
title: Add file-based resources to the VMM library
description: This article provides guidance for adding files to the library in the VMM compute fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Add file-based resources to the VMM library



After you've [set up](manage-library-server.md) the System Center - Virtual Machine Manager (VMM) library, use this article if you want to add file-based resources to the library, and mark objects in the library as equivalent.

You can add file-based resources to the library as follows:

- Copy files to the share in the VMM console
- Import and export file-based resources between library shares
- Copy files to the library share from outside the VMM console

## Copy files to the share in the VMM console

1. Go to **Library** > **Library Servers**.
1. Right-click a library share > **Explore**.
1. Copy files to the share.

## Import and export files between libraries

1. Click **Library** > **Import Physical Resource**.
1. Select whether to import a resource or custom resources, select the destination library server, share, and optionally a folder. Click **OK** > **Import**. Verify the import in **Library Servers** > target location > **Physical Library Objects**.
1. To export click **Export Physical Resource**.
1. Right-click a library share > **Explore**. Select the resources you want to export (Select and hold the SHIFT key for multiple) and click **OK**. Select a destination folder and click **OK** > **Export**.
1. Copy files to the share.

## Mark objects as equivalent

You can group library resources together so they're considered equivalent. Then when you create templates and profiles and point to a specific virtual disk on a library share, VMM can substitute any equivalent object when a VM or service is created. This means you can author templates and profiles without relying on specific physical resources, and resources can be serviced without affecting template and profile availability.

VMM supports virtual disks, .iso images, and custom resources as equivalent objects. Equivalent resources must be the same file type.

You'll need to be an admin, delegated admin or self-service user to mark objects as equivalent.  Delegated admins can mark on library shares within their scope. Self-service users can marks objects in their user role data path.

1. Click **Library** > **Library servers**.
1. For admins and delegated admins the **Library Server** column indicates the location of each resource. Self-services users should expand **Self Service User Content** > **Type** to sort library resources.
1. Right-click the resources > **Mark Equivalent**.
1. In **Equivalent Library Objects** type the family name and release value to create a new equivalent set, or click a family name to add to an existing set. Objects must have the same family name, release value, and namespace (automatically assigned by VMM) to be equivalent.

## Next steps

[Learn about](library-profiles.md) adding profiles to the VMM library.
