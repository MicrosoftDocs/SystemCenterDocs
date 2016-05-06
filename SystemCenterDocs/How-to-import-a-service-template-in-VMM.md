---
title: How to import a service template in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5673c1e-5792-4210-acb9-327f5ccafadc
---
# How to import a service template in VMM
Use the following procedure to import a service template in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)].

### To import a service template

1.  In the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, open the Library workspace.

2.  In the Library pane, expand the **Templates** node, and then click **Service Templates**.

3.  On the **Home** tab, in the **Import** group, click **Import Template**.

4.  In the Import Package wizard, on the **Select Package** page, do the following:

    1.  In **Package path**, use the **Browse** button to select the .XML file for the exported service template that you want to import. The .XML file will have the name of the service template

    2.  If you want to import sensitive settings such as passwords, product keys, and application and global settings that are marked as secure, select the **Import sensitive template settings** check box. If you do not want to import sensitive data, you can update the references during the template import.

5.  After you have made your selections, click **Next**.

    If sensitive data was encrypted when the service template was exported, and you chose to import the sensitive data, a **Password** dialog box opens

6.  In the **Password** box, enter the encryption password that was used to encrypt sensitive data when the service template was exported, and then click **OK**.

7.  On the **Configure References** page, do the following:

    -   In the **Name** box, enter a name for the service template. If you are restoring a service template, keep the same service template name.

    -   In **Release** box, provide a release value for the service template. If you are restoring a service template, keep the same release value.

    -   Review the list of logical and physical resources that the service template references to identify any missing resources.

        In the resource list, each missing resource has a **Current Mapping** value of **None**. The most common missing resources are logical networks and virtual hard disks.

    -   If necessary, update missing logical or physical resources to a resource that is available in the current [!INCLUDE[vmm12short](Token/vmm12short_md.md)] environment.

        To update a resource, click the pencil icon at the right end of the resource entry to display a list of available resources. After you select a new resource, the **Current Mapping** for the resource displays the selected resource.

        > [!NOTE]
        > You can import a template that references missing resources and update the resource references later.

    After you finish updating references, click **Next**.

8.  If the name and the release value match those of an existing service template in the current [!INCLUDE[vmm12short](Token/vmm12short_md.md)] environment, you will be prompted to confirm whether you want to overwrite settings in the existing service template. Click **Yes** to continue, or cancel the operation and then change the service template name or release value.

9. On the **Summary** page, review your selections, and then click **Import**.

10. To verify that the service template was imported successfully, you can do the following:

    -   In the Jobs workspace, verify that the **Import template** job completed successfully.

    -   In the Library workspace, In the **Library** pane, expand **Templates**, and then click **Service Templates**. The **Templates** pane should display the new service template. The **Status** should be **OK**.

        > [!NOTE]
        > If any unavailable resources were not mapped, the template status is **Missing**. To review errors in a service template, open the service template in the Service Template Designer.

## See Also
[Exporting and importing service templates in VMM](Exporting-and-importing-service-templates-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


