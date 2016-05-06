---
title: Release Notes for Service Provider Foundation for System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c47ba2f1-426a-4e35-bc1a-48682eb35ae5
---
# Release Notes for Service Provider Foundation for System Center 2012 R2
These release notes apply to [!INCLUDE[spflong](./Token/spflong_md.md)], a component of [!INCLUDE[orchlong](./Token/orchlong_md.md)]. They contain up\-to\-date information about known issues that you might experience.

For release notes that pertain to the [!INCLUDE[spfshort](./Token/spfshort_md.md)] software development guide, see the [Release Notes for Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263702).

## Known Issues

## Installations with VMM 2012 SP1 causes problems
**Description:** Although you can complete the installation of [!INCLUDE[spfshort](./Token/spfshort_md.md)] 2012 R2 on a server with [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] 2012 SP1, they will not function together correctly.

**Workaround:** None. You must uninstall [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] 2012 SP1, then install VMM 2012 R2, and then install [!INCLUDE[spfshort](./Token/spfshort_md.md)] 2012 R2.

## SPF server names must be in FQDN format
**Description:** Specifying a NetBIOS name for a Service Provider Foundation \(SPF\) server will not work. Instead, SPF names must be in fully qualified domain name \(FQDN\) format. SPF is a feature in Orchestrator.

**Workaround:** Use FQDN format to name SPF servers.

## Updating SPF Run As Account Values Individually Will Fail
**Description:** Updating Domain, User Name, or Password values individually for a Service Provider Foundation \(SPF\) Run As account will fail. SPF is a feature in Orchestrator.

**Workaround:** When updating a Run As account with a new Domain, User Name or Password, all values must be entered at the same time.

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

## Passwords with double quotes in a silent installation
**Description:** If you perform a silent installation of [!INCLUDE[spfshort](./Token/spfshort_md.md)] using passwords that contain double quotes that are not correctly escaped, they can cause the application pools credentials to use the Network Service instead of the expected Service Account.

**Workaround:** In Internet Information Services \(IIS\), verify the application pool identity credential is set correctly for each of the [!INCLUDE[spfshort](./Token/spfshort_md.md)] web services. For more information about silent installs, see [Setup Command-Line Options for Service Provider Foundation](./Setup-Command-Line-Options-for-Service-Provider-Foundation.md).

## See Also
[Deploying Service Provider Foundation](./Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](./Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](./Architecture-Overview-of-Service-Provider-Foundation.md)


