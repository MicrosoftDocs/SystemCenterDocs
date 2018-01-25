---
ms.assetid: c97929cf-5a66-4597-ae74-d1c3e6bcd5d8
title: Upgrade to SPF 1801
description: This article provides information about  how to upgrade to System Center Service Provider Foundation (SPF) 1801 from a previous version.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  01/24/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  service-provider-foundation
monikerRange: 'sc-spf-1711'
---

# Upgrade System Center 1801 -  Service Provider Foundation

This article describes how to upgrade from System Center 2012 R2 UR 12/2016 UR2 - Service Provider Foundation (SPF)  to SPF 1801. 

The upgrade instructions in this article assume the following scenario:

- Windows Azure Pack is running on Windows Server 2012 R2 with [update rollup 12] or 2016 UR2.
- SPF and VMM are running on System Center 2012 R2 UR12/2016 UR2.
- The VMM console whether System Center 2012R2 or 2016 should be running their latest URs. The OS can be 2012 R2 or 2016.

## Upgrade order

Here's the recommended upgrade order for the above scenario:

1. Update the VMM console to 1801. If required, update the VMM server to 1801.
2. Update SPF to 1801.


## Run the SPF upgrade

1. Make sure Windows Azure Pack, SPF, and VMM are all running the required updates.
2. Verify [SPF deployment requirements](deploy-spf.md#before-you-begin).
3. [Verify operating system requirements](https://technet.microsoft.com/system-center-docs/system-requirements/client-operating-system-compatibility) for the VMM 1801 console. Then upgrade the VMM console from 2012 R2/2016 to 1801. [Learn more](https://technet.microsoft.com/system-center-docs/vmm/deploy/deploy-install-console).
4. If you need access to a full VMM server to provide to create fabric and provide services to tenants, upgrade the VMM server from 2012 R2/2016 to 1801. [Learn more](https://technet.microsoft.com/system-center-docs/vmm/deploy/deploy-upgrade).
5. Now upgrade SPF. To do that, first uninstall the current version of SPF (2012 R2/2016) from the Control Panel.  The SPF uninstall does not uninstall the database. Before you uninstall, note the SQL Server and database used by the current SPF installation. You can do this by running the following command on the SPF server:

    ``Import-module SpfAdmin
    Get-SCSPFConnectionString``

6. Uninstall the SPF 2012 R2/2016 and the Virtual Machine Manager Console. To uninstall, go to **Control Panel** > **Programs**, click **Uninstall a program**. Then, under **Name**, right-click System Center 2012 R2 Service Provider Foundation, and then click **Uninstall**.
7. Now [install SPF 1801](~/spf/deploy-spf.md). Specify the name of the current SQL Server during the setup.


## Next steps

[Manage SPF](manage/manage-spf.md)
