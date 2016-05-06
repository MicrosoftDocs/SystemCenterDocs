---
title: How to configure the VMM library to support self-service users
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0e20064-169c-4024-ac70-e4ba605dc06e
---
# How to configure the VMM library to support self-service users
Use the following procedures to prepare the library to enable self\-service users to deploy virtual applications to a private cloud in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. To give all private cloud users access to prepared resources that are used widely in service deployment, create library shares to add as read\-only library shares on private clouds. To enable members of a self\-service user role to upload and share the physical resources that they use to create service templates and to deploy services, configure a user data path for their self\-service user role. For background information about configuring the library, see [Configuring the VMM library to support self-service users](./Configuring-the-VMM-library-to-support-self-service-users.md).

**Account requirements** All of these procedures must be performed by a [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] administrator. Delegated administrators can add library shares on library servers that are in the scope of their user role, can configure read\-only library shares on private clouds that they created, and can configure user data paths on self\-service user roles that they created. Only members of the local Administrators group can grant access permissions on their user data paths.

## Sharing physical resources with private cloud users
To share physical resources with self\-service users who deploy virtual machines and services to private clouds, you can add the resources to read\-only library shares for the private clouds. The resources on read\-only library shares for a private cloud are available to members of all self\-service user roles that have the private cloud in their scope. The resources can be used in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], but the files cannot be accessed directly through the file system and modified by self\-service users.

Use the read\-only library shares on private clouds to make prepared resources widely available. For example, VHDs, ISO images, and other resources that are assigned to self\-service user roles must be stored either on a read\-only library share for a private cloud that is associated with the self\-service user role or on the user data path for the self\-service user role. You might also store resources such as the Application Frameworks resources on these shares to enable self\-service users to configure templates and profiles with scripts that install the Microsoft Web Deployment tool during service deployment.

#### To create shares for read\-only resources for users

1.  In Windows Explorer, create a shared folder to store all resources that will be used by self\-service users who deploy services to private clouds. This folder will include read\-only library shares for private clouds, and it will include user data paths for self\-service user roles. For convenience, you can create the folder near your default library share so that it is easy to access when you manage library resources. For example, create the following folder:

    C:\\ApplicationData\\Virtual Machine Manager Cloud Resources

2.  Within that folder, create a folder to store the \\ApplicationFrameworks resources. Then share the folder so that you can add it as a library share. For example, create and share the following folder:

    C:\\ApplicationData\\Virtual Machine Manager Cloud Resources\\ApplicationFrameworks

    > [!IMPORTANT]
    > The shared folder cannot be in the path of the default library share. You cannot add a library share that is in the path of an existing library share.

3.  Copy the ApplicationFrameworks folder from your default library share to the share that you created for private cloud resources.

4.  Add the share to the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library:

    1.  In the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, open the **Library** workspace.

    2.  On the **Library** pane, expand **Library Servers**, and click the library server that contains the default library share.

    3.  On the **Library Server** tab, in the **Library Server** group, click **Add Library Shares**.

        The **Add Library Shares Wizard** opens.

    4.  On the **Add Library Shares** page, select each shared folder that you want to add to the library. For example, select ApplicationFrameworks, on the C:\\VMM Cloud Resources path.

    5.  On the **Summary** pane, click **Add Library Shares**.

5.  After the **Add library shares** job completes, on the **Library** pane, expand **Library Servers**, and then expand the node for the library server that contains your default library share. The node should display the new library share. You can expand the share node to see resources stored on the share.

#### To add read\-only library shares to a private cloud in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]

1.  Open the **VMs and Services** workspace.

2.  On the **VMs and Services** pane, expand clouds, and click the private cloud that you want to update.

3.  On the **Folder** tab, in the **Properties** group, click  **Properties**.

4.  In the **Properties** dialog box, open the **Library** tab.

5.  By **Read\-only library shares**, click **Add**.

6.  In the **Add Library Shares** dialog box, select each library share that you want to add to the read\-only library share for the private cloud, and tehn click **OK**.

7.  Click **OK** a second time to save the updates to the private cloud properties.

## Providing a place for self\-service users to store and share their resources
Use the following procedure to set up a user data path for a self\-service user role. The user data path enables members of a self\-service user role to upload and share the physical resources that they use to create service templates and to deploy services. Each self\-service user role has only one user data path for all private clouds that are in the scope of the user role. The user data path must be in a library share.

Access to the physical resources on a user data path is controlled through the file system. To enable members of a self\-service user role to use and share their own resources in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], grant Read\/Write permission on the folder to all role members.

In the **Library** workspace, self\-service users can see any resources for which they have permissions on the **Library** pane, in the **Self\-Service User Data** node. However, only members of a self\-service user role that has the **Author** action assigned to it can use the resources to create profiles and templates in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

To enable members of a self\-service user role to use their own application packages to create service templates and deploy services in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], configure a user data path for the self\-service user role and grant Read\/Write permission on the folder.

#### To create a folder for resources owned by a self\-service user role

1.  In Windows Explorer, create a folder to store all shared resources that will be used by self\-service users who deploy virtual machines and services to private clouds. For example, create the following folder:

    C:\\ProgramData\\Virtual Machine Manager Cloud Resources\\Self\-Service User Data

2.  Within that folder, create a subfolder to store resources for the self\-service user role. For example, create the following folder:

    C:\\ProgramData\\Virtual Machine Manager Cloud Resources\\Self\-Service User Data\\Finance Service Managers

3.  Within that folder, create a subfolder to store the application packages for all releases of the virtual application that you will use in this scenario; within that folder, create a subfolder to store the application package for the first release of the service. For example, create the following folder, where <MyApplication> is the name of the application that is being developed and managed through self\-service:

    C:\\ProgramData\\Virtual Machine Manager Cloud Resources\\Self\-Service User Data\\Finance Service Managers\\<MyApplication>\\<MyApplication v1>

4.  To enable members of the self\-service user role to access the resources and upload their own resources to the folder, grant all members Read\/Write permission on the folder.

5.  If needed, share the folder that contains user data for all self\-service user roles, and then add the share to the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library.

    To be assigned to a self\-service user role, a user data path must be on a library share.

### To configure a user role data path for a self\-service user role

1.  Open the **Settings** workspace.

2.  On the **Settings** pane, expand **Security**, and click **User Roles**.

3.  On the **User Roles** pane, click the self\-service user role. For example, click Finance Service Managers.

4.  On the **Home** tab, in the **User Role** group, click **Properties**.

5.  In the user role properties, open the **Resource** tab.

6.  In **Data path**, use the **Browse** button to select the folder that you created to store shared resources for members of the self\-service user role. For example, for the Finance Service Manager user role, you would select the following folder:

    C:\\ProgramData\\Virtual Machine Manager Cloud Resources\\Self\-Service User Data\\Finance Service Managers

7.  Click **OK** to store the updates to the self\-service user role.

    After you save the user role, the data path is added to the **Library** workspace.

8.  To verify that the new data path has been added:

    1.  Open the **Library** workspace.

    2.  On the **Library** pane, expand **Self\-Service User Content**.

        You should see a node with the name of the self\-service user role \- for example, Finance Service Managers. Unless you have added yourself to the self\-service user role, you will not be able to see the physical resources that are stored in the folder.

## See Also
[Managing a self-service environment for tenants](./Managing-a-self-service-environment-for-tenants.md)
[Configuring the VMM library to support self-service users](./Configuring-the-VMM-library-to-support-self-service-users.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)
[Managing tenant resources in the VMM library](./Managing-tenant-resources-in-the-VMM-library.md)
[Managing the VMM library and its resources](./Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


