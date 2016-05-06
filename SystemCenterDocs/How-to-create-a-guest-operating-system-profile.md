---
title: How to create a guest operating system profile
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9649115e-b018-4a4e-8eb5-e411733d8fae
---
# How to create a guest operating system profile
You can use the following procedure to create a guest operating system profile in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. A guest operating system profile specifies the operating system settings that you want the virtual machine to use when the virtual machine is created and deployed.

### To create a guest operating system profile

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Guest OS Profile**.

    The **New Guest OS Profile** dialog box opens.

3.  On the **General** tab, in the **Name** box, enter a name for the guest operating system profile. For example, enter **Domain\-joined Windows Server 2008 R2 Enterprise**.

4.  Click the **Guest OS Profile** tab, and then configure the desired settings. For example, you can configure the following settings:

    -   **Computer name**

        For the computer name, you can provide a pattern to generate computer names. For example, if you type **server\#\#\#\#**, the computer names that are created are server0001, server0002, and so on. Using a pattern ensures that when you add additional virtual machines to a service, unique computer names are created, and these computer names are related and identifiable. If you use this method to specify the computer name, you cannot use it in combination with a name prompt parameter \(@<name>@\). You can use one method or the other, but not both.

    -   **Local administrator account password**

        > [!NOTE]
        > If you want to use the guest operating system profile in a virtual machine template that is used in a service template, under **Admin Password**, do not select the **No local administrator credential required** option. You can either specify the password of the local administrator account, or select a Run As account. This setting does not apply to Linux\-based profiles.

    -   **Product key**

        If applicable, enter the product key to use for the virtual machine.

    -   **Operating system to install**

        > [!NOTE]
        > This setting lets you choose a Windows\-based or a Linux\-based operating system.

    -   **Domain to join**

        If you will use the profile in a virtual machine template within a service template, under **Networking**, you can specify optional Active Directory domain settings by using the FQDN or by using at signs \(@\) before and after, for example, by entering @Domain@. By using the at signs \(@\) in this way, the necessary information can be entered when the virtual machine is deployed as part of a service. A trust relationship is not necessary between the domain where the service is deployed and the domain of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server.

    -   **Windows Server roles or features to install**

        The settings for roles or features apply only if you deploy the virtual machine as part of a service and only for Windows\-based profiles. Also, to support these settings, the virtual machine cannot use a guest operating system earlier than [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)].

    -   **RunOnce commands**

        This setting applies only to Linux\-based profiles. These commands run in the specified order during deployment after the operating system has been configured. If shell conventions such as pipes are used, we recommend wrapping each command with an explicit invocation of the shell, for example, `/bin/sh –c “<your command>”`. In this example, double quotes in the command must be escaped.

    -   **Public SSH key**

        Under **Root Credentials**, **Public SSH key** is a Linux\-specific option. This option sets the content of a specified public Secure Shell \(SSH\) key as an authorized key for authentication of the root user. Enter the name of a public key file that is stored in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library, and that has the extension .sshkey.

    After you have made your selections, click **OK**.

5.  To verify that the profile was created, in the **Library** pane, expand **Profiles**, and then click **Guest OS Profiles**.

    The guest operating system profile appears in the **Profiles** pane.

## See Also
[Creating profiles and templates in VMM](../Topic/Creating-profiles-and-templates-in-VMM.md)
[Managing the VMM library and its resources](../Topic/Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

