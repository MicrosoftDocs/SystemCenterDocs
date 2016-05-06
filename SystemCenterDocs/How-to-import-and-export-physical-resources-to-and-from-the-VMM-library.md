---
title: How to import and export physical resources to and from the VMM library
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36e7924e-5476-450e-8b76-fd12eb8ad281
---
# How to import and export physical resources to and from the VMM library
You can use the following procedures to import and export file\-based resources between library servers and library shares in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. This functionality also enables you to transfer files between library servers that are associated with different [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management servers.

This is the recommended method for self\-service users to import and export physical resources to and from the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library. This is especially true if the self\-service user does not have permissions set outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] to access private cloud library shares or their user role data path through Windows Explorer.

**Account requirements** You must be a member of the Administrator, Delegated Administrator, or Self\-Service user role with the **Author** permission to complete these procedures. Delegated administrators can only import and export resources to and from library locations that are within the scope of their user role. Self\-service users can only import resources to their user role data path in the Self Service User Content node of the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library. Self\-service users can export resources that are available in their user role data path and in their private cloud library shares.

### To import physical resources

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Import** group, click **Import Physical Resource**.

3.  In the **Import Library Resources** dialog box, click either of the following:

    -   **Add custom resource**

        This option enables you to import a folder and its contents. You can select a folder that has a .CR extension to import the folder as a custom resource package. Or, you can select a folder without a .CR extension that contains one or more files of a supported file type. If you select a folder without a .CR extension, only the files of a supported file type will appear in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library. However, if you use Windows Explorer to access the library share, you can access all files in the folder depending on the file and share permissions that are configured outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

        > [!TIP]
        > If the folder with .CR extension contains more than one hundred files to be imported, it is recommended that you zip the files before the import. This will improve performance.

    -   **Add resource**

        This option enables you to import one or more files of a supported type to another library location. For information about the supported file types, see the table in the “File\-based resources” section of [Configuring the VMM library](./Configuring-the-VMM-library.md).

4.  If you are an administrator or a delegated administrator, after you have selected the desired resources, under **Select library server and destination for the imported resources**, click **Browse**. Then, click the desired library server, the library share, and optionally, the desired folder location, and then click **OK**.

5.  When you are finished, click **Import**.

    To verify that the resources were imported, if you are an administrator or a delegated administrator, under **Library Servers**, locate and then click the target location. In the **Physical Library Objects** pane, make sure that the resources are listed.

    If you are a self\-service user, expand **Self Service User Content**, and then click the user role data path. In the **Self Service User Objects** pane, make sure that the resources are listed.

### To export physical resources

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Export** group, click **Export Physical Resource**.

3.  In the **Export Library Resources** dialog box, click **Add**.

    All physical library resources in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library that the user has access to are listed.

    > [!TIP]
    > You can right\-click the column header to select which columns appear.

4.  Select the physical resources that you want to export, and then click **OK**. \(To select multiple resources, press and hold the CTRL key, and then click each resource. To select a range, click the first resource in the range, press and hold the SHIFT key, and then click the last resource in the range.\)

5.  Under **Specify a destination for the export files**, click **Browse**. In the **Browse for Folder** dialog box, click a destination folder, and then click **OK**.

6.  When you are finished, click **Export**.

## See Also
[Managing a self-service environment for tenants](./Managing-a-self-service-environment-for-tenants.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)
[Managing tenant resources in the VMM library](./Managing-tenant-resources-in-the-VMM-library.md)
[Managing the VMM library and its resources](./Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](./Managing-fabric-resources-with-VMM.md)


