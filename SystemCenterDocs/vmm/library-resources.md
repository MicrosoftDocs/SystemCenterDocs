---
ms.assetid: a3c877d9-c9f5-449f-bba9-0da7ec32db60
title: Add service templates to the VMM library
description: This article provides guidance for adding service templates to the library in the VMM compute fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Add service templates to the VMM library

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to learn about setting up service templates in the System Center 2016 - Virtual Machine Manager (VMM) library.

Service templates group VMs together to provide an app. They contain information about a service, including the VMs that are deployed as part of the service, the applications installed on VMs, and the network settings that should be used. You can add VM templates, network settings, applications, and storage to a service template.

Service templates can be single or multi tier:

- A single tier service contains one VM used as a specific app.
- A multi-tier service contains multiple VMs. For example you could create a three-tier service with a backend tier running a SQL Server database, a middle tier running the business server, and a third tier running a frontend web interface.
- Tiers can be added based on a copy of an existing VM template (which can be customized) or a virtual hard disk in the library.

You set up service templates using the VMM service template designer.

## Before you start

You can create service templates if you have VMM admin or delegated admin permissions, or if you have a self-service user account with **Author** enabled.

## Create a service template

1. Click **Library** > **Create** > **Create Service Template**.
2. In **New Service Template**  > **Name**, specify a template name. In **Release** indicate the template version.
3. To configure a tier using the predefined templates click in the designer workload and select a preconfigured tier pattern (blank, 1, 2, or 3 tiers). Click **Save and Validate** to save the template. After its created you can click on a template object to modify its name, release version or users/roles that can access it.
4. When the tier appears in the workspace drag a VM template to it. The properties of the VM template are applied to the tier. Note that this doesn't establish a link between the tier and the template. Changing the template properties does not modify the tier properties.

	NOTE: You can also click **Add Machine Tier** to add a tier manually. This opens the Create Machine Tier Template Wizard. In **Select Source** select a source for the tier. You can use an exact copy of an existing VM template, or to customize an existing VM template. Click **Browse** to select the template or hard disk. In **Additional Properties**, you'll configure the tier properties described in the next step.

5. You can click on a tier to access its properties in the details pane of the designer.  Click **View All Properties** to modify all the properties in a single view. Here's what you can modify when you select to view all:

	- In **General** specify:

		- The order in which tiers are deployed and serviced. For example if you need the database tier to be running in order to run a frontend web app, you'd set the database tier to 1.
		- Whether you want to be able to add additional VMs to the tier in order to scale out (you can scale out to 5 VM instances in a tier).
		- More than one upgrade domain to minimize service interruptions when a tier is updated. VMM will update VMs in the tier according to their upgrade domains. VMM upgrade an upgrade domain at a time. It shuts down VMs in the domain, updates them, brings them online, and moves to the next domain to reduce impact.
		- The creation of an availability set for the tier. The availability set helps VMs in the service remain available during maintenance. VMM tries to separate VMs in the same availability set by placing them on separate hosts.

	- In **Configure Hardware** you'll see the hardware settings for the associated VM template. You can select an alternative hardware profile, or configure hardware settings manually. [Learn more](library-profiles.md#create-a-hardware-profile).
	- In **Configure Operating System** you'll see the operating system settings for the associated VM template. you can select an alternative guest OS profile, or configure settings manually. [Learn more](library-profiles.md#create-a-guest-os-profile).
	- In **Application Configuration** or **SQL Server Configuration** you can select an application/SQL Server profile or configure settings for a new profile. Learn more about [application](library-profiles.md#create-an-application-profile) and [SQL Server](library-profiles.md#create-a-sql-server-profile) profiles.

## Add a VM network to the service template

You'll need to configure network settings for a tier by connecting the tier adapters to one or more [VM networks](network-virtual.md). To do this you'll add a logical network component and then use the connector tool to connect it to the adapter.

1. In the Service Template Designer, click **Service Template Components** > **Add VM Network**.
2. When the network appears as a component, use the Connector to connect to the appropriate NIC.

## Next steps

[Set up load balancing for a service tier](network-nlb.md)
