---
description: Provides an overview of how you can purge the Service Management Automation database.
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
ms.date: 11/01/2024
title: Purge the Service Management Automation database
ms.subservice: service-management-automation
ms.custom: engagement-fy24
---

# Purge the Service Management Automation database

In Service Management Automation (SMA), database purging is automatic, but you can adjust it to your needs.

- To enable the automatic database purge, you must enable the SQL Server Agent (MSSQLSERVER) service for Automatic start. The service isn't turned on by default, but it's frequently started by SQL Server database administrators for other tasks.
- If the SQL Server Agent service isn't running, the purge won't happen, and eventually there will be performance issues, first in the portal and then in the back end.
- The job that performs purge can be set up in the installer, even if you're not running the SQL Server Agent service. The job doesn't do anything until the service is enabled.
- The database purge job is automatic, but it can be regulated by the SMA administrator.
- By default, the database purge job runs every 15 minutes, but only if there are records to purge.
- Records are purged if they're older than the default duration of 30 days. You can set this time using the **Set-SmaAdminConfiguration** cmdlet by setting the **"PurgeJobsOlderThanCountDays** parameter.
- If the total job record count exceeds the **MaxJobRecords** parameter set by the **Set-SmaAdminConfiguration** cmdlet, then more job records will be purged. The default value for this parameter is 120,000 records.
