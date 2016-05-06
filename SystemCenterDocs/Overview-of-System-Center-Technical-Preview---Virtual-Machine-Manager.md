---
title: Overview of System Center Technical Preview - Virtual Machine Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e624ca43-e6a1-45b2-8f66-f732bbb9aa5c
---
# Overview of System Center Technical Preview - Virtual Machine Manager
[!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] is a management solution for the virtualized data center. You can use it to configure and manage your virtualization host, networking, and storage resources in order to create and deploy virtual machines and services to private clouds that you have created. This topic describes the following tasks:

-   [Deploying VMM](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_deploying)

-   [Configuring security for VMM](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_security)

-   [Configuring fabric resources in VMM](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_fabric)

-   [Deploying virtual machines and services in VMM](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_vms)

-   [Scalability](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_scalability)

-   [Managing the VMM environment](./Overview-of-System-Center-Technical-Preview---Virtual-Machine-Manager.md#BKMK_managing)

## <a name="BKMK_deploying"></a>Deploying VMM
A deployment of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] consists of the following.

|Name|Description|
|--------|---------------|
|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server|The computer on which the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] service runs. It processes commands and controls communications with the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database, the library server, and virtual machine hosts.|
|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database|A Microsoft SQL Server database that stores [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] configuration information such as virtual machine and service templates, and profiles.|
|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console|The program that you can use to connect to a [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server in order to centrally view and manage physical and virtual resources, such as virtual machine hosts, virtual machines, services, and library resources.|
|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library and [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library server|The catalog of resources \(for example, virtual hard disks, templates, and profiles\) that are used to deploy virtual machines and services.<br /><br />A library server hosts shared folders that are used to store file\-based resources in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library.|
|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] command shell|The Windows PowerShell–based command shell that makes available the cmdlets that perform all functions in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].|

For information about deploying [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], see [Deploying System Center 2016 - Virtual Machine Manager](./Deploying-System-Center-2016---Virtual-Machine-Manager.md).

## <a name="BKMK_security"></a>Configuring security for VMM
You can perform the following tasks to configure security in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

|Task|Description|For more information|
|--------|---------------|------------------------|
|Configure Run As accounts|Create Run As accounts to provide the necessary credentials for performing operations in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].|[Configuring Run As accounts in VMM](./Configuring-Run-As-accounts-in-VMM.md)|
|Create user roles|Create self\-service users, delegated administrators, and read\-only administrators to ensure that users can perform the appropriate actions on the appropriate resources in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].|[Creating user roles in VMM](./Creating-user-roles-in-VMM.md)|
|Review ports and protocols|Review ports and protocols, and as appropriate, modify ports that [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] uses for communication and file transfers between the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] components.|[Ports and protocols for VMM](./Ports-and-protocols-for-VMM.md)|

## <a name="BKMK_fabric"></a>Configuring fabric resources in VMM
The following resources in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] are referred to as ‘*fabric*’, and you must configure them before you can deploy virtual machines and services to a private cloud or to virtual machine hosts. You can use [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] to configure and manage the following fabric resources.

|Resource|Description|For more information|
|------------|---------------|------------------------|
|Virtual machine hosts|Hosts and host clusters on which you will deploy virtual machines and services. These can be running Microsoft Hyper\-V Server, Hyper\-V in Windows Server, or VMware ESX.<br /><br />You can create host groups to organize your hosts based on physical site location, resource allocation, or other criteria.|[Managing Hyper-V hosts and host clusters with VMM](./Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)<br /><br />[VMM support for VMware](./VMM-support-for-VMware.md)<br /><br />[Overview: using host groups in VMM](./Overview--using-host-groups-in-VMM.md)|
|Networking|Networking resources, such as logical networks, IP address pools, and load balancers that are used to deploy virtual machines and services.|[Configuring Networking in VMM](./Configuring-Networking-in-VMM.md)|
|Storage|Storage resources, such as storage classifications, logical units, and storage pools that are made available to Hyper\-V hosts and host clusters.|[Configuring Storage in VMM](./Configuring-Storage-in-VMM.md)|
|Library servers and library shares|A catalog of resources \(for example, virtual hard disks, templates, and profiles\) that are used to deploy virtual machines and services.|[Configuring the VMM library](./Configuring-the-VMM-library.md)|

