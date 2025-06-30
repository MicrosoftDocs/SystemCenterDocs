---
title: Import data from Active Directory Domain Services
description: This article provides an overview of using a connector to import data from Active Directory Domain Services (AD DS) into Service Manager and it also describes how to create, synchronize, and enable or disable an Active Directory connector.
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: d039eac3-e5cd-4f11-ac6c-bb856bafcc92
ms.custom: UpdateFrequency3, engagement-fy24
---

# Import data from Active Directory Domain Services

The Service Manager database in Service Manager contains information about your enterprise, and it's used by all the parts of your service management structure. You can use an Active Directory connector to add users, groups, printers, and computers (and only these object types) as configuration items into the Service Manager database.

> [!NOTE]
> If the same user name exists in two different organizational units (OUs) within the Active Directory domain, Service Manager can't import both user accounts, and an event is logged in the System Center Operations Manager application log.

In addition, when you configure an Active Directory connector to import data from an Active Directory group, you can select an option to automatically add users from the Active Directory group. When they're selected, any users that are added to the Active Directory group will be automatically added to the Service Manager database. If those users are removed from the Active Directory group, they'll remain in the Service Manager database; however, they'll reside in the Deleted Items group.

When you've created an Active Directory connector, **Select objects** in the connector can't be updated. Instead, you create security groups in Active Directory that map to User Roles in Service Manager. For example, you can create a Security Group in Active Directory Domain Services (AD DS) named Incident Resolvers. In Service Manager, you can assign this security group to the Incident Resolvers user role. When you create the Active Directory connector and you select **Automatically add users of AD Groups imported by this connector**, when a user who is a member of the Incident Resolvers security group starts the Service Manager console, they'll be granted Incident Resolver rights and permissions.

If you're importing data from several OUs or subdomains, you've the option of creating a Lightweight Directory Access Protocol (LDAP) query that specifies computers, printers, users, or user groups to import with the connector. For example, an LDAP filter of all objects that are in either Dallas or Austin and that have the first name of John looks like `(&(givenName=John) (|(l=Dallas) (l=Austin)))`. You can test your queries, and all errors must be corrected before you can configure the Active Directory connector. For more information about LDAP queries, see [Search Filter Syntax](/windows/win32/adsi/search-filter-syntax).

If you must later perform maintenance operations on the Service Manager database, you can temporarily disable the connector and suspend the importation of data. Later, you can resume the importation of data by re-enabling the connector.

When you import a large number of users from AD DS) or from Configuration Manager, CPU utilization might increase to 100 percent. You'll notice this on one core of the CPU. For example, if you import 20,000 users, CPU utilization might remain high for up to an hour. You can mitigate this issue by creating connectors and importing the users into Service Manager before you deploy the product in your enterprise and by scheduling connector synchronization during off hours. Installing Service Manager on a computer that has a multi-core CPU also minimizes the impact of importing a large number of users.

## Create an Active Directory connector

You can use the following procedures in Service Manager to create, validate, and confirm the status of an Active Directory connector to import objects from Active Directory Domain Services (AD DS).

::: moniker range=">=sc-sm-2019"

>[!NOTE]
> The Active Directory (AD) connector has been improvised to synchronize with a specific domain controller. You may specify the Domain Controller in the LDAP query of the Active Directory connector.

::: moniker-end

### Create an Active Directory connector and import objects from AD DS

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, under **Connectors**, select **Create Connector**, and select **Active Directory Connector**.

4. Complete these steps in the Active Directory Connector Wizard:

    1. On the **Before You Begin** page, select **Next**.

    2. On the **General** page, in the **Name** box, enter a name for the new connector. Ensure that the **Enable this connector** checkbox is selected, and select **Next**.

    3. On the **Domain or organizational unit** page, select **Use the domain: _domain name_**. Or select **Let me choose the domain or OU**, and then select **Browse** to choose a domain or an organizational unit (OU) in your environment.

    4. In the **Credentials** area, select **New**.

    5. In the **Run As Account** dialog, in the **Display name** box, enter a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to read from AD DS, and select **OK**. On the **Domain or organizational unit** page, select **Test Connection**.

        > [!NOTE]
        > Special characters (such as the ampersand [&]) in the **User Name** box aren't supported.

    6. In the **Test Connection** dialog, ensure that **The connection to the server was successful** is displayed, and select **OK**. On the **Domain or organizational unit** page, select **Next**.

    7. On the **Select objects**, do the following:

        1. Select **All computers, printers, users, and user groups** to import all items or,

        2. Select **Select individual computers, printers, users or user groups** to import only the selected items or,

        3. Select **Provide LDAP query filters for computers, printers, users, or user groups** if you want to create your own Lightweight Directory Access Protocol (LDAP) query.

        If you want new users that are added to any groups you import to be added automatically to Service Manager, select **Automatically add users of AD Groups imported by this connector**, and select **Next**.

    8. On the **Schedule** page, in the **Synchronize** list, set the frequency and time of synchronization, and select **Next**.

    9. On the **Summary** page, ensure that the settings are correct, and select **Create**.

    10. On the **Completion** page, ensure that you receive the following confirmation message:

        *Active Directory connector successfully created.*

        Then, select **Close**.

        > [!NOTE]
        > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### Validate the creation of an Active Directory connector

