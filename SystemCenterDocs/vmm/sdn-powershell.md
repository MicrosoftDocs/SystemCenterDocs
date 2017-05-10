---
ms.assetid: dd9c6826-5cc4-482e-947d-bb645d64f3f9
title: Set up Software Defined Network (SDN) components in the VMM fabric using PowerShell
description: This article describes how to use PowerShell to deploy SDN components in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  05/10/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Set up Software Defined Network (SDN) components in the VMM fabric using PowerShell

>Applies To: System Center 2016- Virtual Machine Manager

System Center 2016 - Virtual Machine Manager (VMM) can be used to deploy and manage a Software Defined Network (SDN) infrastructure.

You can deploy SDN components in the VMM fabric, including:

- **Network Controller**: The network controller allows you to automate configuration of your network infrastructure, instead of manually configuring network devices and services.
- **RAS Gateway for SDN**: RAS Gateway is a software-based, multitenant, BGP capable router in Windows Server 2016 that is designed for CSPs and Enterprises that host multiple tenant virtual networks using HNV.
- **Software Load Balancing (SLB) for SDN**: SDN in Windows Server 2016 can use Software Load Balancing (SLB) to evenly distribute tenant and tenant customer network traffic among virtual network resources. The Windows Server SLB enables multiple servers to host the same workload, providing high availability and scalability.

There are a couple of ways to deploy these components:

- **VMM console**: Deploy the [network controller](sdn-controller.md), [SLB](sdn-slb.md), and [RAS gateway](sdn-gateway.md) manually in the VMM console.
- **PowerShell**: Deploy all components using PowerShell scripts.

## Advantages of PowerShell deployment

- Deploy all SDN components with PowerShell scripts.
- Using a script can reduce the introduction of manual errors, and save significant deployment time.
- If you deploy using the script, afterwards you can modify settings in the VMM console, just as you would if you deploy the SDN components manually.
- Like the manual deployment, you have the option of setting up a new management logical network and switch, or to reuse an existing network and switch.
- If the script deployment fails, all changed settings are rolled back, so that you can start again.
- You can turn off deployment for specific components, For example, if you already have network controller deployed, you can deploy SLB and RAS gateway only.


## Before you start

- SET-enabled switch deployment isn't currently supported in a PowerShell deployment. You need to deploy the SET-enabled switch out-of-band, and then specify the name of the switch during deployment.
- Check you have the prerequisites for SDN component deployment in place:
    - [Network controller prerequisites](sdn-controller.md#before-you-start)
    - [SLB prerequisites](sdn-slb.md#before-you-start)
    - [RAS gateway prerequisites](sdn-gateway.md#before-you-start)

## Deployment steps

Here's what you need to do to set up SDN components in VMM with PowerShell.


1. **Configure hosts and physical network infrastructure**: You need access to your physical network devices to configure VLANs, routing etc. You also need Hyper-V hosts to host the SDN infrastructure and tenant VMs. [Learn more](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure).
2. [Prepared virtual hard disk](sdn-controller.md#prepare-a-virtual-hard-disk) for the service templates in VHD or VHDX format.
3. Download the [network controller](sdn-controller.md#download-the-network-controller-service-template) service template, the [SLB service](sdn-slb.md#download-the-service-template) template, and the [RAS gateway](sdn-gateway.md#download-the-service-template) service template.
4. Import the [network controller](sdn-controller.md#import-the-template), [SLB](sdn-slb.md#import-the-service-template), and [RAS gateway](sdn-gateway.md#import-the-service-template) templates into the VMM library.
5. [Set up Active Directory security groups](sdn-controller.md#set-up-active-directory-groups). One for network controller management, and another for network controller clients. Each group will need at least one user account in it.
6. [Set up a VMM library share](sdn-controller.md#create-a-library-share-for-logging).You can have an optional library file share for keeping diagnostic logs. This library share will be accessed by the network controller to store diagnostics information throughout its lifetime.
7. [Set up a dedicated VMM host group](sdn-controller.md#set-up-host-groups) for all SDN Hyper-V hosts. Note that hosts must be running the latest version of Windows Server 2016, and have the Hyper-V role enabled.
8. [Set up a certificate](sdn-controller.md#set-up-the-security-certificates). You need an SSL certificate for HTTPS communications between VMM and the network controller.
9. [Download](https://github.com/manishmsft/SDN/tree/master/VMM/VMM%20SDN%20Express) and run the SDN scripts. There are three scripts:

    - **VMMExpress.ps1**: This script deploys the SDN stack. After you download it, you can your own customizations.
    - **Fabricconfig.psd1**: This file accepts all the inputs for setting up SDN.
    - **Fabricconfig_Example.psd1**: A sample file that contains dummy parameters. You can replace those with your own parameters.

## Next steps

[Configure hosts and physical network infrastructure for SDN ](https://technet.microsoft.com/windows-server-docs/networking/sdn/plan/plan-a-software-defined-network-infrastructure).
