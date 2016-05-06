---
title: Release Notes for Service Provider Foundation for System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf74c3db-6bc0-4e68-b690-85867d9c5fdb
---
# Release Notes for Service Provider Foundation for System Center 2012 SP1
These release notes apply to [!INCLUDE[spflong](./Token/spflong_md.md)], a component of [!INCLUDE[orchlong](./Token/orchlong_md.md)]. They contain up\-to\-date information about known issues that you might experience.

## Known Issues

## Installation fails on a computer with only IPv6 enabled
**Description:** Installation of [!INCLUDE[spfshort](./Token/spfshort_md.md)] fails on a computer that has only IPv6 enabled for the network adapters.

**Workaround:** Enable IPv4.

## You cannot move a virtual machine across clouds
**Description:**[!INCLUDE[spfshort](./Token/spfshort_md.md)] cannot accommodate moving a virtual machine from one cloud to another.

**Workaround:** None. This is a known limitation.

## A new virtual machine is unusable if it is created without a guest operating system
**Description:** You can create a new virtual machine from a template by using a blank virtual hard disk \(VHD\). However, a 13206 error appears in the summary page. The virtual machine will be unusable if it is created with a VHD that contains no guest operating system.

**Workaround:** Create the virtual machine with a guest operating system.

## Creating a virtual disk drive from a large VHD results in timeout exceptions
**Description:** Sporadic timeout exceptions might occur when you are creating a virtual disk drive with a large VHD.

**Workaround:** Retry the operation.

## Creation of a user role fails occasionally
**Description:** In attempting to create a new user role on a second [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] server, the administrator user role might be unable to create a new user role, because the attempt is treated as an accidental impersonation.

**Workaround:** Recycle the VMM application pool.

## An endpoint was registered successfully, but it cannot be registered as a Virtual Machine Cloud Provider
**Description:**[!INCLUDE[spfshort](./Token/spfshort_md.md)] has been successfully installed, the endpoint can be accessed, but the service will not register as a Virtual Machine Cloud Provider.

**Workaround:** Copy the required files to the [!INCLUDE[spfshort](./Token/spfshort_md.md)] endpoint website.

## Updating a tenant to a new issuer and key does not work
**Description:** If you create a tenant with a specified key and issuer name and then update that same tenant \(such as by using the T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFTenant cmdlet\) to a new key and issuer name, the new key for the tenant will not be updated in the database.

**Workaround:** Recreate the tenant as shown in the following example.

```
PS C:\> $tenant = Get-SCSPFTenant -Name "TenantToFix"
PS C:\> $issuerName = (Get-SCSPFTrustedIssuer -Tenant $tenant).Name
PS C:\> $stamps = Get-SCSPFStamp -Tenant $tenant
PS C:\> $userroles = Get-SCSPFTenantUserRole -Tenant $tenant | Select-Object Name
PS C:\> Remove-SCSPFTenant -Tenant $tenant
PS C:\> $tenant2 = New-SCSPFTenant -Name "FixedTenant" -IssuerName $issuerName -Key $key2 -Stamps $stamps
PS C:\> $userroles | foreach {New-SCSPFTenantUserRole -Tenant $tenant2 -Name $_.Name}

```

## See Also
[Deploying Service Provider Foundation](./Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](./Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](./Architecture-Overview-of-Service-Provider-Foundation.md)


