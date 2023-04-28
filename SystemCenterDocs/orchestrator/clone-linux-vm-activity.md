---
title: Clone Linux VM activity
description: The article describes the Clone Linux VM activity,  to create a copy of an existing Linux virtual machine or template in a runbook.
ms.custom: UpdateFrequency3
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
author: jyothisuri
ms.author: jsuri
manager: mkluck
monikerRange: '<=sc-orch-2019'
ms.date: 04/27/2023
---

# Clone Linux VM activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Clone Linux VM activity is used in a runbook to create a copy of an existing Linux virtual machine or template. This can be used to create new virtual machines quickly and easily using the existing virtual machines or templates as models.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

With the exception of "Source VM/Template Path," all properties and published data refer to the destination VM produced by the clone operation.

> [!IMPORTANT]
> To support multiple network adapters, the IP Address, Subnet Mask, Gateway, and DNS Suffix optional properties can support a comma-separated list of values. Each list must contain the same number of values. The value DHCP causes that network adapter value to be assigned by a DHCP server. If no IP address is specified for a network adapter, it will be assigned by a DHCP server.
> For example, to assign network details to three network adapters, use the following format:
> - IP Address = 192.168.0.2, DHCP, 10.0.0.3
> - Subnet Mask = 255.255.255.0, DHCP, 255.0.0.0
> - Gateway = 192.168.0.1, DHCP, 10.0.0.1
> - DNS Suffix = a.com, b.com, c.com<br><br>

### Clone Linux VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Clone Task Timeout in seconds | The number of seconds to wait for the clone operation to complete. After the timeout has been reached, the activity will fail if the clone operation hasn't completed.   | Integer   | No   |
| Customize   | Indicates whether the virtual machine guest settings are customized after the virtual machine is cloned. If set to False, guest customizations (IP address, DNS name, and so on) won't be applied. | Boolean   | Yes   |
| Datastore Path   | The data store name for the cloned virtual machine.   | String   | Yes   |
| Folder Path   | The path to the folder where the cloned virtual machine will be saved.   | String   | Yes   |
| Host System Path   | The path to the host system of the cloned virtual machine.   | String   | Yes   |
| Memory Size (MB)   | The amount of memory, in megabytes, to assign to the cloned virtual machine.   | Integer   | No   |
| New Virtual Machine Name   | The name of the cloned virtual machine.   | String   | No   |
| Power on after creation   | Indicates whether the cloned virtual machine is turned on after it's created.   | Boolean   | Yes   |
| Resource Pool Path   | The path to the resource pool that the cloned virtual machine will use.   | String   | Yes   |
| Source VM/Template Path   | The name of the virtual machine or template that you want to clone.   | String   | Yes   |
| Virtual Processors   | The number of virtual processors to assign to the cloned virtual machine.   | Integer   | No   |

### Clone Linux VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| DNS Name   | The Hostname or Short DNS Name with no spaces or periods (.).   | String   | No   |
| DNS Server   | The name of the DNS server that will resolve name requests for the clone virtual machine.   | String   | No   |
| Domain Name   | The name of the domain that the cloned virtual machine will belong to.   | String   | No   |
| Gateway   | The gateway that the cloned virtual machine will use   | String.  | No   |
| IP Address   | The IP address that will be assigned to the cloned virtual machine.   | String   | No   |
| Subnet Mask   | The subnet mask that the cloned virtual machine will use.   | String   | No   |
| DNS Suffix   | The DNS Suffix that will be assigned to the network adapter of the cloned virtual machine. For example, example.com. | String   | No   |

### Clone Linux VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Clone Task Timeout in seconds   | The timeout setting for the clone operation.   | Integer   |
| Customize   | Indicates whether the virtual machine computer settings were customized after cloning.   | Boolean   |
| Datastore Path   | The path of the data store.   | String   |
| DNS Name   | The name of the virtual machine in the domain naming service.   | String   |
| DNS Server   | The name of the DNS server.   | String   |
| Domain Name   | The name of the domain that the cloned virtual machine uses.   | String   |
| Folder Path   | The path to the destination folder for the cloned virtual machine.   | String   |
| Gateway   | The gateway that the cloned virtual machine uses.   | String   |
| Host System Path   | The path of the destination vSphere host system.   | String   |
| IP Address   | The static IP address of the cloned virtual machine.   | String   |
| Memory Size(MB)   | The amount of memory, in megabytes, assigned to the cloned virtual machine.   | Integer   |
| Power on after creation   | Indicates whether the cloned virtual machine was turned on after creation.   | Boolean   |
| Resource Pool Path   | The path to the resource pool that the cloned virtual machine uses.   | String   |
| Source VM/Template Path   | The name of the virtual machine or template that you want to clone.   | String   |
| Subnet Mask   | The subnet mask that the cloned virtual machine will use.   | String   |
| New Virtual Machine Name   | The name of the cloned virtual machine.   | String   |
| Virtual Processors   | The number of virtual processors assigned to the cloned virtual machine.   | Integer   |
| DNS Suffix   | The DNS Suffix that will be assigned to the network adapter of the cloned virtual machine. For example, example.com. | String   |

## Configuring the Clone Linux VM Activity

The following procedure describes the steps required to configure a Clone Linux VM activity.

#### To configure the Clone Linux VM Activity

1.  From the **Activities** pane, drag a **Clone Linux VM** activity to the active runbook.

2.  Double-click the **Clone Linux VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
