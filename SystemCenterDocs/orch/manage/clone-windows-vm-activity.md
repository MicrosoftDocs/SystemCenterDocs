---
title: Clone Windows VM Activity
description: The Clone Windows VM activity is used in a runbook to create a copy of an existing Windows virtual machine or template.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab0c21ce-3a9d-4901-ad45-4e9e76757a48
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Clone Windows VM Activity

Applies To: System Center 2016 - Orchestrator

The Clone Windows VM activity is used in a runbook to create a copy of an existing Windows virtual machine or template. This creates virtual machines quickly and easily using existing virtual machines or templates as models.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

With the exception of "Source VM/Template Path," all properties and published data refer to the destination VM produced by the clone operation.

<br><br><strong>Note</strong><br>To support multiple network adapters, the IP Address, Subnet Mask, Gateway, and DNS Suffix optional properties support a comma-separated list of values. Each list must have the same number of values. For example, to assign network details to three network adapters, use the following format:<br> IP Address = 192.168.0.2, DHCP, 10.0.0.3<br> Subnet Mask = 255.255.255.0, DHCP, 255.0.0.0<br> Gateway = 192.168.0.1, DHCP, 10.0.0.1<br> DNS Suffix = a.com, b.com, c.com<br> The value DHCP causes that network adapter value to be assigned by a DHCP server. If no IP address is specified for a network adapter, it will be assigned by a DHCP server.<br><br>

<br><br><strong>Note</strong><br>If you clone an existing Windows virtual machine with guest customizations, such as IP Address, Admin Password, Computer Name, and so on, and you want to verify these customizations on the new cloned virtual machine, follow the steps below:<br> After the clone operation completes, ensure that the cloned virtual machine is turned on in the vSphere client.<br> After the cloned virtual machine boots to the lock screen, wait two minutes.<br> After the cloned virtual machine automatically reboots, the VMware customization message appears.<br> After the cloned VM reboots for a second time to the lock screen, wait two minutes.<br> Verify that all the customizations (which you specified in the Properties dialog box of this activity) in vSphere client. You can view these customizations on the Virtual Machine Properties dialog box, or the Summary tab window, or you can log into the guest operating system in the vSphere console.<br><br>

### Clone Windows VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
| Clone Task Timeout in seconds | The number of seconds for the clone activity to complete before timing out. The activity will fail if the clone operation has not completed within the configured time.   | Integer   | No   |
|:---|:---|:---|:---|
| Customize   | Indicates whether the virtual machine computer settings are customized after the virtual machine is cloned. If set to False, any guest customizations such as IP address or DNS name will not be applied. | Boolean   | Yes   |
| Datastore Path   | The data store name that the cloned virtual machine will use.   | String   | Yes   |
| Folder Path   | The path to the folder containing the cloned virtual machine.   | String   | Yes   |
| Host System Path   | The path to the host operating system of the cloned virtual machine.   | String   | Yes   |
| Memory Size (MB)   | The amount of memory, in megabytes, assigned to the cloned virtual machine.   | Integer   | No   |
| New Virtual Machine Name   | The name of the cloned virtual machine.   | String   | No   |
| Resource Pool Path   | The path to the resource pool of the cloned virtual machine.   | String   | Yes   |
| Source VM/Template Path   | The name of the virtual machine or template to clone.   | String   | Yes   |
| Virtual Processors   | The number of virtual processors assigned to the cloned virtual machine.   | Integer   | No   |

### Clone Windows VM Activity Optional Properties

