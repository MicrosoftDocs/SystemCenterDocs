---
ms.assetid: f327b30f-ff15-4460-be00-dd4fa1a665f5
title: Add VM templates to the VMM library
description: This article provides guidance for adding VM templates to the library in the VMM compute fabric
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 07/02/2018
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Add VM templates to the VMM library

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Read this article to learn about VM templates and how to manage them in the System Center - Virtual Machine Manager (VMM) library.

Templates help you to create VMs with consistent settings. VMM provides two types of templates:

- VM templates are database objects that are stored in the VMM library. They're used to quickly set up VMs.
- [Service templates](library-resources.md) define how a service is configured. They include information about the VMs that are deployed as part of the service, which applications to install on VMs, and the network settings that should be used. Service templates usually contain VM templates.

There are two methods for creating a VM template:

- From an existing virtual hard disk or VM template in the VMM library.

  > [!NOTE]
  > Ensure the virtual hard disk was Sysprepped.

- From an existing VM deployed on a host.

## Before you start

- You can base a new VM template on an existing VM template or on a virtual hard disk that is stored in the library. You can configure hardware settings, guest operating system settings, application installation, and Microsoft SQL Server instances. You can configure each of these settings manually or you can import the settings from an existing profile.
- Static IP address settings are available only when you deploy a VM from a VM template.
- If you create a VM template  based on Linux, some of the Linux-specific settings, such as operating system specialization, work only if you deploy the Linux-based VM on a Hyper-V host.
- The option to create a VM template that's based on an existing VM on a host isn't applicable for Linux-based virtual machine templates.
- Application deployment, SQL Server deployment, and configurable service settings only apply when you deploy a VM as part of a service.
- If you grant rights for a particular template to a user that does not have rights to the Run As account that's specified in the template, then the user can potentially extract the credentials for the Run As account from the template during deployment.
- Before creating a template based on a VM, you'll need to create a new local administrator account on that VM. Using the default built-in administrator account will cause Sysprep to fail. In addition, make sure that the VM isn't joined to a domain.

## Create a VM template based on an existing VHD or VM template in the library

1. Click **Library** > **Create** > **Create VM Template**.
2. In  the Create VM Template Wizard, select **Source** > **Use an existing VM template or virtual hard disk stored in the library**. Select the disk or template in **Select VM Template Source**.
3. In **Identity**, type in a template name and description.
4. In **Configure Hardware**, specify the hardware settings. You can select to use an existing hardware profile. Note that the profile and hardware options will depend on which you're configuring - generation 1 or generation 2 VMs. To learn more, review [how to create a hardware profile](library-profiles.md#create-a-hardware-profile).
5. In **Configure Operating System**, specify the machine settings. You can use a guest OS profile or configure specific settings. To learn more, review [how to create a guest OS profile](library-profiles.md#create-a-guest-os-profile).
6. In **Configure Applications**, set up app settings. This isn't relevant if you're using the VM template to deploy VMs that aren't part of a service. To learn more, review [how to create an application profile](library-profiles.md#create-an-application-profile). If you're configuring SQL Server set in up in **Configure SQL Server**, review [how to create a SQL Server profile](library-profiles.md#create-a-sql-server-profile).
7. In **Summary**, review the settings and click **View Script** if you want to see the script that will be used to create the template. Then click **Create**. In **Jobs**, you can track the template being created. Wait for the **Completed** status.
8. When you create a VM you'll be able to create it based on the template you've just created.

## Create a VM template based on a VM deployed on a host

1. Click **Library** > **Create** > **Create VM Template**.
2. In  the Create VM Template Wizard > select **Source** > **From an existing virtual machine that is deployed on a host**. Select the VM in **Select VM Template Source**.
3. In **Identity**, type in a template name and description. Note that the template will destroy the source VM and data on it could be lost. Clone it if it's important to you.
4. In **Configure Hardware**, click **Next**.

5. In **Configure Operating System**, specify the guest operating system settings. You can use a guest OS profile or configure specific settings. To learn more, review [how to create a guest OS profile](library-profiles.md#create-a-guest-os-profile).
6. In **Select Library Server**, click the library server for the VM you're using for the template and in **Select Path** specify the share/folder.
7. In **Summary**, review the settings and click **Create**. In **Jobs**, you can track the template being created. Wait for the **Completed** status.

You can create VMs based on the template you've just created.

::: moniker range=">sc-vmm-2016"

## Assign a storage QoS policy template

1. After step 3 in the [previous procedure](#create-a-vm-template-based-on-a-vm-deployed-on-a-host), in **Configure Hardware**, click  **Advanced** under **Bus configuration**, and select appropriate option under **Storage QoS Policy**.

2. Proceed with rest of the steps to complete the wizard.

::: moniker-end

## Next steps

Review the following on how to [create VMs based on the template](vm-template.md) you've just created.
