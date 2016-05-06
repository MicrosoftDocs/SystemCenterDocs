---
title: Configure self-service recovery of SQL Server databases
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e47202e-3cc4-400b-8b4c-cdb52b820da6
---
# Configure self-service recovery of SQL Server databases
[!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)] includes the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Self\-Service Recovery Configuration Tool for SQL Server \(SSRCT\), which is installed on the DPM server and accessed from the **Protection** task area in DPM Administrator Console. You can use this tool to create, modify, or delete DPM roles, which specify which users can perform self\-service recovery of protected SQL Server databases that they own.

You set up self\-service recovery by creating a role. You can then manage these roles as required. When you create a role you specify the following settings:

-   **Security groups**: One or more security groups that contain the users for whom you want to enable self\-service recovery of SQL Server databases.

-   **Recovery items**: Instances of SQL Server and SQL Server databases that are currently protected by [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] for which you want to enable self\-service recovery by users.

-   **Recovery targets**: Instances of SQL Server that users can use as targeted locations to recover databases during self\-service recovery.

### To create a DPM role by using the DPM Self\-Service Recovery Configuration Tool

1.  In DPM Administrator Console, go to the **Protection** view, and then click **Configure self service recovery**.

    The DPM Self\-Service Recovery Configuration Tool for SQL Server opens.

2.  To create a new DPM role, click **Create Role**.

3.  The Create New Role Wizard opens and guides you through the following pages to create a DPM role:

    -   On the Security Groups page, click **Add** and type in a security group in the format *domain\\security group*, or an individual user in the format *domain\\user name*. You can add multiple groups and users to a DPM role.

    -   On the Recovery Items page, to specify an instance of SQL Server as a recovery item, click **Add**, and then type the instance name in the following format, <computer name\\instance name>, and optionally, to specify an SQL Server database, press the TAB key, and then type a database name, or to enable users of this role to recover all databases on the instance, press the TAB key, and then press the Spacebar to clear the text in the **Database Name** column.

        Note that when you enable users of a DPM role to recover all SQL Server databases on an instance of SQL Server, those users can also recover any SQL Server databases that are subsequently added to the instance. When you enable access by using DPM roles, ensure that all members of the role have been granted appropriate permission to view and access all databases.

    -   On the Recovery Target Locations page, specify one or more recovery target locations and file paths to restrict where users of this DPM role can recover the files for their specified databases. You do not need to specify recovery target locations or paths for users of this DPM role to recover their SQL Server databases files. If you do not restrict the recovery target locations, at the time of recovery, the users can recover database files to any location for which they have write permission. However, users cannot overwrite the original database files, and the DPM Self\-Service Recovery Tool \(SSRT\) for SQL Server blocks them if they attempt to do so. If you do not want to specify recovery target locations for users, leave the **Allow users to recover the databases to another instance of SQL Server** check box clear, and then click **Next.**. You can specify multiple instances of SQL Server.

        To restrict the locations to which users can recover SQL Server database files, select the **Allow users to recover the databases to another instance of SQL Server** check box, click **Add**, and then type an instance of SQL Server in the **SQL Server Instance** column, and optionally type a path in the **Recovered File Path** column where users of this role can recover their SQL Server database files, or to enable users to recover to any path on the instance, press the TAB key, and then press the Spacebar to clear the text in the **Recovered File Path** column.If all of the users for this role are SQL Server database administrators, you might want to enable them to recovery their database files to any location on an instance of SQL Server. However, if the users are not SQL Server administrators, you might want to restrict the locations to which they can recover the database files so that they do not affect the functioning of other SQL Server databases.

### To create a DPM role using PowerShell

1.  Create a DPM role.

    > [!IMPORTANT]
    > To create a DPM role, all of the following commands must be run in the following order.

    ```
    New-DPMRole -Name <NewDMPRoleName> -DPMServerName <DPMServerName> [-Description <DPMRoleDescription>] [<CommonParameters>]
    ```

