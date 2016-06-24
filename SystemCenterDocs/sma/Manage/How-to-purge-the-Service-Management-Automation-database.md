---
title: How to purge the Service Management Automation database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09b8fca5-e1db-4775-910d-48cb8214401b
---
# How to purge the Service Management Automation database
In Service Management Automation, database purging is automatic, but you can adjust it to your needs.

To enable the automatic database purge, you must enable the SQL Server Agent (MSSQLSERVER) service for Automatic start. The service is not turned on by default, but it is frequently started by SQL Server database administrators for other tasks.

If the SQL Server Agent service is not running, the purge will not occur and eventually the customer will experience performance issues, first in the portal. and then with the back end.)

The job task that performs purge can be set up in the installer even if the customer is not running the SQL Server Agent service. But it will not do anything until the service is enabled.

The database purge job is automatic, but it can be regulated by the Service Management Automation administrator.

-   By default, the database purge job runs every 15 minutes, and it runs only if there are records to purge.

-   Records are purged only if they are older than the default duration of 30 days. This time is configurable by using the **Set-SmaAdminConfiguration** cmdlet and setting the **–PurgeJobsOlderThanCountDays** parameter.

-   If the total job record count exceeds the **MaxJobRecords** parameter set by the same **Set-SmaAdminConfiguration** cmdlet, then more job records will be purged. The default value for this parameter is 120,000 records.


