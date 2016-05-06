---
title: How to export a service template in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0aae8258-0c2f-416d-b39c-378957ea4a31
---
# How to export a service template in VMM
Use the following procedure to export a service template in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)].

**Account requirements** Administrators and delegated administrators can export any template in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. Self\-service users can export templates that they own.

### To export a service template

1.  In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, open the Library workspace.

2.  In the Library pane, expand the **Templates** node, click **Service Templates**, and then in the **Template** pane, select the service template that you want to export.

3.  On the **Service Template** tab, in the **Actions** group, click **Export**.

4.  In the **Export Template Resources** dialog box, do the following:

    -   To export physical resources associated with the service template \(for example, a virtual hard disk or an application package\), under the **Physical Resources** column, click **None**. In the **Select Resources** dialog box, select the physical resources that you want to export, and then click **OK**.

    -   Select the **Overwrite the existing export files** check box if you want to overwrite an earlier export file for any of the selected templates.

    -   Select the **Export any sensitive template settings** checkbox if you want to include sensitive data such as passwords, product keys, and application and global settings that are marked as secure. If you select this option, you can configure encryption for the sensitive settings. If you choose not to include sensitive settings, an administrator can provide the settings during template import or by updating the template after it is imported.

    -   To configure encryption for sensitive settings in the template, select the **Encrypt template settings** check box, and then enter an encryption password for the .XML file.

        > [!IMPORTANT]
        > To protect sensitive data, if you choose to export sensitive template settings, we strongly recommend that you use encryption.

    -   In the **Location** box, use the **Browse** button to select the folder where you want to store the exported service template. The location does not have to be a library share. However, we recommend that you store exported service templates in the library to ensure access for import. If you are a self\-service user, you might store the template on the user data path for your self\-service user role.

    After you make your selections, click **OK**.

5.  To verify that the service template export completed successfully, you can do the following:

    -   In the Jobs workspace or the Jobs window, verify that the **Export service template** job completed successfully.

    -   In **Windows Explorer**, verify that an .XML file with the name of the service template was saved in the folder that you specified.

    -   If you stored the exported service template on a library share, you can verify that the .XML file was added to physical library objects in the Library workspace. On the **Library** pane, navigate to the library share where you stored the exported service template. You should see an .XML file with the name of the service template.

## See Also
[Exporting and importing service templates in VMM](../Topic/Exporting-and-importing-service-templates-in-VMM.md)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

