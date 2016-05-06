---
title: How to create a guest cluster by using a service template in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbd26c78-7685-4a8f-b7f1-9b344d91f7d4
---
# How to create a guest cluster by using a service template in VMM
This topic explains how to create a guest cluster by using a service template in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. A guest cluster can be configured to run a variety of applications, but one application that guest clusters often run is SQL Server.

Service templates can be built up from other profiles and templates. Regardless of how a service template is created for a guest cluster, it includes instructions that tell [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to deploy multiple virtual machines together as a “tier” \(in this case, the tier is the guest cluster\). The service template also includes instructions that tell [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] how to run appropriate scripts to create a cluster from the virtual machines as they are deployed.

**Prerequisites**

To prepare to create a guest cluster, review the following prerequisites:

-   **Host cluster**: Virtual machines in a guest cluster can be deployed only to host clusters running[!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)]. If you deploy a service from a service template that includes one or more guest clusters, and there are no host clusters running[!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](../Token/winthreshold_server_2_md.md)] to which the guest cluster can be deployed, deployment of the guest cluster will fail. For information about host clusters, see [Managing Hyper-V hosts and host clusters with VMM](../Topic/Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md).

-   **Scripts**: Scripts that you will need for creating the guest cluster include:

    -   A script to run on the first virtual machine so that it can form the cluster.

    -   A script to run on the later virtual machines so that they can join the cluster.

    -   Potentially, scripts that install your application correctly for a cluster. For example, to run SQL Server 2012, you might need a script that installs SQL Server 2012 correctly on the first node of the guest cluster, and another script to install it on later nodes. \(You cannot use   a     sysprepped image of SQL Server for installation, because this does not work in the context of a cluster.\)

    > [!NOTE]
    > In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], script settings are specified as part of the “application” configuration—either in an application profile or on the application tab of a VM template or service\-tier template.

-   **Information about hardware settings**: You will need to know basic hardware settings, such as the amount of memory, that you want on the nodes \(the virtual machines\) in the guest cluster.

-   **One or more virtual hard disks to be used by all nodes in the guest cluster**: Most clusters have one or more shared disks that are used by all nodes in the cluster, although this is not required. To configure shared disks for your guest cluster, use the following guidelines:

    -   Review the virtual hard disks \(VHDX files\) in your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library, and make sure that the VHDX files that will be shared by the cluster nodes are in the library.

    -   Use new VHDX files. Do not reuse VHDX files from a previous cluster.

    -   Identify a single location \(path\) in SCSI\-based shared storage where all the VHDX files for the guest cluster will be placed at deployment time.

        You can use storage classifications to control the placement of the shared VHDX files, but within your storage classification, you must have at least one location with the capacity to contain all the shared VHDX files for your guest cluster. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will not deploy the shared VHDX files to multiple locations.

        You can vary the location of shared VHDX files at deployment time, even if you use the same service template to deploy a series of guest clusters. To do this, you must deploy your guest clusters to a host group \(not a cloud\). Then, at deployment time, you can specify a single location \(path\) for the shared VHDX file or files for that particular guest cluster. This will override the location that you specified in the virtual machine template.

    For background information about virtual hard disks that are used for a guest cluster, see[Virtual Hard Disk Sharing Overview](http://technet.microsoft.com/library/dn281956.aspx).

    > [!IMPORTANT]
    > For best results with managing the guest cluster in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], we recommend that you create the guest cluster as a service in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], rather than creating the guest cluster by using Hyper\-V.

-   **Virtual hard disk for the operating system for each node of the guest cluster**: You will need a virtual hard disk file that contains the operating system \(prepared with Sysprep\) that you want the virtual machines in the guest cluster to use. \(This is different from the virtual hard disk file that will be deployed to shared storage.\) When each node is created, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will use a copy of this virtual hard disk file for the system disk of the node.

With these prerequisites in place, you can create a service template and connect all the configuration elements together.

This topic contains the following procedures:

