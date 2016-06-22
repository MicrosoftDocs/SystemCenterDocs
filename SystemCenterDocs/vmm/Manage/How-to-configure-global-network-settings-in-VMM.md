---
title: How to configure global network settings in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7454f9e3-3730-47c1-bec8-f880302e4c04
---
# How to configure global network settings in VMM
You can use the following procedure to configure global networking settings in Virtual Machine Manager \(VMM\). These are optional settings for the situation where you add a host to VMM management and you don't have any logical networks associated with physical network adapters on the host. In that situation, VMM can create a logical network for you automatically, depending on how these global settings are configured.

> [!NOTE]
> This procedure is optional. Change these settings only if you want to modify the default behavior.

**Account requirements** To complete this procedure, you must be a member of the Administrator user role.

### How to configure global networking settings

1.  Open the **Settings** workspace.

2.  In the **Settings** pane, click **General**.

3.  In the results pane, double\-click **Network Settings**.

4.  Configure any of the following settings:

    |Area|Settings|
    |--------|------------|
    |**Logical network matching**|You can configure how VMM determines the logical network name to use when the automatic creation of logical networks is enabled. The following options are available. **Note:** This setting is only applied when you add a host to VMM management and there is no logical network associated with a physical network adapter on the host.  Changes to this setting do not affect hosts that are already under management. Also, for VMware ESX hosts, the options of **First DNS Suffix Label** and **DNS Suffix** are not supported. Therefore, by default, ESX hosts use the **Virtual Network Switch Name** option.<br /><br />-   **First DNS Suffix Label** \(the default\)<br />    The first suffix label of the connection\-specific DNS suffix. For example, if the DNS suffix is corp.contoso.com, VMM creates a logical network that is named “corp”.<br />-   **DNS Suffix**<br />    The full connection\-specific DNS suffix. For example, if the DNS suffix is corp.contoso.com, VMM creates a logical network that is named “corp.contoso.com”.<br />-   **Network Connection Name**<br />    The network connection name. For example, if the network connection is named Local Area Connection 2, VMM creates a logical network that is named “Local Area Connection 2”.<br />-   **Virtual Network Switch Name**<br />    The name of the virtual network switch to which the physical network adapter of the host is bound.<br />-   **Disabled**<br /><br />You can also specify the option to use if the first logical network matching selection fails. You can select one of the following options:<br /><br />-   **Virtual Network Switch Name** \(default\)<br />-   **Network Connection Name**<br />-   **Disabled**|
    |**Automatic creation of logical networks**|By default, the **Create logical networks automatically** setting is enabled. If there is no logical network associated with a physical network adapter on the host, VMM automatically creates and associates a logical network based on the logical network matching selection. By default, this is the first DNS suffix label of the connection\-specific DNS suffix. On the logical network, VMM also creates a VM network configured with “no isolation.” **Note:** This setting is only applied when you add a host to VMM management and there is no logical network associated with a physical network adapter on the host. Changes to this setting do not affect hosts that are already under management.|

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


