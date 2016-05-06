---
title: Reviewing Availability and Recovery Options for Protecting the VMM Database
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71326238-bb75-4f83-a83b-29996ca136f0
---
# Reviewing Availability and Recovery Options for Protecting the VMM Database
When you are choosing among options for protecting the VMM database, whether in the context of availability or the context of disaster recovery, it is a good idea to review what can happen if the VMM database must be put “back in time” because of a failure situation. This can be necessary with some backup and recovery options and some availability options. For example, using SQL Server Availability Groups in asynchronous\-commit availability mode can require that you perform a failover that puts the database “back in time.”

## Database failover or recovery situations that might require restoring “back in time”
As with any database, if a hardware failure or other problem occurs, recent changes to the VMM database might be lost. Depending on the availability and recovery options in place, the VMM database might have to be failed over, or restored from backup, when the only version of the VMM database that remains available is slightly out of date. This is sometimes called going “back in time” for a database.

Database administrators study availability and recovery options with careful thought for how the database can be restored—meaning how closely it can be brought back to a precise moment in time, if a failure occurs. This topic does not attempt to describe all the pros and cons of various choices for availability or recovery, but two situations are worth calling out for the VMM database:

-   If SQL Server AlwaysOn Availability Groups are used with asynchronous commit mode, a forced failover might be necessary. Asynchronous commit mode means that any secondary replica of the database might lag behind the primary replica at any point. At the moment of a forced failover, if it is necessary to fail over to a secondary replica that has lagged behind, this will take the VMM database back in time. Asynchronous commit mode is described in more detail in the following topics:

    -   [Overview of AlwaysOn Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx), especially the [Availability Modes section](http://msdn.microsoft.com/library/ff877884.aspx#AvailabilityModes) in that topic

    -   [Availability Modes (AlwaysOn Availability Groups)](http://msdn.microsoft.com/library/ff877931.aspx), especially the [Asynchronous-Commit Availability Mode section](http://msdn.microsoft.com/library/ff877931.aspx#AsyncCommitAvMode) in that topic

-   For disaster recovery, it might be necessary to restore from a backup that was made somewhat before the moment of failure. This of course depends on the interval between VMM database backups \(including offsite backups\). If it is necessary to restore from a backup that was made before the point of failure, the VMM database would be put back in time.

## Information that can be affected if the VMM database must be put back in time
It can be useful to review the possible effects that can result if the VMM database must be put back in time. Examples include:

-   Permissions that were changed shortly before a failure occurred might be reverted after the VMM database is failed over or restored.

-   Access that was removed shortly before a failure occurred might be available again after the VMM database is failed over or restored.

    For example, access to the contents of a VHD might be available to users who otherwise would not have access.

-   VM networks that were removed shortly before a failure occurred might be available again after the VMM database is failed over or restored.

When choosing among availability and recovery options for protecting the VMM database, it can be useful to review the previous list in relation to your specific environment and requirements.

## See Also
[Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

