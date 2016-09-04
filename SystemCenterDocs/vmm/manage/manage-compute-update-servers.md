---
title: Set up Update servers in the VMM compute fabric
description: This article describes how to set up update servers in the VMM fabric
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-09-04
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Set up update servers in the VMM compute fabric

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Read this article to set up update servers in the System Center 2016 - Virtual Machine Manager (VMM) fabric. The article includes prerequisites, instructions for adding a WSUS server to the fabric, explains how to set update baselines and how to run a scan. You can also create update exemptions.

## Overview

You can deploy update servers in the VMM fabric to manage compliance and remediation for virtualization hosts, library servers, the VMM management server, PXE servers, the WSUS server itself, and any infrastructure servers running Windows Server 2012 R2 or later.

1. Add a WSUS server to the VMM fabric
2. Create and assign update baselines
3. Scan computers for compliance


## Before you start

- A WSUS server must be running a 64-bit edition of Windows Server Update Service (WSUS) 3.0 with SP2 or later. If you're using version 3.0 with SP2 you must install KB [2734608](http://go.microsoft.com/fwlink/p/?LinkID=268122). From Windows Server 2012 onwards WSUS is an integrated server role.
- The WSUS server must be running Windows Server 2008 R2 with SP1 or a later operating system.
- The WSUS server must be in the same domain as the VMM server, or in a domain with full trust.
- VMM can use a WSUS root server or downstream WSUS server. You can't use a WSUS replica server.
- The WSUS server can be dedicated to VMM or an existing server.
- The WSUS server can be installed on the VMM management server but if you'll be processing a large number of updates we recommend a separate server.
- VMM can work with System Center Updates Publisher but only full content updates are supported. Metadata-only updates can't be added to a baseline.
- After you add a WSUS server to VMM you should manage it in the VMM console and not in the WSUS console. In VMM, you update the properties of the update server to configure a proxy server for synchronizations and to change the update categories, products, and supported languages that are synchronized by the WSUS server.
- In VMM, administrators and delegated administrators manage fabric updates. Only administrators can manage the update server and synchronize updates. Delegated administrators can scan and remediate updates on computers that are within the scope of their user roles. Delegated administrators can use baselines created by administrators and other delegated administrators. But delegated administrators cannot modify or delete baselines created by others.


## Add a WSUS server to the VMM fabric

1. Ensure that the server is running the WSUS role.
2. Click **Fabric** > **Home** > **Add** > **Add Resources** > **Update Server**.
3. In **Add Windows Server Update Services Server**, specify the name, port, and credentials of the WSUS server. The account needs admin rights on the server. Use an existing Run As account or create a new one. Specify whether you want to use SSL for connections.
4. The WSUS server will be added to the fabric, followed by initial synchronization of the updates catalog. This could take a while. Monitor status in the **Add Update Server** and **Synchronize Update Server** jobs.
5. After the server is added, you can update its properties to configure a proxy server for synchronization. In **Fabric** > **Servers** > **Update Server** > **Properties**, click the **Proxy Server** tab. Configure WSUS to use a proxy server when configuring updates, or update the port for an existing proxy server.
6. In addition, you can click **Update Classification** to select the update classification that you want to synchronize, click **Product** to select the products that want to include when synchronizing, and **Language** to select the supported synchronization languages.

After you've added the server you can update the WSUS settings and perform manual synchronization in **Servers** > WSUS server name > **Update Server**.


## Add WSUS servers that are managed in Configuration Manager

If you want to add an existing WSUS server from a Configuration Manager environment to the VMM fabric you'll need to do the following:

1. Create a collection in Configuration Manager and add any servers that you'd like to add to the VMM fabric.
2. Exclude this collection from any software update deployments delivered by Configuration Manager. This ensures that VMM controls update management for the servers. You'll still be able to view compliance information for the collection in Configuration Manager reports.
3. If you want to include VMM compliance information in Configuration Manager, create an update group in Configuration Manager that contains all of the updates for which you want to measure compliance for the machines that will be in the VMM fabric. This  update group is only for reporting. Don't deploy it to the machines managed by VMM.
4. Now add the WSUS server as described above.
5. After adding the server, select **Update Server** > **Properties** > **General** > **Allow Update Server configuration changes**.

## Create and assign update baselines

After you've added the WSUS server to the fabric you can configure update baselines. An update baseline contains a set of required updates scoped to an object such as a host group, a standalone host, a host cluster, a VMM management server, or an infrastructure server.

