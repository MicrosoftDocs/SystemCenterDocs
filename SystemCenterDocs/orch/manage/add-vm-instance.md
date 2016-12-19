---
title: Add VM Instance
description: The Add VM Instance activity adds a virtual machine to an existing deployment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f142536a-1a83-42d6-aab3-9ad72799942e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Add VM Instance
===============

Applies To: System Center 2016 - Orchestrator

The **Add VM Instance** activity adds a virtual machine to an existing deployment. It is part of the Azure Virtual Machines category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Add VM Instance Required Properties
-----------------------------------

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Service Name   | Specifies the cloud service in which to create the virtual machine.   | String   |
| Deployment Name   | Specifies the deployment in which to create the virtual machine.   | String   |
| Use Default Template   | Whether to use a default template or a raw configuration file to create the virtual machine.   | True, False   |
| VM Instance Name   | Specifies the name for the virtual machine. The name must be unique within Windows Azure.   | String   |
| Image Type   | Whether to use a Windows Azure platform image or a user disk for the VM's source image.   | PlatformImage, UserDisk   |
| Operating System Type   | The operating system type for the VM.   | Windows, Linux   |
| Computer Name   | Specifies the computer name for the virtual machine.   | String   |
| Admin Password   | Specifies the base-64 encoded string representing the administrator password to use for the virtual machine.   | String   |
| Reset password on first logon   | Specifies whether the user must change the administrator password on first logon.   | True, False   |
| Enable Automatic Updates   | Specifies whether automatic updates are enabled for the virtual machine.   | True, False   |
| Add Endpoint   | Whether to add an external endpoint to the virtual machine or not.   | True, False   |
| Endpoint Local Port   | Specifies the internal port on which the virtual machine is listening to serve the endpoint.   | Integer   |
| Endpoint Name   | Specifies the name for the external endpoint.   | String   |
| Endpoint Public Port   | Specifies the external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | Specifies the transport protocol for the endpoint.   | TCP, UDP   |
| Blob URI to create the VHD   | Specifies the location within the storage account to save the created vhd file.   | String   |
| Source Image Name   | Specifies the name of the disk image to use to create the virtual machine.   | String   |
| VM Instance Size   | The size of the virtual machine to allocate.   | ExtraSmall, Small, Medium, Large, ExtraLarge |
| Host Name   | Specifies the host name for the VM.   | String   |
| User Name   | Specifies the name of a user to be created in the sudoer group of the virtual machine.   | String   |
| User Password   | Specifies the associated password for the user name. Passwords are ASCII character strings 6 to 72 characters in length. | String   |
| Disable SSH Password Authentication | Specifies whether or not SSH password authentication is disabled.   | True, False   |
| XML Configuration File Path   | The path to the configuration file to use to create the virtual machine.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

Add VM Instance Optional Properties
-----------------------------------

There are no optional properties for this activity.

Add VM Instance Published Data
------------------------------

| **Element**   | **Description**   | **Value type**   |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Service Name   | Specifies the cloud service in which to create the virtual machine.   | String   |
| Deployment Name   | Specifies the deployment in which to create the virtual machine.   | String   |
| Use Default Template   | Whether to use a default template or a raw configuration file to create the virtual machine.   | True, False   |
| VM Instance Name   | Specifies the name for the virtual machine. The name must be unique within Windows Azure.   | String   |
| Image Type   | Whether to use a Windows Azure platform image or a user disk for the VM's source image.   | PlatformImage, UserDisk   |
| Operating System Type   | The operating system type for the VM.   | Windows, Linux   |
| Computer Name   | Specifies the computer name for the virtual machine.   | String   |
| Reset password on first logon   | Specifies whether the user must change the administrator password on first logon.   | True, False   |
| Enable Automatic Updates   | Specifies whether automatic updates are enabled for the virtual machine.   | True, False   |
| Add Endpoint   | Whether to add an external endpoint to the virtual machine or not.   | True, False   |
| Endpoint Local Port   | Specifies the internal port on which the virtual machine is listening to serve the endpoint.   | Integer   |
| Endpoint Name   | Specifies the name for the external endpoint.   | String   |
| Endpoint Public Port   | Specifies the external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | Specifies the transport protocol for the endpoint.   | TCP, UDP   |
| Blob URI to create the VHD   | Specifies the location within the storage account to save the created vhd file.   | String   |
| Source Image Name   | Specifies the name of the disk image to use to create the virtual machine.   | String   |
| VM Instance Size   | The size of the virtual machine to allocate.   | ExtraSmall, Small, Medium, Large, ExtraLarge |
| Host Name   | Specifies the host name for the VM.   | String   |
| User Name   | Specifies the name of a user to be created in the sudoer group of the virtual machine.   | String   |
| Disable SSH Password Authentication | Specifies whether or not SSH password authentication is disabled.   | True, False   |
| XML Configuration File Path   | The path to the configuration file to use to create the virtual machine.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

