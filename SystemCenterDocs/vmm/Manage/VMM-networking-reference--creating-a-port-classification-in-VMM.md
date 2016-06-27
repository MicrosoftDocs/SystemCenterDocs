---
title: VMM networking reference: creating a port classification in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe59aa97-794a-4d64-b382-a1d7b5cd6437
---
# VMM networking reference: creating a port classification in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Port classifications provide global names for identifying different types of virtual network adapter port profiles. A port classification can be used across multiple logical switches while the settings for the port classification remain specific to each logical switch. For example, you might create one port classification named FAST to identify ports that are configured to have more bandwidth, and another port classification named SLOW to identify ports that are configured to have less bandwidth.

For more information about port profiles, port classifications, and logical switches, see [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md).

Use the following procedure to create a port classification.

> [!NOTE]
> You can also create a new port classification from within the Create Logical Switch Wizard.

### To create a port classification

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking**, and then click **Port Classifications**.

4.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Port Classification**.

    The Create Port Classification Wizard opens.

5.  On the **Name** page, enter a name and optional description for the port classification, and then click **OK**.

## See Also
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[How to create a logical switch in VMM](How-to-create-a-logical-switch-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



