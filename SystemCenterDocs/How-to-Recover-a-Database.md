---
title: How to Recover a Database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8d559d9-2bf9-4d2e-a11c-37cf292c2782
---
# How to Recover a Database
The Orchestrator database can be backed up and restored using most standard MS SQL Server database backup\/restore mechanisms. This includes Microsoft SQL Server Backup, DPM SQL Server backup, and others. Orchestrator provides a VSS Writer that will discover the database server that is associated with the Management Server and back up the database when the Management Server is backed up.

However, there are a few key considerations when restoring.

## Orchestrator Cryptography
System Center 2012 Orchestrator provides a set of services for encryption and decryption of runbook properties and published data. These services are based on Microsoft SQL Server 2008 R2 cell\-level encryption. The Orchestrator database has a database encryption key that is created during its installation. This key is generated using a random passphrase. When a full database backup is performed, the key is backed up with the database. Likewise, the key is restored when the database is restored.

However, the encryption services also depend on the MS SQL Server Service Master Key. The service master key should be backed up and stored in a secure, off\-site location. Creating this backup should be one of the first administrative actions performed on the server. The procedure for doing this is documented for [Microsoft SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=249148) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=249148\).

The database key is essentially paired with the service master key on the database server targeted by the installer. If either the database key or the service master key is lost, encrypted data stored in the data is likewise lost. This would include the license key, either entered by the user or an automatically created trial license.

#### To perform a backup

1.  Back up the Microsoft SQL Server service master key using the procedure for [backing up the service master key for Microsoft SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=249148). This is a one\-time operation. Note "password" is the password that will be used to protect the service master key in the file that is created. If the password is lost, the service master key cannot be recovered from the file.

    ```
    BACKUP SERVICE MASTER KEY TO FILE = ‘path_to_file’
                ENCRYPTION BY PASSWORD = ‘password’
    ```

2.  Back up the entire Orchestrator database. The backup may be performed when the system is running, but it is best to perform the backup when all runbook authors have checked in any pending changes to their runbooks. Pending changes are cached on the Runbook Designer and are not backed up with a database backup.

#### To restore the database

1.  If you are restoring to the same database server from which the backup was taken, and the service master key has not changed, simply restore the backup.

2.  If you are restoring to a different database server with a different service master key, or you are restoring to the same database from which the backup was taken but the service master key has changed, the service master key must be restored to match the one used during the database backup. Use the procedure for [restoring the service master key for Microsoft SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=249149) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=249149\).

    ```
    BACKUP SERVICE MASTER KEY TO FILE = ‘c:\temp_backups\keys\service_master_key’ 
             ENCRYPTION BY PASSWORD = ‘3dH85Hhk003GHk2597jheij4’
    ```

    > [!NOTE]
    > If there are multiple databases using this service master key for encryption on your Microsoft SQL Server, all of these databases could be affected by this change. Consulting with your DBA before performing this administrative task is strongly recommended.

3.  Restore the database from the backup.

4.  On the Orchestrator Management Server, run the Data Store Configuration utility from the Start menu.

5.  Provide the connection details to connect to the new database. Note: Do not use "localhost" or ".". Explicitly specify the database server name and database name.

6.  Restart the Management Service.

7.  Run the Data Store Configuration utility on each Runbook Server. This utility is not located in the Start menu on Runbook Servers. It can be found in <SC2012OrchestratorInstallDir>\\Microsoft System Center 2012\\Orchestrator\\Runbook Server. Note: For Runbook Servers installed on the same server as the Management Server one doesn't need to run the Data Store Configuration utility a second time. Running it once will update the configuration for both the Management Server and Runbook Server at the same time.

8.  Restart the Runbook Server\(s\).

9. Follow the Web Components Recovery Process to update the Web Components to connect to the new database.