## <a name="BKMK_vms"></a>Deploying virtual machines and services in VMM
After you configure your hosts and your networking, storage, and library resources, you can perform the following tasks to deploy virtual machines and services in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity. An example is the deployment of a multiple\-tier line\-of\-business application.

|Task|Description|For more information|
|--------|---------------|------------------------|
|Create private clouds|Combine hosts and networking, storage, and library resources to create a private cloud.|[Overview: creating a private cloud with VMM](./Overview--creating-a-private-cloud-with-VMM.md)|
|Configure self\-service|Create a self\-service user role that can create, deploy, and use virtual machines and services in one or more private clouds.|[Managing a self-service environment for tenants](./Managing-a-self-service-environment-for-tenants.md)|
|Create profiles|Create profiles \(hardware profiles, guest operating system profiles, application profiles, and SQL Server profiles\) that will be used in a template to deploy virtual machines.<br /><br />For example, an application profile provides instructions for installing applications such as Web Deploy applications and SQL Server data\-tier applications \(DACs\), and for running scripts during the deployment of a virtual machine.<br /><br />You can use hardware profiles and guest operating system profiles when you deploy virtual machines through a virtual machine template or a service template. You can use application profiles and SQL Server profiles only when you deploy virtual machines through a service template.|[Creating profiles and templates in VMM](./Creating-profiles-and-templates-in-VMM.md)|
|Create virtual machine templates|Create virtual machine templates that can be used to create new virtual machines and to configure tiers in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] services.|[How to create a virtual machine template](./How-to-create-a-virtual-machine-template.md)|
|Create service templates|Use the Service Template Designer to create service templates that can be used to deploy services.|[Creating service templates in VMM](./Creating-service-templates-in-VMM.md)|
|Deploy virtual machines|Deploy virtual machines to private clouds or hosts by using virtual machine templates.|[Creating and deploying virtual machines in VMM](./Creating-and-deploying-virtual-machines-in-VMM.md)|
|Deploy services|Deploy services to private clouds or hosts by using a service template.|[Managing services with VMM](./Managing-services-with-VMM.md)|
|Scale out a service|Add more virtual machines to a deployed service.|[Scaling out services in VMM](./Scaling-out-services-in-VMM.md)|
|Update a service|Make changes to a deployed service.|[Updating services in VMM](./Updating-services-in-VMM.md)|
|Support tenants by using [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] with Windows Azure Pack|Use [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] with Windows Azure Pack to enable tenants to deploy preconfigured virtual machines.|[Creating Virtual Machine Role Templates by using VMM and Windows Azure Pack](./Creating-Virtual-Machine-Role-Templates-by-using-VMM-and-Windows-Azure-Pack.md)|

## <a name="BKMK_scalability"></a>Scalability
The different elements in a [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] deployment can scale as described in the following table.

|[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] element|Scalability in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]|
|-------------------------------------------------------------|----------------------------------------------------------------------------|
|Virtual machine hosts|1,000|
|Virtual machines|25,000|
|User roles|1,000|
|Tenants \(based on one user role per tenant accessing the system\)|1,000|
|Concurrent jobs|250|
|Concurrent clients<br /><br />\(such as VMM consoles and Windows PowerShell sessions\)|50|
|Job history records|5 Million|
|Tenants|1,000|

## <a name="BKMK_managing"></a>Managing the VMM environment
You can perform the following tasks to manage the servers, virtual machines, and services in your [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] environment.

|Task|Description|For more information|
|--------|---------------|------------------------|
|Manage update compliance of servers \(for example, Hyper\-V hosts and library servers\)|Scan servers \(for example, Hyper\-V hosts and library servers\) for update compliance, view update compliance status, and perform update remediation by using a Windows Server Update Services \(WSUS\) server.|[Managing fabric updates in VMM](./Managing-fabric-updates-in-VMM.md)|
|Monitor the health and performance of virtual machines and their hosts and provide reports|Use [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] with [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] and enable Performance and Resource Optimization \(PRO\).|[Integrating VMM and System Center Operations Manager](./Integrating-VMM-and-System-Center-Operations-Manager.md)|
|Perform common maintenance tasks such as backing up the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] database|Perform common maintenance tasks, such as using maintenance mode to prepare to take a host offline, or backing up and restoring the SQL Server database that [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] uses.|[Performing maintenance tasks in VMM](./Performing-maintenance-tasks-in-VMM.md)|