1.  [Specify settings for scripts that run when a guest cluster is created](../Topic/How-to-create-a-guest-cluster-by-using-a-service-template-in-VMM.md#BKMK_app)

2.  [Create a virtual machine template and include it in a service tier for a guest cluster](../Topic/How-to-create-a-guest-cluster-by-using-a-service-template-in-VMM.md#BKMK_service)

## <a name="BKMK_app"></a>Specify settings for scripts that run when a guest cluster is created
In the application settings in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can include scripts that will be run at specific times in relation to the creation of a guest cluster, such as **Creation: First VM** or **Creation: VMs After First**. The following procedure provides steps for specifying such settings.

#### To specify settings for scripts that run when a guest cluster is created

1.  Confirm that your application components, especially your scripts, have been copied to the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library share. When you copy a script, place it in a folder in the library share and give the folder an extension of **.cr**, which indicates a “custom resource” in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

2.  Open the **Library** workspace.

3.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Application Profile**.

    The New Application Profile dialog box opens.

4.  On the **General** tab, in the **Name** box, type a name and an optional description. For example, type the name **GuestSQL**.

5.  On the **General** tab, in the **Compatibility** list, leave the default selection, **General**.

    You must use the **General** option for a profile in which you specify scripts that first form a cluster and then join nodes to the cluster.

6.  Click the **Application Configuration** tab, click **OS Compatibility**, and then select one or more editions of a server operating system. For a guest cluster, do not select an operating system earlier than Windows Server 2012.

7.  Still on the **Application Configuration** tab, add the scripts that you need for creating the first node of the cluster and for adding other nodes to the cluster. To add a script, click **Add** and then select **Script**. The number of scripts is not limited, and you can specify the order in which the scripts will run. Provide the following types of information for each script:

    -   For a script that will run on the first node of the cluster when it is created \(and not on other nodes\), for **Script command type**, select **Creation: First VM**.

    -   For a script that will run on later nodes of the cluster when they are created \(and not on the first node\), for **Script command type**, select **Creation: VMs After First**.

    -   For each script, specify the executable name and the parameters through which the script will run.

        > [!NOTE]
        > A script can contain settings to be entered when you are configuring the service for deployment. To format this type of setting, type the parameter in the **Parameters** field in the following format: @<SettingLabel>@ \(for example, type @ClusterName@\).

        For example, consider a script that runs with the executable name **Cmd.exe** with the **\/q** and **\/c** parameters. Suppose that the script is called **FormCluster.cmd**, and it requires that the cluster name is supplied when the cluster is deployed. For this script, you could specify the following information:

        Executable program: **Cmd.exe**

        Parameters: **\/q \/c FormCluster.cmd @ClusterName@**

    -   For each script, provide the script location. Under **Script resource package**, click **Browse** and then select the folder with the **.cr** extension into which you copied the script. Click **OK**.

    -   For each script, provide a **Run As account**.

    -   Configure other settings as needed, such as how long the script should run before timing out, the failure and restart policies that specify what to do if there is an error, and other settings. To configure these settings, under **Scripts**, select the script and review or change the deployment order, timeout, or other settings. As needed, click **Advanced** and view or configure advanced settings such as failure and restart policies.

    You can also add scripts that will delete the guest cluster in an orderly way. For such a script, select a **Script command type** of **Deletion: VMs Before Last** or **Deletion: Last VM**.

8.  To add more scripts to the application profile, on the **Application Configuration** tab, click **Add**, select **Script**, and specify appropriate settings.

    You can add scripts that use a **Script command type** that was not mentioned in the previous step. For example, with a **Script command type** of **Pre\-Install**, a script will run on the first virtual machine and also on later virtual machines that are created as part of the service tier.

9. After you have made all your selections, click **OK**.

10. To verify that the profile was created, in the **Library** pane, expand **Profiles**, and then click **Application Profiles**.

    The application profile appears in the **Profiles** pane.

## <a name="BKMK_service"></a>Create a virtual machine template and include it in a service tier for a guest cluster
When you create a virtual machine template and you include it in a service tier for a guest cluster, in most cases, you will include settings for a shared VHDX file in the virtual machine template. This VHDX file must be deployed to shared storage that has SCSI channels available for each node of the cluster. This configuration provides each node of the guest cluster with access to the same VHDX file \(disk\).

Also, the service tier in which the virtual machine template is placed must have settings for scaling the tier out to multiple instances of the virtual machine. Each instance in the tier is one node in the guest cluster.

#### To create a virtual machine template and include it in a service tier for a guest cluster

1.  Ensure that on the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library share, you have a virtual hard disk that contains the operating system \(prepared with Sysprep\) that you want the virtual machines in the guest cluster to use. This virtual hard disk cannot be blank. \(This is different from the virtual hard disk file that will be deployed to shared storage.\)

2.  Open the **Library** workspace.

3.  On the **Home** tab, in the **Create** group, click **Create VM Template**.

    The Create VM Template Wizard opens.

4.  On the **Select Source** page, click **Use an existing VM template or a virtual hard disk stored in the library**, and then click **Browse**.

5.  In the **Select VM Template Source** dialog box, click the virtual hard disk described in step 1 of this procedure, click **OK**, and then click **Next**.

6.  On the **VM Template Identity** page, provide a name for the virtual machine template, and for the **Generation**, select **Generation 1**. Then click **Next**.

    Because the VM template must be added into a service template, you cannot choose **Generation 2**.

7.  On the **Configure Hardware** page, configure the hardware settings. If you want to use a hardware profile, make sure it includes the settings in the list that follows, and then in the **Hardware profile** list, click the intended hardware profile.

    When you configure hardware settings, consider the following:

    -   If you intend to deploy the virtual machine to a private cloud, under **Capability**, you must select a cloud capability profile that is supported by the private cloud.

    -   To configure the guest cluster to use a shared virtual hard disk \(in the VHDX format\), under **Bus Configuration**, click **SCSI adapter 0**, and then near the top of the page, beside **New**, click **Disk**. The new disk appears as a listing under the SCSI adapter. Select that disk and then select **Share the disk across the service tier**. Ensure that the check box for **Contains the operating system for the virtual machine** is cleared. Click **Browse**, select the VHDX file that you want VMM to deploy to shared storage, and then click **OK**. Repeat this process for each additional node in the cluster—add the same disk each time, but ensure that the SCSI channel is unique for each instance of that disk.

        > [!IMPORTANT]
        > For each node that you plan to have in the guest cluster, configure one instance of the same disk, and give that instance a unique SCSI channel.

        You can repeat the process of adding disks that will be used by the cluster. However, be sure to review “Prerequisites,” earlier in this topic, for details about choosing the shared storage location. If you do add more shared disks, ensure that each additional disk is configured with the same number of SCSI channels as the number of nodes that you plan to have in the guest cluster.

    -   If you configure a network adapter to use static IP addresses, you must also set the media access control \(MAC\) address to static.

    -   Under **Network Adapters**, select the network adapter, and at the bottom of the details pane, select **Enable guest specified IP addresses**. This enables the nodes \(virtual machines\) in the guest cluster to specify IP addresses for the cluster itself, and for applications that you configure to run in the cluster.

    -   Under **Advanced**, click **Availability**, and then select **Make this virtual machine highly available**. When this is selected, the virtual machine is created as a clustered instance on the host cluster, so that if one host fails, the virtual machine will fail over to another host in the cluster.

    -   As a best practice, under **Advanced**, click **Availability**, and then click the **Manage availability sets** button. To create a new availability set, click the **Create** button, provide a name for the set, and then click **OK**. In the **Manage Availability Sets** dialog box, click **OK**.

        The availability set name that you specify will be used by all the nodes \(virtual machines\) in the guest cluster, which means that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will attempt to keep the virtual machines on separate hosts, so that if one host fails, a virtual machine on another host can provide service as needed. \(If you have worked with failover clusters in other contexts, you might know this setting as **AntiAffinityClassNames**.\)

    After you have configured the hardware settings, click **Next**.

8.  On the **Configure Operating System** page, open the **Guest OS profile** list and either select a guest operating system profile, or select **\[Create new Windows operating system customization settings\]**. Your selection from the list determines the settings that are displayed on the wizard page. Your selection also determines whether additional wizard pages are displayed.

    When you configure operating system settings, consider the following:

    -   Under **Identity Information**, for the **Computer name**, you can provide a pattern to generate computer names. For example, if you enter **server\#\#\#\#**, the computer names that are created are server0001, server0002, and so on. The use of a pattern ensures that when you add additional virtual machines to a service, the computer names that are generated are related and identifiable. If you use this method to specify the computer name, you cannot use it in combination with a name prompt parameter \(@<name>@\). You can use one method or the other, but not both.

    -   Under **Networking**, you can specify specify settings for Active Directory Domain Services by using the FQDN or by using at signs \(@\) before and after the domain name, for example, @Domain@. By using the at signs \(@\) in this way, the necessary information can be entered when the virtual machine is deployed as part of a service. A trust relationship is not necessary between the domain where the service is deployed and the domain of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server.

    After you configure the guest operating system settings, click **Next**.

9. On the **Configure Applications** page, click **Next**. You will add these settings to your configuration later, as described in this procedure.

10. On the **Configure SQL Server** page, click **Next**.

11. On the **Summary** page, confirm the settings, and then click **Create**. Confirm that the virtual machine template was created.

12. In the **Library** workspace, on the **Home** tab, in the **Create** group, click **Create Service Template**.

    The **New Service Template** dialog box opens.

13. Specify a name, version, and pattern for the template. The patterns help you begin to create a service template, but you can change the number of tiers after you exit this dialog box. After you complete your selections, click **OK**.

    The pattern that you selected appears on the canvas. If you select a pattern with tiers, the tiers exist, but they do not have VM templates applied to them.

14. In the **VM Templates** pane \(next to the canvas\), click the virtual machine template that you just created and drag it onto a tier. If you do not yet have tiers on the canvas, drag the virtual machine template anywhere on the canvas.

    The label in the box \(for the tier\) changes to reflect the name of the virtual machine template. If the virtual machine template contains network settings, a connector might appear lower in the box. This connector shows a connection to a VM network.

    Dragging a virtual machine template onto the canvas is the basic process for building a service template. You can change the number of tiers as needed. You can add a tier by dragging an additional virtual machine template onto the canvas, or remove a tier by deleting a virtual machine template that is on the canvas.

15. On the canvas, right\-click the tier that you just dragged the virtual machine template onto, click **Properties**, and then click **Application Configuration**. Near the top of the page, next to **Application profile**, click the drop\-down list, and then click the application profile that you created in the procedure earlier in this topic. Then click **OK**.

    Because you have taken this step, when the service is deployed, the scripts that you specified in the application profile will run.

16. On the **Home** tab, in the **Service Template** group, click **Save and Validate** to save the service template.

    If there are any validation errors, a warning icon appears on the element of the service template that caused the validation error, and a message that describes the issue appears in the properties pane in the Service Template Designer window.

17. Right\-click the box that represents the tier for the guest cluster, and then click **Properties**. On the **General** tab, select **This machine tier can be scaled out**, and then specify values greater than 1 for **Default instance count** and **Maximum instance count**. The values that you specify control the number of nodes in the guest cluster. For example, **Default instance count** specifies the number of nodes that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will create when the cluster is created.

    > [!IMPORTANT]
    > Be sure that the **Maximum instance count** is less than or equal to the number of SCSI channels that you previously configured for the disk \(under **Bus Configuration**\). Be sure that the **Default instance count** is less than or equal to the **Maximum instance count**.

18. With the properties of the tier for the guest cluster still displayed \(as in the previous step\), for **Number of upgrade domains**, specify a value that is the same as the **Maximum instance count** that you specified in the previous step.

    For example, if you specified a **Default instance count** of **3** and a **Maximum instance count** of **3**, the guest cluster would have three nodes. When you updated the service, if you specified an incorrect value of **1** for the **Number of upgrade domains**, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] would perform the update in one stage, which means it would update all three virtual machines at the same time. This would cause the cluster to lose quorum and stop running during the update process. However, if you specified an appropriate value of **3** for the **Number of upgrade domains**, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] would perform the update in three stages, which means it would update one virtual machine at a time. This would leave two virtual machines in the guest cluster running at any given time, and the cluster would continue to run during the update process.

    For more information about upgrade domains, see [Updating services in VMM](../Topic/Updating-services-in-VMM.md).

19. On the **Home** tab, in the **Service Template** group, click **Save and Validate** to save the service template.

For information about deploying the service, see [Deploying services in VMM](../Topic/Deploying-services-in-VMM.md).

## See Also
[Creating profiles and templates in VMM](../Topic/Creating-profiles-and-templates-in-VMM.md)
[Preparing to create services in VMM](../Topic/Preparing-to-create-services-in-VMM.md)
[Deploying services in VMM](../Topic/Deploying-services-in-VMM.md)
[Virtual Hard Disk Sharing Overview](http://technet.microsoft.com/library/dn281956.aspx)
[Configuring availability options for virtual machines in VMM](../Topic/Configuring-availability-options-for-virtual-machines-in-VMM.md)
[How to configure priority in VMM for a virtual machine on a host cluster](../Topic/How-to-configure-priority-in-VMM-for-a-virtual-machine-on-a-host-cluster.md)
[Using Guest Clustering for High Availability](http://technet.microsoft.com/library/dn440540.aspx)
[Test Lab Guides: System Center 2012 SP1 - Virtual Machine Manager](http://www.microsoft.com/download/details.aspx?id=38837)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