2.  Specify the individual users or security groups that contain the users for whom you want to enable self\-service recovery of SQL Server databases.

    ```
    Add-DPMSecurityGroup -SecurityGroups <SecurityGroupsToAddToDPMRole> -DpmRole <DPMRoleName> [<CommonParameters>]
    ```

    > [!NOTE]
    > Specified users can recover their SQL Server databases regardless of the database permissions configured on the instances of SQL Server.

3.  Specify the instances of SQL Server and SQL Server databases that are currently protected by DPM for which you want to enable self\-service recovery by users.

    ```
    Add-DPMRecoveryItem -Datasources <SQLServerDatabaseName> -Type SQLDatabase -DpmRole <DPMRoleName> [<CommonParameters>]
    ```

    \-Or\-

    ```
    Add-DPMRecoveryItem -SQLInstances <SQLDataSource> -Type SQLInstance -DpmRole <DPMRole> [<CommonParameters>]
    ```

4.  Identify and add the instances of SQL Server that users can use as targeted locations to recover databases during self\-service recovery.

    1.  Create a recovery target object.

        ```
        New-DPMRecoveryTarget -Type SQLInstance or SQLDatabase -RecoveryTarget <ComputerName\InstanceName> -RecoveredFilesPath <FilePath> [<CommonParameters>]
        ```

    2.  Add the recovery target object to the role.

        ```
        Add-DPMRecoveryTarget -DpmRole <DMPRoleName> -RecoveryTargets <TargetRecoveryTargetName> [<CommonParameters>]
        ```

5.  Save the new DPM role.

    ```
    Set-DPMRole -DpmRole <DMPRoleName> -Confirm [<CommonParameters>]
    ```

You can modify or delete a DPM role you created, as follows:

### To modify a DPM role by using the DPM Self\-Service Recovery Configuration Tool

1.  In DPM Administrator Console, go to the **Protection** view, and then click **Self service recovery**.

    The DPM Self\-Service Recovery Configuration Tool for SQL Server opens.

2.  To modify a DPM role, select the role, and then click **Modify**.

### To rename a DPM role by using DPM Management Shell cmdlets

1.  Open the DPM role for editing.

    ```
    Get-DPMRole -Name <DMPRoleName> -DPMServerName <DPMServerName> -Editable <SwitchParameter> [<CommonParameters>]
    ```

2.  Rename the DPM role.

    ```
    Rename-DPMRole -Name <NewDMPRoleName> [-Description <DPMRoleDescription>] -DpmRole <DPMRoleName> [<CommonParameters>]
    ```

    > [!NOTE]
    > Users in the specified security groups can recover their SQL Server databases regardless of the database permissions configured on the instances of SQL Server.

3.  Save the modified DPM role.

    ```
    Set-DPMRole -DpmRole <DMPRoleName> -Confirm [<CommonParameters>]
    ```

### To remove a recovery target location

1.  Open the DPM role for editing.

    ```
    Get-DPMRole -Name <DMPRoleName> -DPMServerName <DPMServerName> -Editable <SwitchParameter> [<CommonParameters>]
    ```

    > [!NOTE]
    > The fully qualified domain name \(FQDN\) is required when removing a targeted location.

2.  Remove the recovery target location.

    ```
    Remove-DPMRole -DpmRole <DMPRoleName> [<CommonParameters>]
    ```

3.  Save the modified DPM role.

    ```
    Set-DPMRole -DpmRole <DMPRoleName> -Confirm [<CommonParameters>]
    ```

### To delete a DPM role by using the DPM Self\-Service Recovery Configuration Tool

1.  In DPM Administrator Console, go to the **Protection** view, and then click **Self service recovery** .

    The DPM Self\-Service Recovery Configuration Tool for SQL Server opens.

2.  To delete a DPM role, select the role, and then click **Delete**.

### To delete a DPM role by using DPM Management Shell cmdlets

1.  Open the DPM role.

    ```
    Get-DPMRole -Name <DMPRoleName> -DPMServerName <DPMServerName> -Editable <SwitchParameter> [<CommonParameters>]
    ```

2.  Delete the DPM role.

    ```
    Remove-DPMRole -DPMRole <DMPRoleName> [<CommonParameters>]
    ```


