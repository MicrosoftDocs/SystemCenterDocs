---
title: Post-Installation Tasks for Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f61c476-ccfd-4067-a3ef-3b8fd525b030
---
# Post-Installation Tasks for Service Provider Foundation
After installing, review [Manage Web Services and Connections in Service Provider Foundation](../Topic/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md) for important information about web services, credentials, and connections for using [!INCLUDE[spflong](../Token/spflong_md.md)].

As the administrator for a hosting provider, there are a few key tasks that you need to perform after you install [!INCLUDE[spflong](../Token/spflong_md.md)]. You need to populate the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database sufficiently to start managing tenants. There are three ways to get started:

-   Portal applications

    If you installed [!INCLUDE[spfshort](../Token/spfshort_md.md)] to use with [!INCLUDE[katal_1](../Token/katal_1_md.md)], you can register the [!INCLUDE[spfshort](../Token/spfshort_md.md)] web service endpoint and start provisioning virtual machine clouds and create plans for tenants. For more information, see [Register the Service Provider Foundation Endpoint for Virtual Machine Clouds](assetId:///197ac7a4-6ca2-46a4-855d-327979b68ea5).

    If you installed [!INCLUDE[spfshort](../Token/spfshort_md.md)] to use with [!INCLUDE[conceroshort](../Token/conceroshort_md.md)], you can connect to hosting provider. For more information, see [How to Connect to a Hosting Provider in System Center 2012 SP1](assetId:///5f2729ef-9647-4f5f-bb39-27ea8fc3f0e6).

    For detailed information about using portals, see [Portals in Service Provider Foundation](../Topic/Portals-in-Service-Provider-Foundation.md).

-   [!INCLUDE[spfshort](../Token/spfshort_md.md)] Cmdlets

    These Windows PowerShell cmdlets are suited for performing administrative tasks efficiently. For more information see [Service Provider Foundation cmdlet Reference](http://technet.microsoft.com/library/jj612525(v=sc.20).aspx). For the most current help in the console, run the following command.

    ```powershell
    PS C:\> update-help –module spfadmin
    ```

-   Program applications that consume [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services

    See the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).

## Populating the database

> [!NOTE]
> If you installed [!INCLUDE[spfshort](../Token/spfshort_md.md)] to use with [!INCLUDE[katal_1](../Token/katal_1_md.md)], all virtual machines and clouds defined in [!INCLUDE[vmmblue_1](../Token/vmmblue_1_md.md)] will automatically appear on the **VM Clouds** tab on the [!INCLUDE[katal_adminportal_1](../Token/katal_adminportal_1_md.md)]. There is no need to use Windows PowerShell to define them.

A basic, general procedure for populating the SCSPF database using cmdlets is as follows:

```powershell
PS C:\> # Create a server.
PS C:\> $server = New-SCSPFServer -Name "server23G.contoso.com" -ServerType VMM
PS C:\> # Create a stamp. A stamp is a logical container for a tenant's association with one or more servers.
PS C:\> $stamp = New-SCSPFStamp –Name "StampA" –Servers $server
PS C:\> # Create a tenant. A tenant is your paying customer or business unit.
PS C:\> $tenant = New-SCSPFTenant -Name "jonathan@treyresearch.net"
PS C:\> # Associate the stamp to the tenant. You can set the stamp to the tenant and also to a different server if needed.
PS C:\> Set-SCSPFStamp -Stamp $stamp -Tenants $tenant
```

## See Also
[Deploying Service Provider Foundation](../Topic/Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](../Topic/Architecture-Overview-of-Service-Provider-Foundation.md)
[Integrating Service Management Portal and API with System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=298454)

