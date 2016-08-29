---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to create a hardware profile
ms.technology:  virtual-machine-manager
ms.assetid:  7ea7a41f-a294-43a8-a768-f11180ebebd6
---

# How to create a hardware profile

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedure to create a hardware profile in Virtual Machine Manager (VMM). A hardware profile specifies the hardware settings that you want the virtual machine to use when the virtual machine is created and deployed.

### To create a hardware profile

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Hardware Profile**.

    The New Hardware Profile dialog box opens.

3.  On the **General** tab, in the **Name** box, enter a name for the hardware profile. For example, enter **8 GB 2 processor server**.

    In the **Generation** box, select **Generation 1** or **Generation 2**. (For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).)

4.  Click the **Hardware Profile** tab, and then configure the desired settings. For example, you can configure the following settings:

    -   The number of processors

    -   The amount of static or Dynamic memory

    -   The logical network

    -   Whether to make the virtual machine highly available

    -   Which capability profiles to use

    > [!NOTE]
    > -   If you want to deploy the virtual machine to a private cloud, you must select a capability profile that is supported by the private cloud. For more information about capability profiles, see [How to create a private cloud from host groups in VMM](How-to-create-a-private-cloud-from-host-groups-in-VMM.md).
    > -   The hardware options that are available are those of the generation that you selected in the previous step.

    After you have made your selections, click **OK**.

5.  To verify that the profile was created, in the **Library** pane, expand **Profiles**, and then click **Hardware Profiles**.

    The hardware profile appears in the **Profiles** pane.

## See Also
[Creating profiles and templates in VMM](Creating-profiles-and-templates-in-VMM.md)
[Managing the VMM library and its resources](Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



