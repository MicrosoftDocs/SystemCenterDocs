---
title: How to configure deployment settings for a service
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1dab5b7b-eeb0-43f7-979b-48d0f904bb24
---
# How to configure deployment settings for a service
When you are configuring a service for deployment to a private cloud or to a host group in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], you can configure settings for the following:

-   The service

-   The virtual machines being deployed in each tier

-   The applications that are being installed

> [!NOTE]
> The procedures below assume that you have started the deployment process for a service and that you are working in the **Deploy Service** window. For information about starting the deployment process, see [How to deploy a service in VMM](../Topic/How-to-deploy-a-service-in-VMM.md).

### To configure deployment settings for the service

1.  On the deployment map, select the service object. The service object contains the name of the service template being used and the release value.

2.  The details pane displays the settings that you can configure for the service. The following are some key settings that you can configure:

    |Setting|Description|
    |-----------|---------------|
    |**Name**|The name for the deployed service. This is the name that will appear in the VMs and Services workspace after the service is deployed.|
    |**Folder**|The host group to which you want to deploy the service. This setting is only displayed if you are deploying the service to a host group.|

    To save your changes to the deployment settings, click the down arrow in the top left corner of the ribbon, and then click **Save**.

### To configure deployment settings for a virtual machine in a tier

1.  On the deployment map, select the virtual machine object in a tier.

2.  The details pane displays the settings that you can configure for the virtual machine. The following are some key settings that you can configure:

    |Setting|Description|
    |-----------|---------------|
    |**VM name**|The name for the virtual machine. This is the name that will appear in the VMs and Services workspace after the service is deployed.<br /><br />We recommend that you set the value of **VM name** to match the value of **Computer name** to ensure consistent displays when monitoring the health and performance of the virtual machine with Operations Manager.|
    |**Computer name**|The computer name to use for the guest operating system of the virtual machine. Ensure that this computer name is not already being used in your environment.|
    |**Folder**|The host group to which you want to deploy the virtual machine. This setting is only displayed if you are deploying the service to a host group.|
    |**Host**|The host to which you want to deploy the virtual machine. This setting is only displayed if you are deploying the service to a host group.|

    > [!TIP]
    > The pin icon next to a setting allows you to specify whether the value you enter can be changed when the virtual machine is created and deployed. When the pin is in a horizontal position, the setting will not be changed.

    To save your changes to the deployment settings, click the down arrow in the top left corner of the ribbon, and then click **Save**.

### To configure deployment settings for an application being installed

-   In the left pane, the **Settings** tab displays the service settings that will be used during application deployment. The contents of the **Settings** tab varies depending on the application packages and scripts that are configured for the service.

-   For more information about configuring application installations, see [How to create an application profile in a service deployment](../Topic/How-to-create-an-application-profile-in-a-service-deployment.md).

## See Also
[Deploying services in VMM](../Topic/Deploying-services-in-VMM.md)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

