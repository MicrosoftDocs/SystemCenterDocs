---
title: How to add hardware load balancers in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 679cc787-b5e9-4fb1-ae6f-91ba20f15124
---
# How to add hardware load balancers in VMM
You can use the following procedure to discover and add hardware load balancers to Virtual Machine Manager (VMM). By adding load balancers to VMM management and by creating associated virtual IP templates (VIP templates), users who create services can automatically provision load balancers when they create and deploy a service.

> [!IMPORTANT]
> If you want to use Microsoft Network Load Balancing (NLB), you do not have to complete this procedure. When you install VMM, NLB is automatically included as a load balancer. To use NLB, you must create NLB virtual IP templates. For more information, see [How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md).

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a Delegated Administrator where the administrative scope includes the host groups to which you want to make the load balancer available.

## Prerequisites
Before you begin this procedure, make sure that the following prerequisites are met:

-   You must have a supported hardware load balancer. VMM supports the following hardware load balancers:

    -   Brocade ServerIron ADX from Brocade Communications Systems, Inc.

    -   Citrix NetScaler from Citrix Systems, Inc.

-   You must obtain the load balancer provider from the load balancer vendor, and install the provider on the VMM management server. You can use the following links to obtain the load balancer provider from your vendor’s website:

    > [!NOTE]
    > In the following list, all information and content at the listed Web addresses is provided by the owner or the users of each website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

    -   [Download the Brocade ServerIron ADX load balancer provider](http://www.brocade.com/partnerships/technology-alliance-partners/partner-details/microsoft/microsoft-systems-center/index.page)

        > [!NOTE]
        > You must create or have an existing login to the Brocade website to download the provider.

    -   [Download the Citrix NetScaler load balancer provider](https://www.citrix.com/community.html)

    > [!IMPORTANT]
    > After you install the load balancer provider, you must restart the System Center Virtual Machine Manager service. To restart the service, from an elevated command prompt, type the command **net stop scvmmservice**, press ENTER, type **net start scvmmservice**, and then press ENTER.
    > 
    > Also, if you uninstall a VMM management server and then reinstall it, you must also uninstall and then reinstall the load balancer provider.

-   Although it is not a required prerequisite, you can create a Run As account before you begin this procedure. (You can also create the account during the procedure.) The associated credentials must have permissions to configure the load balancers that you want to add.

    For example, create a Run As account that is named **Load Balancers**.

    > [!NOTE]
    > You can create a Run As account in the **Settings** workspace. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

#### To add a hardware load balancer

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **Load Balancers**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Load Balancer**.

    The Add Load Balancer Wizard opens.

5.  On the **Credentials** page, next to the **Run As account** box, click **Browse**, and then click a Run As account that has permissions on the load balancer. When you are finished, click **OK**, and then click **Next**.

    For example, if you created the Run As account that is described in the Prerequisites section, select the **Load Balancers** Run As account.

    > [!NOTE]
    > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

6.  On the **Host Group** page, select the check box next to each host group where the load balancer will be available. By default, any child host groups are also selected.

    For example, under **Seattle**, select the check box next to the **Seattle** host group, and then click **Next**.

7.  On the **Manufacturer and Model** page, specify the load balancer manufacturer and model, and then click **Next**.

8.  On the **Address** page, do the following, and then click **Next**:

    1.  Specify the IP address, fully qualified domain name (FQDN), or the NetBIOS names of the load balancers that are of the same manufacturer and model that you specified in the previous step. Separate each load balancer by using a comma or by adding the load balancer on a new line.

    2.  In the **Port number** box, enter the port number that you use to connect to for management of the load balancers.

    For example, enter the FQDN **LoadBalancer01.contoso.com**, and the port number that is used to communicate with the load balancer, such as port 443.

9. On the **Logical Network Affinity** page, specify the load balancer affinity to logical networks, and then click **Next**.

    Setting the load balancer affinity enables you to provide some control over which load balancer will be used for a service. This is based on logical network information. VMM uses this information to determine the valid static IP address pools that are accessible from both the load balancer and the host group that the service tier will be deployed to. Note the following:

    -   When you configure front-end affinity, select the logical networks from which the load balancer can obtain its virtual IP (VIP) address. The VIP address is the IP address that is assigned to a load balancer during the deployment of a load-balanced service tier. Clients can connect to the VIP address through a registered DNS name to access the service.

        During the deployment of a load-balanced service tier, VMM looks for static IP address pools with available VIP addresses on the logical network that you select for the “Client connection” object when you configure a load balancer in a service template.

        For the load balancer to be selected during placement, when you configure the load balancer “Client connection” object, the logical network that you select must be in the list of logical networks that are selected for front-end affinity.

        > [!IMPORTANT]
        > For front-end affinity, make sure that you select one or more logical networks where the associated network site with a reserved VIP address range is available to a host group or parent host group that is also available to the hardware load balancer.

    -   When you configure back-end affinity, select the logical networks to which you want to make the load balancer available for connections from the virtual machines that make up a service tier.

        For the load balancer to be selected during placement, when you configure the load balancer “Server connection” object in a service template, the logical network that the NIC object is connected to must be in the list of logical networks that are selected for back-end affinity.

10. On the **Provider** page, do the following, and then click **Next**:

    1.  In the **Provider** list, click an available provider to use for load balancer configuration.

    2.  In the **Load balancer for configuration test** list, click an available load balancer, click **Test**, and view the test results.

11. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

12. Verify that the load balancer appears in the **Load Balancers** pane. The **Provider Status** column indicates whether the provider is active.

## See Also
[Configuring load balancing in VMM](Configuring-load-balancing-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[How to create VIP templates for hardware load balancers in VMM](How-to-create-VIP-templates-for-hardware-load-balancers-in-VMM.md)


