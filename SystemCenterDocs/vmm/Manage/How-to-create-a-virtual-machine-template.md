---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to create a virtual machine template
ms.technology:  virtual-machine-manager
ms.assetid:  4b4f0d28-a723-4197-a825-ec2766787e15
---

# How to create a virtual machine template

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedure to create a virtual machine template in Virtual Machine Manager (VMM). Virtual machine templates help you create new virtual machines and configure tiers in a service template. 

You can create a virtual machine template based on an existing virtual machine template or based on an existing virtual hard disk that is stored in a library. Alternatively, you can create a virtual machine template based on an existing virtual machine that is deployed on a host. This option requires that the existing machine has been stopped.

If you base your new virtual machine template on an existing virtual machine template or on a virtual hard disk that is stored in the library, you can configure hardware settings, guest operating system settings, application installations, and the installation of instances of Microsoft SQL Server. You can configure each of these settings manually, or you can import the settings from an existing profile. 
If you create a virtual machine template that is based on the Linux operating system, some of the Linux-specific settings, such as operating system specialization, work only if you deploy the Linux-based virtual machine on a Hyper-V host. Also, the option to create a virtual machine template that is based on an existing virtual machine that is deployed on a host is not applicable for Linux-based virtual machine templates. 

Before you create a virtual machine template, note the following:

-   When you create a virtual machine template, you can customize IP address settings. Static IP address settings are available only when you deploy a virtual machine from a virtual machine template.

-   Application deployment, SQL Server deployment, and configurable service settings apply only when you deploy the virtual machine as part of a service.

-   If you grant rights for a particular template to a user that does not have rights to the Run As account that is specified in the template, then the user can potentially extract the credentials for the Run As account from the template during deployment.

-   Make sure the template has the correct operating system specified.

-   Before creating a template based on a virtual machine, you must create a new local administrator account on that virtual machine. Using the default built-in administrator account will cause Sysprep to fail.

-   Before creating a template based on a virtual machine, make sure that the virtual machine is not joined to a domain. Otherwise, Sysprep will fail. For more information, see [SCVMM create virtual machine error 66](http://social.technet.microsoft.com/Forums/f50894e2-6733-4d04-8fb9-bba4a16717c7/scvmm-create-virtual-machine-error-66?forum=virtualmachinemanager).

> [!NOTE]
> For Sysprep best practices, see [Sysprep, SkipRearm, and Image Build Best Practices](http://blogs.technet.com/b/askcore/archive/2011/05/11/sysprep-skiprearm-and-image-build-best-practices.aspx).

### To create a virtual machine template that is based on an existing virtual hard disk or virtual machine template

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create VM Template**.

    The Create VM Template Wizard opens.

3.  On the **Select Source** page, click **Use an existing VM template or a virtual hard disk stored in the library**, and then click **Browse**.

4.  In the **Select VM Template Source** dialog box, click the appropriate virtual hard disk or virtual machine template, click **OK**, and then click **Next**.

5.  On the **Identity** page, enter the virtual machine name and an optional description.

    If the VM template source that you selected on the previous page was a virtual hard disk in VHDX format, the **Generation** box also appears. In the **Generation** box, select **Generation 1** or **Generation 2**. (For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).)

    Then click **Next**.

6.  On the **Configure Hardware** page, configure the hardware settings. If you have an existing hardware profile that you want to use, in the **Hardware profile** list, click the desired hardware profile. After you have configured the hardware settings, click **Next**.

    When you configure hardware settings, consider the following:

    -   **Capability profile**: If you intend to deploy the virtual machine to a private cloud, under **Capability**, you must select a cloud capability profile that is supported by the private cloud.

    -   **Generation**: If you selected **Generation 1** or **Generation 2** in the previous step, the hardware profiles and hardware options that are available are those of the generation that you selected. For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).

    -   **Network�static IP**: If you configure a network adapter to use static IP addresses, you must also set the media access control (MAC) address to static.

    -   **Storage classifications**: If you want the virtual hard disks that are created from this template to be placed on storage resources in one of your storage classifications (for example, you might have created storage classifications called **Gold**, **Silver**, and **Bronze**), at the bottom of the pane for a virtual hard disk, select the classification. 
    -   **Priority (on a host cluster)**: If the virtual machine will be on a host cluster, you can use VMM to configure virtual machine priority for the virtual machine. 
    -   **Guest clustering**: You can use VMM to create virtual machines that will work together as a guest cluster. 
