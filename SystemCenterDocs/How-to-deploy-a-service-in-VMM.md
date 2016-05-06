---
title: How to deploy a service in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 609585a9-f7d4-48fe-9011-1e395c41538d
---
# How to deploy a service in VMM
Use the following procedures to deploy a service to a private cloud or to a host group in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. You can initiate service deployment from the Library workspace, from the Service Template Designer, or from the VMs and Services workspace.

### To deploy a service from the Library workspace

1.  In the Library workspace, expand the **Templates** node, and then click **Service Templates**.

2.  In the **Templates** pane that lists the available service templates, select the service template that you want to use to deploy the service.

    > [!NOTE]
    > For information about service templates, see [Creating service templates in VMM](Creating-service-templates-in-VMM.md).

3.  On the **Service Template** tab, in the **Actions** group, click **Configure Deployment**.

4.  In the **Select name and destination** dialog box, do the following:

    1.  In **Name** box, enter a name for the service instance. For example, enter **Corporate Finance Application**.

    2.  In **Destination**, select the host group or private cloud where you want to deploy the service.

    After you have made your selections, click **OK**.

5.  [!INCLUDE[vmm12short](Token/vmm12short_md.md)] performs a placement check to determine the best location on which to deploy the service and then opens the **Deploy Service** window.

    The **Deploy Service** window contains the following areas:

    -   In the left pane, the **Service Components** tab lists the tiers of the service and each instance of a tier that will be deployed.

    -   In the left pane, the **Settings** tab displays the global settings that will be used during application deployment. The contents of the **Settings** tab varies depending on the scripts that are configured for the service.

    -   In the center pane, a deployment map shows the recommended deployment location for each tier and each instance of a tier that will be deployed as part of the service. If you are deploying the service to a host group, the recommended host for each virtual machine to be deployed will be shown. If you are deploying the service to a private cloud, the host information is not shown.

    -   In the right pane, the **Minimap** tab allows you to adjust the size of the contents in the deployment map. This is intended to help you navigate the deployment map for a service that is made up multiple tiers.

    Review the deployment configuration settings. For more information about making changes, see [How to configure deployment settings for a service](How-to-configure-deployment-settings-for-a-service.md).

6.  If the placement process encounters an issue, an icon \(error, warning or informational\) will appear on the element of the service that needs attention and a message will appear in the details pane. Resolve any errors that are identified in the deployment configuration, and review warnings to resolve any conditions that need attention. You cannot deploy a service until all errors are resolved.

7.  To deploy the service, on the **Home** tab, in the **Service** group, click **Deploy Service**. Then, in the **Deploy service** dialog box, click **Deploy** to begin the deployment of the service.

    > [!NOTE]
    > If you close the **Deploy Service** window before you deploy the service, you will be prompted whether you want to save your deployment configuration settings for the service. If you click **Save**, you can deploy the service at a later time with the deployment configuration settings that you have already specified. To deploy the service at a later time, go to the Library workspace, expand the Templates node, and then click **Service Deployment Configurations**. Select the service that you saved, and then click **Configure Deployment**. The **Deploy Service** window will open.

8.  You can track the progress of the service deployment in the Jobs window.  A **Create service instance** job is created for a service deployment. For information about viewing a service after the service has been deployed, see [How to view and manage a deployed service](How-to-view-and-manage-a-deployed-service.md).

    > [!TIP]
    > Service deployment is a complex process that can take 15 minutes or longer. You can perform other tasks in the VMM console while you monitor the job.

### To deploy a service from the Service Template Designer

1.  In the Library workspace, expand the **Templates** node, and then click **Service Templates**.

2.  In the **Templates** pane that lists the available service templates, select the service template that you want to use to deploy the service.

3.  On the **Service Template** tab, in the **Actions** group, click **Open Designer**.

4.  In the Service Template Designer, on the **Home** tab, in the **Service Template** group, click **Configure Deployment**.

5.  Follow the steps described above for making selections in the **Select name and destination** dialog box, reviewing the deployment configuration settings, resolving any errors and warnings, and then deploying the service.

### To deploy a service from the VMs and Services workspace

1.  In the VMs and Services workspace, select the private cloud or host group to which you want to deploy the service.

2.  On the **Home** tab, in the **Create** group, click **Create Service**.

3.  In the **Create Service** dialog box, ensure **Use an existing service template** is selected, and then click **Browse**.

4.  In the **Select Service Template** dialog box, select the service template that you want to use, and then click **OK**.

5.  In the **Create Service** dialog box, enter the name for the service in the **Name** box, ensure that the correct location is specified in the **Destination** list, and then click **OK**.

6.  [!INCLUDE[vmm12short](Token/vmm12short_md.md)] performs a placement check to determine the best location on which to deploy the service and then opens the **Deploy Service** window.

7.  Follow the steps described above for reviewing the deployment configuration settings, resolving any errors and warnings, and then deploying the service.

## See Also
[Deploying services in VMM](Deploying-services-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


