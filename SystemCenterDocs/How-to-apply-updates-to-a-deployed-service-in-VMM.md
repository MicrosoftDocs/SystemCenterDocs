---
title: How to apply updates to a deployed service in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e80340-0604-45ec-a581-72caa17b57c4
---
# How to apply updates to a deployed service in VMM
You can apply updates to a deployed service in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. To apply updates, first publish an updated service template and then use that updated service template to apply updates to the deployed service.

### To publish an updated service template

1.  In the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, open the Library workspace, expand the **Templates** node, and then click **Service Templates**.

2.  In the **Templates** pane that lists the available service templates, select the service template that you want to publish.

3.  On the **Service Template** tab, in the **Actions** group, click **Publish**.

    > [!NOTE]
    > If you no longer want to make the service template available, click **Revoke**.

4.  Open the VMs and Service workspace and find the service that you want to update with the updated service template. The **Update Status** column for the service should display **New Release Available**.

### To apply updates to a deployed service by using an updated service template

1.  In the VMs and Service workspace, select the service that you want to update with the updated service template.

2.  On the **Service** tab, in the **Update** group, click **Set Template**.

3.  In the Change Service Template wizard, on the **Updated Service Template** page, select **Replace the current template with an updated template for this service**.

    > [!NOTE]
    > Use the **Modify application settings for this service** option if you only need to change the setting of an application installed in the service. For example, if you need to change the name of the SQL Server database that an application is using.

4.  Click **Browse**, select the updated service template, click **OK**, and then click **Next**.

5.  On the **Settings** page, configure any application settings that are listed, and then click **Next**.

6.  On the **Update Method** page, select whether you want to make the updates in\-place to the existing virtual machines or whether you want to deploy new virtual machines with the updated settings, and then click **Next**.

    > [!NOTE]
    > For more information about these two update methods, see [Updating services in VMM](Updating-services-in-VMM.md).

7.  On the **Updates Review** page, review your selections, and then **Next**.

    > [!NOTE]
    > If you want the updates to be made immediately, select the **Apply the changes to the service immediately after this wizard completes** check box.

8.  On the **Summary** page, review the settings, and then click **Finish**.

9. When you are ready to apply the updates to the deployed service \(for example, during a regularly scheduled maintenance windows\), in the VMs and Service workspace, select the service that you want to update.

10. On the **Service** tab, in the **Upgrade** group, click **Apply Template**.

11. In the **Apply Service Template** dialog box, review the updates that will be made, and then click **OK**.

    You can track the progress of the service being updated in the Jobs window. A **Perform servicing on a service** job is created.

12. After the update job has completed, in the VMs and Services workspace, verify that the **Template Release** value for the service has been updated.

## See Also
[Updating services in VMM](Updating-services-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


