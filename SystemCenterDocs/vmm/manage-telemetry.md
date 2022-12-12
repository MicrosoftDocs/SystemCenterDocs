---
ms.assetid: f0f2b1aa-d9a3-4044-b419-be868da35ec9
title: Manage VMM Telemetry settings
description: This article provides information about how to turn off/on telemetry in system center VMM.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 04/13/2018
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Manage telemetry settings in VMM

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article provides information about how to turn on/off the telemetry settings in System Center - Virtual Machine Manager (VMM).

> [!NOTE]
> Microsoft does not collect any personal data from the customers. We only listen to events that would help diagnostics in VMM. [Learn more](#telemetry-data-collected)


## Turn on/off telemetry in VMM
Use the following procedure:
1. On the VMM console, select **Settings** .

   **General** settings window appears with available list of settings.
2. Select **Diagnostics and Usage Data Settings**.

   ![Screenshot of Diagnostics and Usage.](./media/telemetry/diagnostics-and-usage-data.png)

   Page with **Do you want to send Diagnostics and Usage Data to Microsoft** message appears with an option to select either Yes or No.

   ![Screenshot of Diagnostics and Usage Data Settings.](./media/telemetry/telemetry-selection-options.png)

   > [!NOTE]
   > We recommend you to go through the privacy statement provided on this page before making a selection.

3. To turn on telemetry, select **Yes I am willing to send data to Microsoft**.

4. To turn off telemetry, select **No I prefer not to send data to Microsoft**.

## Telemetry data collected

| **Data related To** | **Data collected** |
| --- | --- |
| **Census Data** | Unique ID generated for the VMM deployment <br /><br /> VMM build version <br /><br />ID used for correlation with other System Center products |
| **Assurance Data** | Information about the VMM deployment - whether guardian service deployment or not <br /><br /> Count of guarded hosts being managed <br /><br />Count of hosts being managed <br /><br />Count of shielded VM templates <br /><br />Count of VM templates <br /><br /> Count of shielded VMs <br /><br />Count of VMs <br /><br /> Count of shielded clouds <br /><br />Count of guarded hosts in a cluster <br /><br />Count of guarded hosts in standalone deployments <br /><br />Count of code integrity policy in Global Settings <br /><br /> Count of Physical Computer Profile (PCP) with host guarding set <br /><br />If the VMM deployment is a guardian service deployment and OM integrated <br /><br /> If the VMM deployment is a guardian service deployment and WSUS integrated <br /><br /> Count of hosts with attestation mode as TPM<br /><br /> Count of hosts with attestation mode as AD <br /><br /> Count of CI policies existing in a library <br /><br /> Count of hosts being managed <br /><br /> Count of DMZ hosts being managed  <br /><br /> Count of Hyper-v hosts <br /><br /> Count of clusters <br /><br /> Count of non-trusted hosts being managed <br /><br />Information if customer is managing the VMWare hosts<br /><br />Minimum, maximum, and average host cluster size <br /><br />Minimum, maximum, and average host memory size <br /><br /> Minimum, maximum, and average VMWare cluster size
| **Job related** | Indication if jobs are user initiated or background jobs<br /><br />Count of the number of times a job description type has failed<br /><br />Number of times job has run<br /><br />Maximum, minimum, and average number of jobs run per day |
| **Dynamic Optimization Settings** | Count of hosts considered for dynamic optimization<br /><br />Count of hosts considered for power optimization<br /><br />Minimum, maximum, and average frequency to run dynamic optimization |
| **Network** | Count of Edge NAT instances<br /><br />Count of Edge forwarding instances<br /><br />Count of Edge S2S instances<br /><br />Count of VPN connections<br /><br />Count of tenants per multi-tenant gateway<br /><br />Count of Edge load balancers<br /><br />Count of Edge load balancer VIP templates<br /><br />Count of NC managed VPN connections<br /><br />Count of NC managed IPsec VPN connections<br /><br />Count of NC managed GRE VPN connections<br /><br />Count of NC managed L3 VPN connections |
| **IP Pool** | Count of IPV4 and IPV6 address pools<br /><br />Maximum size of IPV4 and IPV6 pools<br /><br />Total reserved IPV4 and IPV6 addresses<br /><br />Average pool usage size<br /><br />Count of NC managed IPV4 and IPV6 addresses |
| **Library** | Count of library shared being managed<br /><br />Count of VHDs and VHDXs registered in the library<br /><br />Count of service templates registered in the library<br /><br />Count of VM templates registered in the library<br /><br />Count of host groups belonging to the library<br /><br />Count of equivalent resources registered in the library |
| **Logical Network** | Count of Logical networks<br /><br />Count of logical network definitions<br /><br />Count of one connected network managed by network controller<br /><br />Count of VLAN based independent networks<br /><br />Count of private VLAN networks |
| **Policy Distribution** | Minimum and maximum policy RTT<br /><br />Policy errors |
| **Service Objects** | Count of service instances<br /><br />Count of deployed service instances<br /><br />Count of failed service instances<br /><br />Count of servicing failed service instances<br /><br />Count of service instances deployed to non Hyper-V host groups<br /><br />Count of VM roles<br /><br />Count of applications<br /><br />Count of script applications<br /><br />Maximum, minimum and average tiers per service<br /><br />Count of services using application hosts<br /><br />Count of services using SQL application<br /><br />Count of services using Web deploy application<br /><br />Maximum, minimum, and average number of applications per customer, computer tier<br /><br />Count of service tiers with load balancers<br /><br />Count of services deployed on VMware |
| **VM** | Count of HA VM instances<br /><br />Count of Non HA VM instances<br /><br />Count of HA VM instances on clustered storage<br /><br />Count of HA VM instances on SMB share<br /><br />Count of DiffDisk VM instances<br /><br />Count of Hyper-V VM instances<br /><br />Count of VMWare VM instances<br /><br />Count of OS type, OS name, OS edition, OS version on VMs<br /><br />List of possible VM states<br /><br />Count of VMs per state
| **VM OS** | OS version of VMs<br /><br />OS name of the VMs<br /><br />OS edition of VMs<br /><br />OS Type of VMs<br /><br />Count of VMs for various OS<br /><br />List of possible VM states<br /><br />Count of VMs for each state |
| **VMM Settings** | Indication of highly available installation of VMM<br /><br />Indication if VMM is upgraded<br /><br />VMM SKU type<br /><br />Indication of VMM running as domain account<br /><br />Indication if VMM DB is on remote server<br /><br />Indication if VMM is running on a VM<br /><br />Indication if VMM is running on a default path<br /><br />Count of VM networks<br /><br />Count of VM subnets<br /><br />Count of NC managed VM networks and VM subnets |
| **Host OS** | OS version on the host<br /><br />OS name of the host<br /><br />SKU type of host<br /><br />Indication of Nano type host<br /><br />Number of hosts with specific OS |
| **Storage Inventory** | Count of all storage providers<br /><br />Count of SMIS CIMXML, SMIS WMI, Native Windows, SMP WMI storage providers<br /><br />Count of providers managing arrays<br /><br />Count of providers managing file shares<br /><br />Count of providers managing both arrays and file shares<br /><br />Count of providers managing FC fabric<br /><br />Count of storage classification defined by user<br /><br />Count of discs where custom classification is used to override inherited disk classification<br /><br />Count of disks where custom classification is used to override pool derived classification<br /><br />Count of fabric classifications<br /><br />Count of primary VMs for which HVR is enabled out of band<br /><br />Count of VMs for which HVR is enabled in band<br /><br />Count of LUN based protected replication groups created Out of Band<br /><br />Count of volume-based protected replication groups created Out of Band<br /><br />Count of volume-based protected replication groups created through Azure Site Recovery<br /><br />Indication if VMM is configured to be connected to Azure Site Recovery<br /><br />Count of QoS policies created in VMM<br /><br />Count of VMs with QoS policies applied |
| **Storage Hyper Converged cluster** | Count of Hyper  converged clusters <br /><br />Count of pools<br /><br />Count of virtual discs<br /><br />Count of volumes<br /><br />Count of local discs attached<br /><br />Average local disc size attached |
| **SAN Arrays** | Count of pools in storage array<br /><br />Count of managed pools in storage array<br /><br />Count of managed LUNs in all managed pools per array<br /><br />List of array capabilities<br /><br />Indication if array also has associated file share |
| **Storage Hosts** | Count of storage hosts or clusters<br /><br />Name of storage aggregate collection<br /><br />Maximum, minimum, average, median, and mode values of storage aggregate of collector |
| **File server storage** | List of total file shares on file server<br /><br />List of managed shares on file server<br /><br />Indication if there is calabria file share capability<br /><br />List of associated storage array capabilities<br /><br />List of SMB file share dialect supported by fileserver |
| **Telemetry Opt out** | Indication if Telemetry is opted out |
