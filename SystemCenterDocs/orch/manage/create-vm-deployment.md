---
title: Create VM Deployment
description: The Create VM Deployment activity provisions a virtual machine based on the supplied configuration.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f779ed1b-43a0-4063-be59-905713b2969a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Create VM Deployment
====================

Applies To: System Center 2016 - Orchestrator

The **Create VM Deployment** activity provisions a virtual machine based on the supplied configuration. It is part of the **Azure Virtual Machines** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Create VM Deployment Required Properties
----------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service Name   | Specifies the cloud service in which to create the deployment.   | String   |
| Deployment Name   | A name for the deployment. The deployment name must be unique among other deployments for the cloud service.   | String   |
| Use Default Template   | Whether to use a default template or a raw configuration file to create the deployment.   | True, False   |
| Deployment Slot   | Specifies the environment in which to deploy the virtual machine.   | Staging, Production   |
| Label   | A label for the deployment.   | String   |
| Role Name   | Specifies the name for the virtual machine. The name must be unique within Windows Azure.   | String   |
| Image Type   | Whether to use a Windows Azure platform image or a user disk for the VM's source image.   | PlatformImage, UserDisk   |
| Operating System Type   | The operating system type for the VM.   | Windows, Linux   |
| Computer Name   | Specifies the computer name for the virtual machine.   | String   |
| Admin Password   | Specifies the base-64 encoded string representing the administrator password to use for the virtual machine.   | String   |
| Reset password on first logon   | Specifies whether the user must change the administrator password on first logon.   | True<br>False   |
| Enable Automatic Updates   | Specifies whether automatic updates are enabled for the virtual machine.   | True<br>False   |
| Add Endpoint   | Whether or not to add an external endpoint to the virtual machine.   | True<br>False   |
| Endpoint Local Port   | Designates the internal port on which the virtual machine is listening to serve as the endpoint.   | Integer   |
| Endpoint Name   | The name for the external endpoint.   | String   |
| Endpoint Public Port   | The external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | The transport protocol for the endpoint.   | TCP<br>UDP   |
| Container URI   | Specifies the location of the container within the storage account in which to save the created virtual hard disk.   | String   |
| Source Image Name   | Specifies the name of the disk image to use to create the virtual machine.   | String   |
| VM Instance Size   | The size of the virtual machine to allocate.   | ExtraSmall, Small, Medium, Large, ExtraLarge |
| Host Name   | Specifies the host name for the VM.   | String   |
| User Name   | Specifies the name of a user to be created in the sudoer group of the virtual machine.   | String   |
| User Password   | Specifies the associated password for the user name. Passwords are ASCII character strings 6 to 72 characters in length. | String   |
| Disable SSH Password Authentication | Specifies whether or not SSH password authentication is disabled.   | True, False   |
| XML Configuration File Path   | The path to the configuration file to use to create the deployment.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

Create VM Deployment Optional Properties
----------------------------------------

There are no optional properties for this runbook activity.

Create VM Deployment Published Data
-----------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Service Name   | Specifies the cloud service in which to create the deployment.   | String   |
| Deployment Name   | A name for the deployment. The deployment name must be unique among other deployments for the cloud service.   | String   |
| Use Default Template   | Whether to use a default template or a raw configuration file to create the deployment.   | Boolean   |
| Deployment Slot   | Specifies the environment in which to deploy the virtual machine.   | String   |
| Label   | A label for the deployment.   | String   |
| VM Instance Name   | Specifies the name for the virtual machine. The name must be unique within Windows Azure.   | String   |
| Image Type   | Whether to use a Windows Azure platform image or a user disk for the VM's source image.   | String   |
| Operating System Type   | The operating system type for the VM.   | String   |
| Computer Name   | Specifies the computer name for the virtual machine.   | String   |
| Reset password on first logon   | Specifies whether the user must change the administrator password on first logon.   | Boolean   |
| Enable Automatic Updates   | Specifies whether automatic updates are enabled for the virtual machine.   | Boolean   |
| Add Endpoint   | Whether or not to add an external endpoint to the virtual machine.   | Boolean   |
| Endpoint Local Port   | The internal port on which the virtual machine is listening.   | Integer   |
| Endpoint Name   | The name for the external endpoint.   | String   |
| Endpoint Public Port   | The external port to use for the endpoint.   | Integer   |
| Endpoint Protocol   | The transport protocol for the endpoint.   | String   |
| Container URI   | Specifies the location of the container within the storage account in which to save the created virtual hard disk. | String   |
| Blob VHD Name   | Specifies the file name for the virtual hard disk.   | String   |
| Source Image Name   | Specifies the name of the disk image to use to create the virtual machine.   | String   |
| VM Instance Size   | The size of the virtual machine to allocate.   | String   |
| Host Name   | Specifies the host name for the VM.   | String   |
| User Name   | Specifies the name of a user to be created in the sudoer group of the virtual machine.   | String   |
| Disable SSH Password Authentication | Specifies whether or not SSH password authentication is disabled.   | Boolean   |
| XML Configuration File Path   | The path to the configuration file to use to create the deployment.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | Boolean   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

