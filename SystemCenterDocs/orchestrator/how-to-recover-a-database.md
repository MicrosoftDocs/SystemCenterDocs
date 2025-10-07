---
title: Recover a Database
description: Describes how to restore a database from backup in System Center - Orchestrator.
ms.date: 04/17/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: engagement-fy23
---

# Recover a database

The Orchestrator database can be backed up and restored using most standard MS SQL Server database backup\/restore mechanisms. This includes Microsoft SQL Server Backup, DPM SQL Server backup, and others. Orchestrator provides a VSS Writer that will discover the database server that is associated with the Management Server and back up the database when the Management Server is backed up.  

However, there are a few key considerations when restoring.  

## Orchestrator cryptography

Orchestrator provides a set of services for encryption and decryption of runbook properties and published data. These services are based on Microsoft SQL Server 2008 R2 cell\-level encryption. The Orchestrator database has a database encryption key that is created during its installation. This key is generated using a random passphrase. When a full database backup is performed, the key is backed up with the database. Likewise, the key is restored when the database is restored.  

However, the encryption services also depend on the MS SQL Server Service Master Key. The service master key should be backed up and stored in a secure, off-site location. Creating this backup should be one of the first administrative actions performed on the server. [Learn more](/sql/t-sql/statements/backup-service-master-key-transact-sql).  

The database key is essentially paired with the service master key on the database server targeted by the installer. If either the database key or the service master key is lost, encrypted data stored in the data is likewise lost. This would include the license key, either entered by the user or an automatically created trial license.  

### Run a backup

To run a backup, follow these steps:

1. [Back up the service master key for Microsoft SQL Server](/sql/t-sql/statements/backup-service-master-key-transact-sql). This is a one\-time operation. Note that **password** is the password that will be used to protect the service master key in the file that is created. If the password is lost, the service master key can't be recovered from the file.  

    ```sql
    BACKUP SERVICE MASTER KEY TO FILE = 'path_to_file'  
                ENCRYPTION BY PASSWORD = 'password'  
    ```  

2. Back up the entire Orchestrator database. The backup may be performed when the system is running, but it's best to perform the backup when all runbook authors have checked in any pending changes to their runbooks. Pending changes are cached on the Runbook Designer and aren't backed up with a database backup.  

### Restore the database  

To restore the database, follow these steps:

1. If you're restoring to the same database server from which the backup was taken and the service master key hasn't changed, simply restore the backup.  
2. If you're restoring to a different database server with a different service master key, or you're restoring to the same database from which the backup was taken but the service master key has changed, the service master key must be restored to match the one used during the database backup. Use the procedure for [restoring the service master key for Microsoft SQL Server](/sql/t-sql/statements/restore-service-master-key-transact-sql). 

    ```sql
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_key'   
             ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597jheij4'  
    ```  

    > [!NOTE]  
    > If there are multiple databases using this service master key for encryption on your Microsoft SQL Server, all of these databases could be affected by this change. Consulting with your DBA before performing this administrative task is strongly recommended.  

3. Restore the database from the backup.  
4. On the Orchestrator Management Server, run the Data Store Configuration utility (`DBSetup`) from the Start menu.  
5. Provide the connection details to connect to the new database.
    > [!NOTE]
    > Don't use `localhost` or `.`. Explicitly specify the database server name and database name.  
6. Restart the Management Service.  
7. Run the Data Store Configuration utility on each Runbook Server. This utility isn't located in the Start menu on Runbook Servers. It can be found in `<OrchestratorInstallDir>\Management Server`.
    > [!NOTE]
    > For Runbook Servers installed on the same server as the Management Server one doesn't need to run the Data Store Configuration utility a second time. Running it once will update the configuration for both the Management Server and Runbook Server at the same time.  
8. Restart the Runbook Server\(s\).  
9. Follow the Web Components Recovery Process to update the Web Components to connect to the new database.  

## Next steps

- [Recover web components](how-to-recover-web-components.md).
- [Configure Orchestrator database connections](how-to-configure-orchestrator-database-connections.md).