| Element   | Description   | Valid Values | Look up |
| Admin Password   | The password of the Administrator account of the cloned virtual machine.   | String   | No   |
|:---|:---|:---|:---|
| Computer Name   | The name of the cloned virtual machine.   | String   | No   |
| DHCP (not available in System Center 2016) | Indicates whether to use DHCP for assigning an IP address to the cloned virtual machine.   | Boolean   | Yes   |
| DNS Name   | The complete domain name for the cloned virtual machine.   | String   | No   |
| DNS Server   | The name of the DNS server to resolve name requests for the cloned virtual machine.   | String   | No   |
| DNS Suffix   | The DNS Suffix that will be assigned to the network adapter of the cloned virtual machine. For example, example.com.   | String   | No   |
| Domain Name   | The domain of the cloned virtual machine.   | String   | No   |
| Domain User Name   | The domain user account that has permission to add the computer to the domain.   | String   | No   |
| Domain User Password   | The password of the domain user account.   | String   | No   |
| Gateway   | The gateway for the cloned virtual machine.   | String   | No   |
| Include Server License Information   | Indicates whether configuring the Windows Server license is part of the cloning process.   | Boolean   | Yes   |
| IP Address   | The IP address assigned to the cloned virtual machine.   | String   | No   |
| License Mode   | The type of license mode configured for the Windows Server licensing settings.   | String   | Yes   |
| Maximum Connections   | The maximum number of client connections configured as part of the Windows Server licensing settings.   | Integer   | No   |
| Computer Membership   | The name of the workgroup if the computer is part of a Windows workgroup, or the domain name if the computer is part of an Active Directory domain.   | String   | Yes   |
| Organization Name   | The name of the owner's organization of the cloned virtual machine.   | String   | No   |
| Owner's Name   | The name of the owner of the cloned virtual machine.   | String   | No   |
| Power on after creation   | Indicates whether the cloned virtual machine is turned on after it is created.   | Boolean   | Yes   |
| Product ID   | The product ID of the cloned virtual machine. You must add a dash after every fifth character to divide the product ID number into five parts. For example, enter AAAAA-BBBBB-CCCCC-DDDDD-EEEEE. | String   | No   |
| Subnet Mask   | The subnet mask for the cloned virtual machine.   | String   | No   |
| Workgroup   | The name of the workgroup the cloned virtual machine belongs to.   | String   | No   |

### Clone Windows VM Activity Published Data

| Name   | Description   | Value Type |
| Clone Task Timeout in seconds   | The timeout setting for the clone operation.   | Integer   |
|:---|:---|:---|
| Computer Membership   | The name of the workgroup if the computer is part of a Windows workgroup, or the domain name if the computer is part of an Active Directory domain. | String   |
| Computer Name   | The name of the computer.   | String   |
| Customize   | Indicates whether the virtual machine settings are customized after cloning.   | Boolean   |
| Datastore Path   | The path of the data store.   | String   |
| DHCP (not available in System Center 2016) | Indicates the type of IP address allocation of the cloned virtual machine: DHCP or static.   | Boolean   |
| DNS Name   | The complete domain name for the cloned virtual machine.   | String   |
| DNS Server   | The name of the DNS server to resolve name requests for the cloned virtual machine.   | String   |
| DNS Suffix   | The DNS Suffix that will be assigned to the network adapter of the cloned virtual machine. For example, example.com.   | String   |
| Domain Name   | The name of the domain that the cloned virtual machine uses.   | String   |
| Domain User Name   | The username that the cloned virtual machine uses to connect to the domain.   | String   |
| Domain User Password   | The password of the domain user account.   | String   |
| Folder Path   | The path to the destination folder for the cloned virtual machine.   | String   |
| Gateway   | The gateway that the cloned virtual machine uses.   | String   |
| Host System Path   | The path to the destination host system.   | String   |
| IP Address   | The static IP address of the cloned virtual machine.   | String   |
| Include Server License Information   | Indicates whether configuring the Windows Server license is part of the cloning process.   | Boolean   |
| License mode   | The type of license mode configured for the Windows Server licensing settings.   | String   |
| Maximum Connections   | The maximum number of client connections configured as part of the Windows Server licensing settings.   | Integer   |
| Memory Size (MB)   | The amount of memory, in megabytes, assigned to the cloned virtual machine.   | Integer   |
| Organization Name   | The organization name.   | String   |
| Owner's Name   | The name of the owner of the cloned virtual machine.   | String   |
| Power on after creation   | Indicates whether the cloned virtual machine is turned on after it is created.   | Boolean   |
| Product ID   | The Windows product ID.   | String   |
| Resource Pool Path   | The path to the resource pool used by the cloned virtual machine.   | String   |
| Source VM/Template Path   | The name of the virtual machine or template to clone.   | String   |
| Subnet Mask   | The subnet mask for the cloned virtual machine.   | String   |
| New Virtual Machine Name   | The name of the cloned virtual machine.   | String   |
| Virtual Processors   | The number of virtual processors assigned to the cloned virtual machine.   | Integer   |
| Workgroup   | The name of the workgroup for the cloned virtual machine.   | String   |

## Configuring the Clone Windows VM Activity

The following procedure describes the steps required to configure a Clone Windows VM activity.

#### To configure the Clone Windows VM Activity

1.  From the **Activities** pane, drag a **Clone Windows VM** activity to the active runbook.

2.  Double-click the **Clone Windows VM** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, click the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Click **Finish**.