7.  On the **Configure Operating System** page, open the  **Guest OS profile** list and either select a guest operating system profile, or select the type of operating system for which you want to create customized settings�Windows, Linux, or none. Your selection from the list determines the settings that are displayed on the wizard page. Your selection also determines whether additional wizard pages are displayed.

    Configure the guest operating system settings, and then click **Next**.

    When you configure operating system settings, consider the following:

    -   Under **Identity Information**:

        -   For the **Computer name**, you can provide a pattern to generate computer names. For example, if you enter **server####**, the computer names that are created are server0001, server0002, and so on. The use of a pattern ensures that when you add additional virtual machines to a service, the computer names that are generated are related and identifiable. If you use this method to specify the computer name, you cannot use it in combination with a name prompt parameter (@<name>@). You can use one method or the other, but not both.

        -   **DNS domain name** is a Linux-specific option. Enter the domain name portion of the fully qualified domain name (FQDN).

    -   The **Roles and Features** settings apply only for Windows, and only if you use the virtual machine template in a service template. Also, to support these settings, the virtual machine cannot use a guest operating system earlier than Windows Server 2008 R2.

    -   The **RunOnce commands** apply only to Linux-based virtual machine templates. These commands run in the specified order during deployment after the operating system has been configured. If shell conventions, such as pipes, are used, we recommend wrapping each command with an explicit invocation of the shell, for example, `/bin/sh �c �<your command>�`. In this example, double quotes in the command must be escaped.

    -   Under **Root Credentials**, **Public SSH key** is a Linux-specific option. This option sets the content of a specified public Secure Shell (SSH) key as an authorized key for authentication of the root user. Enter the name of a public key file that is stored in the VMM library and has the extension .sshkey.

    -   If you will use the virtual machine template in a service template, under **Networking**, you can specify optional Active Directory domain settings by using the FQDN or by using at signs (@) before and after, for example, by entering @Domain@. By using the at signs (@) in this way, the necessary information can be entered when the virtual machine is deployed as part of a service. A trust relationship is not necessary between the domain where the service is deployed and the domain of the VMM management server.

        You can use the virtual machine template in a service template regardless of which option you select under **Admin Password**.

        > [!NOTE]
        > Active Directory domain settings do not apply to Linux-based templates.

8.  If the **Configure Applications** page appears, as needed, configure the applications to install. If you have an existing application profile with settings that you want to use, select that application profile from the **Application profile** list. After you have configured the application settings, click **Next**.

    > [!NOTE]
    > Application deployment settings do not apply if you use the template for stand-alone virtual machines that are not part of a service.

9. If the **Configure SQL Server** page appears, as needed, configure the installation of an instance of SQL Server. If you have an existing SQL Server profile that you want to use, in the **SQL Server profile** list, click the SQL Server profile. After you have configured the SQL Server settings, click **Next**.

    > [!NOTE]
    > SQL Server settings do not apply if you use the template for stand-alone virtual machines that are not part of a service.

10. On the **Summary** page, confirm the settings, and then click **Create**.

### To create a virtual machine template from an existing virtual machine that is deployed on a host

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create VM Template**.

    The Create VM Template Wizard opens.

3.  On the **Select Source** page, click **From an existing virtual machine that is deployed on a host**, and then click **Browse**.

4.  In the **Select VM Template Source** dialog box, click the desired virtual machine, click **OK**, and then click **Next**.

5.  On the **VM Template Identity** page, provide a name for the virtual machine template, and then click **Next**.

    > [!WARNING]
    > A warning message advises you that creating a template will destroy the source virtual machine, and that any user data on the source virtual machine may be lost. To continue, click **Yes**.

6.  On the **Configure Hardware** page, click **Next**.

7.  On the **Configure Operating System** page, configure the guest operating system settings. If you have an existing guest operating system profile that you want to use, in the **Guest OS profile** list, click the desired guest operating system profile. After you have configured the guest operating system settings, click **Next**.

8.  On the **Select Library Server** page, click the library server for the virtual machine, and then click **Next**.

9. On the **Select Path** page, click **Browse**, click a library share and optional folder path, click **OK**, and then click **Next**.

10. On the **Summary** page, confirm the settings, and then click **Create**.