1. In the **Connectors** pane, locate the Active Directory connector that you created. You might have to wait for a minute before the connector appears.

2. In the **Connectors** pane, review the **Status** column for a status of **Finished Success**.

3. In the **Configuration Items** pane, expand **Configuration Items**. Expand **Computers** and **All Windows Computers**, and verify that the intended computers from AD DS appear in the **All Windows Computers** pane. Expand **Printers**, expand **All Printers**, and then verify that the intended printers from AD DS appear in the **All Printers** pane.

4. In the Service Manager console, select **Configuration Items**. In the **Configuration Items** pane, select **Users**, and then verify that the intended users and user groups from AD DS appear in the **Users** pane.

### Confirm the status of an Active Directory connector

- View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of imported configuration items.

![PowerShell symbol](./media/import-data-ads/pssymbol.png)You can use a Windows PowerShell command to create a new Service Manager Active Directory connector. For information about how to use Windows PowerShell to create a new Service Manager Active Directory connector, see [New-SCADConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316255(v=sc.20)).

## Synchronize an Active Directory Connector

To ensure that the Service Manager database is up to date, the Active Directory connector synchronizes with Active Directory Domain Services (AD DS) every hour after the initial synchronization. However, you can use the following procedure to manually synchronize the connector and validate that it's synchronized.

### Manually synchronize an Active Directory connector

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Active Directory connector that you want to synchronize.

4. In the **Tasks** pane, under the name of the connector, select **Synchronize Now**.

    > [!NOTE]
    > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### Validate that an Active Directory connector synchronized

1. In the Service Manager console, select **Configuration Items**.

2. In the **Configuration Items** pane, expand **Printers**, and select **All Printers**. Verify that any new printers in AD DS appear in the middle pane.

3. Expand **Computers**, and select **All Windows Computers**. Verify that any new computers in AD DS appear in the middle pane.

4. In the Service Manager console, select **Configuration Items**.

5. In the **Configuration Items** pane, select **Users**. Verify that any new users and groups in AD DS appear in the middle pane.

## Disable and enable an Active Directory connector

You can use the following procedure to disable or enable an Active Directory connector in Service Manager and validate its change in status.

### Disable an Active Directory connector

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Connectors** pane, select the Active Directory connector that you want to disable.

4. In the **Tasks** pane, under the connector name, select **Disable**.

5. In the **Disable Connector** dialog, select **OK**.

### Enable an Active Directory connector

1. In the Service Manager console, select **Administration**, and select **Connectors**.

2. In the **Connectors** pane, select the Active Directory connector that you want to enable.

3. In the **Tasks** pane, under the connector name, select **Enable**.

4. In the **Enable Connector** dialog, select **OK**.

### Validate the status change of an Active Directory connector

1. After you enable or disable an Active Directory connector, wait for about 30 seconds. Then, in the Service Manager console, select **Administration**, and select **Connectors**.

2. In the middle pane, locate the connector for which you've changed status, and then verify the value in the **Enabled** column.

![PowerShell symbol](./media/import-data-ads/pssymbol.png)You can use Windows PowerShell commands to complete these tasks and other related tasks, as follows:

- For information about how to use Windows PowerShell to start a Service Manager connector, see [Start-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316244(v=sc.20)).

- For information about how to use Windows PowerShell to retrieve connectors that are defined in Service Manager and view their status, see [Get-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316209(v=sc.20)).

- For information about how to use Windows PowerShell to update properties of a Service Manager connector, see [Update-SCSMConnector](/previous-versions/system-center/powershell/system-center-2012-r2/hh316217(v=sc.20)).

## Import data from other domains

You can import data from domains other than the domain in which Service Manager resides. For example, Service Manager is installed in domain A (where the fully qualified domain name [FQDN] is a.woodgrove.com), and you want to import data from domain B (where the FQDN is b.woodgrovetest.net). In this scenario, you must think about how to specify the data source path and how to specify the Run As account.

In domain B, either identify an existing service account or create a new one for this purpose. This service account must be a domain account and must be able to read from Active Directory Domain Services.

Next, in Service Manager, create a new Active Directory connector in the Active Directory Connector Wizard. Follow these steps on the **Domain or organizational unit** page.

### Specify the data source path and Run As account

1. Use the appropriate method according to where the domains are located:

    - If the two domains are in the same forest, in the **Server Information** area, select **Let me choose the domain or OU**, and select **Browse** to select the domain and organizational unit (OU).

    - If the two domains are in different forests, in the **Server Information** area, select **Let me choose the domain or OU**, and then enter the domain and OU in the box. For example, enter **LDAP://b.woodgrovetest.net/OU=*OU Name*,DC=b,DC=woodgrovetest,DC=net**.

2. In the **Credentials** area, select **New**.

3. In the **Run As Account** dialog, in the **User name**, **Password**, and **Domain** boxes, enter the credentials for the service account from the b.woodgrovetest.net domain.

    > [!NOTE]
    > If the two domains are in different forests, you must enter the domain name in the **User name** box. For example, enter `b.woodgrovetest.net\UserName`.

## Next steps

- Lean about how to [Import data and alerts from Operations Manager](import-data-om.md).
