---
title: How to add a VMM library server or VMM library share
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb288be0-b213-4066-a0bb-dae7b439c645
---
# How to add a VMM library server or VMM library share
You can use the following procedures to add a library server and library shares to an existing Virtual Machine Manager (VMM) installation. When you add a library server to VMM management, VMM installs the VMM agent on the new library server.

> [!NOTE]
> During VMM Setup, you can either create a library share or specify an existing share. If you accept the default, a library share that is named MSSCVMMLibrary is created on the VMM management server.

**Account requirements** To add a library server, you must be a member of the Administrator user role or the Delegated Administrator user role. To add a library share, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the library server where the share is located.

## Prerequisites

-   To add a library server, the server must meet the operating system requirements described in [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Deploy/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

-   The library server that you want to add must be in the same domain as the VMM management server, or in a domain that has a two-way trust with the domain of the VMM management server (including domains with disjointed namespaces).

-   When you add a library server, the firewall on the server that you want to add must allow File and Print Sharing (SMB) traffic to enable VMM to enumerate and display the available shares.

-   When you add a library server or you add a library share to a library server that is already under VMM management, you must designate an existing share. Therefore, before you add a library server or library share, you must manually create the shared folder on the target server outside VMM.

    > [!IMPORTANT]
    > Do not create highly available file shares for the VMM library on the same cluster as a highly available VMM management server installation. VMM does not support this configuration.

    > [!NOTE]
    > For a library share to function through VMM, the minimum required permissions are that the Local System (SYSTEM) account has full control permissions at both the share and the NTFS file system level. By default, the Local System account has full control permissions when you create a file share and then add the library share to VMM management.
    > 
    > However, to add resources to a library share, an administrator typically needs to access the share through Windows Explorer. They can do this either outside VMM or through the VMM console, where they can right-click the library share, and then click **Explore**. Because of this, make sure that you assign the appropriate access control permissions outside VMM. For example, we recommend that you assign full control share and NTFS permissions to the Administrators group.

-   When you add a library server, you must specify account credentials for a domain account that has administrative rights on the computers that you want to add. You can enter a user name and password or specify a Run As account. If you want to use a Run As account, you can create the Run As account before you begin this procedure, or create it during the procedure.

    > [!NOTE]
    > You can create Run As accounts in the **Settings** workspace. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

#### To add a library server

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Add** group, click **Add Library Server**.

    The Add Library Server wizard opens.

3.  On the **Enter Credentials** page, enter the credentials for a domain account that has administrative rights on the servers that you want to add, and then click **Next**. You can specify a Run As account or manually enter user credentials in the format *domain_name*\\*user_name*.

    > [!NOTE]
    > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

4.  On the **Select Library Servers** page, do the following:

    1.  In the **Domain** box, enter the name of the domain that the server belongs to.

    2.  In the **Computer name** box, enter the name of the server that you want to add. If you are not sure of the computer name, click **Search**, and then enter the search criteria.

        For example, enter the name of the library server in New York, **NYLibrary01**.

    3.  If you want to skip Active Directory name verification, select the **Skip Active Directory name verification** check box.

    4.  Click **Add** to add the server to the **Selected servers** area.

    5.  To add more library servers, repeat steps 4a through 4c. When you are finished, click **Next**.

5.  On the **Add Library Shares** page, select the check box next to each library share that you want to add. If you want to add the default library resources to the share that are used for services, select the **Add Default Resources** check box.

    > [!NOTE]
    > If you add the default resources, this adds the ApplicationFrameworks folder to the library share. Resources in the ApplicationFrameworks folder include the Microsoft Web Deployment tool, and scripts that you can add to application profiles in service templates to install Web applications during service deployment. If you add the default resources to multiple library shares, the files are automatically grouped as equivalent resources because of matching family names, release values, and namespace.

    When you are finished, click **Next**.

    For example, select the check box next to the **NYLibrary** share on the **NYLibrary01** library server.

6.  On the **Summary** page, review the settings, and then click **Add Library Servers**.

    The **Jobs** dialog box appears. Make sure that the job indicates that the library server was successfully added, and then close the dialog box.

7.  To verify that the library server and shares were added, in the **Library** pane, expand the **Library Servers** node.

    Verify that the library servers and shares are listed.

#### To add a library share

1.  Open the **Library** workspace.

2.  In the **Library** pane, expand **Library Servers**, and then click the library server where you want to add the share.

3.  On the **Library Server** tab, click **Add Library Shares**.

4.  On the **Add Library Shares** page, select the check box next to each library share that you want to add, and then click **Next**. If you want to add the default library resources to the share that are used for services, select the **Add Default Resources** check box.

    > [!NOTE]
    > If you add the default resources, this adds the ApplicationFrameworks folder to the library share. Resources in the ApplicationFrameworks folder include the Microsoft Web Deployment tool, and scripts that you can add to application profiles in service templates to install Web applications during service deployment. If you add the default resources to multiple library shares, the files are automatically grouped as equivalent resources because of matching family names, release values, and namespace.

5.  On the **Summary** page, review the settings, and then click **Add Library Shares**.

    The **Jobs** dialog box appears. Make sure that the job indicates that the library shares were successfully added, and then close the dialog box.

6.  To verify that the new library shares were added, in the **Library** pane, expand the **Library Servers** node, and then expand the library server where you added the share.

    Verify that the library shares appear under the library server name.

## See Also
[How to associate a VMM library server with a host group](How-to-associate-a-VMM-library-server-with-a-host-group.md)
[How to add file-based resources to the VMM library](How-to-add-file-based-resources-to-the-VMM-library.md)
[How to create or modify equivalent objects in the VMM library](How-to-create-or-modify-equivalent-objects-in-the-VMM-library.md)
[How to view and remove orphaned resources in VMM](How-to-view-and-remove-orphaned-resources-in-VMM.md)
[Configuring the VMM library](Configuring-the-VMM-library.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