- Update baselines can be assigned to host groups and to individual computers based on their role in VMM.
- Update baselines that are assigned to a host group are applied to all stand-alone hosts and host clusters in the host group, as well as the stand-alone hosts and host clusters in child host groups.
- During a compliance scan, computers that are assigned to a baseline are graded for compliance with their assigned baselines. After a computer is found noncompliant, an administrator brings the computer into compliance through update remediation.
- If a host is moved from one host group to another, the baselines for the new host group are applied to the host, and the baselines for the preceding host group no longer apply - that is, unless the baseline is assigned to both host groups. Explicit baseline assignments to a managed host stay with the host when it is moved from one host group to another. It is only when the baseline is assigned to a host group that baseline assignments get revoked during the move.
- You can use two methods to prepare update baselines for remediation:
	- A VMM built-in update baseline: Sample Baseline for Critical Updates and Sample Baseline for Security Updates.
	- A custom update baseline.


### Assign servers to a build-in baseline

1. Click **Library** > **Update Catalog and Baselines** > **Update Baselines**.
2. In **Baselines**, click the baseline you want to use.
3. Click **Home** > **Properties** > **Updates** for the baseline. In **Updates**, add or remove baselines as required. To ensure all security updates are remediated don't remove anything.
4. Click **Assignment Scope**, and select the host groups, clusters, standalone servers, and infrastructure servers to add to the baseline. Or click **All Hosts** to add all.

### Assign servers to a custom baseline

1. Click **Library** > **Update Catalog and Baselines** > **Update Baselines**.
2. Click **Home** > **Create** > **Baseline** for the baseline.
3. In **Update Baseline Wizard** > **General**, specify a name and description.
4. In **Update**, add the updates you want to include.
5. In **Assignment Scope**, expand **Host Groups** and **Infrastructure**. Select the groups and servers you want to add.
6. In **Summary**, click **Finish**, and accept the **Microsoft License Terms** if needed to install any of the updates. Verify the baseline in **Library** > **Update Catalog and Baselines** > **Baselines**.

## Scan for update compliance

After you assign computers to an update baseline you can scan them to determine their compliance status for the baselines. When a computer is scanned for compliance.

- WSUS checks each update in the assigned update baselines to determine whether the update is applicable and if the update is applicable, whether the update has been installed.
- After a compliance scan, for every computer, each update has a compliance status of Compliant, Non Compliant, Error, Pending Reboot, or Unknown. You can view compliance properties for additional information.
- The compliance scan focuses only on the updates that the administrator has identified as important by adding them to a baseline. That enables organizations to monitor for compliance for what is deemed important for their organization.
- The following changes can cause an Unknown update status for a computer, and should be followed by a scan operation to access the computer's compliance status:
	- A host is moved from one host group to another host group.
	- An update is added to or removed from a baseline that is assigned to a computer.
	- The computer is added to the scope of a baseline.

To check compliance:

1. Click **Fabric** > **Servers**
2. In **Home** > **Show** click **Compliance**.
3. Since you haven't yet scanned computers the compliance status will show as **Unknown**, with an operational status **Pending Compliance Scan**.
4. Select the computers you want to check, and click **Scan**.
5. While the scan is in progress status will be Unknown. After it's finished compliance status for each update will be **Compliant**, **Non-Compliant**, or **Error**.



## Manage update exemptions

You can create update exemptions for specific machines. For example if an update has caused the machine to be in an unhealthy state, you could uninstall the update out-of-band and then exempt the machine from the update until the issue is resolved. When the compliance scan next runs the machine will show as **Non Compliant**.

1. Click **Fabric** > **Home** > **Show** > **Compliance**. Then on the **Fabric** node, click **Servers** and navigate to the server you want to exempt.
2. In the result pane expand the update baselines for the machine and click the update to select it.
3. Click **Compliance** > **Compliance Properties**.
4. In **Compliance Properties**, select the update > **Create**.
5. In **Create Exemption**, add notes about the reason and the expected exemption data. Change the update status to **Exempt**.
6. After you've resolved the issue and you want to cancel the exemption so that the machine is compliant again, in **Compliance Properties** select the exemption > **Delete** > **Yes**.
7. To return the server to a compliant state, select the non-compliant server and click **Remediate** on the **Compliance** tab.
