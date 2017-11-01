---
ms.assetid: 3e85d403-e8dc-40b0-a578-0caee2b3ee1f
title: Deploy a private VMM cloud
description: This article provides an overview of private cloud deployment in VMM
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 11/01/2017
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---


# Scenario: Deploy a private VMM cloud

>Applies To: System Center 2016 - Virtual Machine Manager

This article provides an overview of System Center - Virtual Machine Manager (VMM) private clouds.

A private cloud is a cloud that is provisioned and managed on-premises by an organization. It's deployed using an organization’s own hardware to leverage the advantages of a private cloud model.

You can use VMM to create and deploy private cloud components, and to manage access to the private cloud and the underlying physical resources. VMM provides the following benefits:

- **Self-service**—Self-service admins can delegate management and usage of the private cloud, while having no knowledge of underlying physical resources. They don't have to ask the private cloud provider for administrative changes, except to request increased capacity and quotas as required.
- **Opacity**—Self-service admins don't need any knowledge of underlying physical resources.
- **Resource pooling**—Administrators can collect and present an aggregate set of resources, such as storage and networking resources. Resource usage is limited by the capacity of the private cloud and by user role quotas.
- **Elasticity**—Administrators can add resources to a private cloud to increase the capacity.
- **Optimization**—Usage of the underlying resources is continually optimized without affecting the overall private cloud user experience.

You can create a private clouds from either:

- VMM host groups that contain resources from virtualization hosts.
- A VMware resource pool

You deploy a private cloud by configuring fabric resources, settings up library paths for private cloud users, and setting cloud capacity.

## Next steps

- [Create a private cloud in VMM](cloud-create.md)
