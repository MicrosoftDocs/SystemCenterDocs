---
ms.assetid: 8522-4f67-9853-2a4639442b0d
title: Upgrade to SPF 2016
description: This article describes how to upgrade to System Center Service Provider Foundation (SPF) 2016
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  11/04/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  service-provider-foundation
---

# Upgrade to SPF 2016
>Apples To: System Center 2016

This article describes how to upgrade from System Center 2012 R2 - Service Provider Foundation (SPF)  to SPF 2016.

The upgrade instructions in this article assume the following scenario:

- Windows Azure Pack is running on Windows Server 2012 R2 with [update rollup 10](https://support.microsoft.com/kb/3158609).
- SPF and VMM are running on System Center 2012 R2.
- SPF is running [update rollup 9](https://support.microsoft.com/en-us/kb/3133705) or later - [10](https://support.microsoft.com/kb/3147172).
- The VMM server is running [update rollup 9](https://support.microsoft.com/kb/3129784) or later - [10](https://support.microsoft.com/kb/3147167), or [11](https://support.microsoft.com/kb/3184831)
- The VMM console is running on a separate computer running Windows Server 2012 R2, and is also running update rollup 9 or later.

## Upgrade order

Here's the recommended upgrade order for the above scenario

1. Update the VMM console to 2016. If required, update the VMM server to 2016.
2. Update SPF to 2016.


## Run the SPF upgrade

1. Make sure Windows Azure Pack, SPF, and VMM are all running the required updates.
2. Verify [SPF deployment requirements](deploy/deploy/deploy-spf.md#before-you-begin).
3. [Verify operating system requirements](https://technet.microsoft.com/system-center-docs/system-requirements/client-operating-system-compatibility) for the VMM 2016 console. Then upgrade the VMM console from 2012 R2 to 2016. [Learn more](https://technet.microsoft.com/system-center-docs/vmm/deploy/deploy-install-console).
4. If you need access to a full VMM server to provide to create fabric and provide services to tenants, upgrade the VMM server from 2012 R2 to 2016. [Learn more](https://technet.microsoft.com/system-center-docs/vmm/deploy/deploy-upgrade).
5. Now upgrade SPF. To do that, first uninstall SPF 2012 R2 from the Control Panel.  The SPF uninstall does not uninstall the database. Before you uninstall note the SQL Server and database used by the current SPF installation. You can do this by running this on the SPF server:

    ``Import-module SpfAdmin
    Get-SCSPFConnectionString``

6. Uninstall Service Provider Foundation System Center 2012 R2 and the Virtual Machine Manager Console.
From Control Panel, in Programs, click Uninstall a program. Then under Name, right-click System Center 2012 R2 Service Provider Foundation, and then click **Uninstall**.
7. Now [install SPF 2016](deploy/deploy-spf.md). Specify the name of the current SQL Server during setup.


## Next steps

[Manage SPF](manage/manage-spf.md)
