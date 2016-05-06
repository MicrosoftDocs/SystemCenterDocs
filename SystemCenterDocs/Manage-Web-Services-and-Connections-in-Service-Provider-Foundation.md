---
title: Manage Web Services and Connections in Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 975d9b1d-d2d5-404c-8e54-961d64ad2ab4
---
# Manage Web Services and Connections in Service Provider Foundation
The [!INCLUDE[spflong](../Token/spflong_md.md)] setup wizard configures web services based on the provided credentials. This topic provides information about verifying and setting credentials in Computer Management, Internet Information Services \(IIS\), and other technologies if changes are required.

Note that the example URLs in this topic use port 8090, the default port, for [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services. This port may be different if another port was specified for the [!INCLUDE[spfshort](../Token/spfshort_md.md)] installation.

## [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services
As a hosting service provider you can use [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services to provide portal applications to your tenants. Administrators can use the [!INCLUDE[spfshort](../Token/spfshort_md.md)]Windows PowerShell cmdlets to perform essential tasks. For information about how to program applications that access the [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services, see the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).

Each web service has two locations to set credentials on the server that has [!INCLUDE[spfshort](../Token/spfshort_md.md)] installed: the application domain pool in IIS and the respective group in Computer Management. These groups \(SPF\_Admin, SPF\_VMM, SPF\_Usage, and SPF\_Provider\) must contain a local credential \(not a domain credential\) that is also a member of the Administrators group. That credential can be the Administrator user itself, but we recommend creating another local user.

### <a name="SPF_Admin"></a>Admin web service
Hosting service providers use the Admin web service to create and manage tenants, user roles, servers, stamps, and other administrative objects. You can access the Admin web service by using the following URLs:

-   For [!INCLUDE[spfshort](../Token/spfshort_md.md)][!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)], use:

    `http://server:8090/SC2012/Admin/Microsoft.Management.Odata.svc`

-   For [!INCLUDE[spfshort](../Token/spfshort_md.md)][!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], use:

    `https://server:8090/SC2012R2/Admin/Microsoft.Management.Odata.svc`

|Credential setting|Requirement|
|----------------------|---------------|
|Admin application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Admin group|
|Administrators group in Computer Management|Must include the credential for the Admin application pool identity|
|SPF\_Admin group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Admin application pool identity|

### <a name="SPF_VMM"></a>VMM web service
The VMM web service invokes [!INCLUDE[vmmblue_1](../Token/vmmblue_1_md.md)] to perform requested operations, such as creating virtual machines, virtual networks, user role definitions, and other fabric for the cloud. This service coordinates the changes among the participants and provides the following dynamic capabilities:

-   Portal applications and other clients detect changes that [!INCLUDE[spfshort](../Token/spfshort_md.md)] and [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)] made.

-   [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)] shows changes that portal applications, other clients, and [!INCLUDE[spfshort](../Token/spfshort_md.md)] made.

-   [!INCLUDE[spfshort](../Token/spfshort_md.md)] reflects all changes that the participants made.

You can use the [T:Microsoft.SystemCenter.Foundation.Cmdlet.New-SCSPFServer](assetId:///T:Microsoft.SystemCenter.Foundation.Cmdlet.New-SCSPFServer) PowerShell cmdlet to register an instance of [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)].

You can access the VMM web service by using the following URLs:

-   For [!INCLUDE[spfshort](../Token/spfshort_md.md)][!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)], use:

    `http://server:8090/SC2012/VMM/Microsoft.Management.Odata.svc`

-   For [!INCLUDE[spfshort](../Token/spfshort_md.md)][!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], use:

    `https://server:8090/SC2012R2/VMM/Microsoft.Management.Odata.svc`

|Credential setting|Requirement|
|----------------------|---------------|
|VMM application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_VMM group|
|Administrators group in Computer Management|Must include the credential for the VMM application pool identity|
|SPF\_VMM group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the VMM application pool identity|
|Administrator user role in [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)]|Must include the credential for the VMM application pool identity as a member of the Administrator user role|

### <a name="SPF_Usage"></a>Usage web service

> [!IMPORTANT]
> [!INCLUDE[spfshort](../Token/spfshort_md.md)] provides the Usage web service to be used only by [!INCLUDE[katal_1](../Token/katal_1_md.md)] or by third party billing providers. The Usage web service endpoint should not be accessed for other purposes to prevent data loss due to unnecessary or erroneous queries.

The Usage web service uses registrations of instances of [!INCLUDE[om12long](../Token/om12long_md.md)] data warehouses \(that [!INCLUDE[vmmblue_2](../Token/vmmblue_2_md.md)] hosts\) for collecting metrics on tenant virtual machine usage and other fabric usage. Usage data is collected for processes such as billing chargeback features.

You can use Windows PowerShell cmdlets to register [!INCLUDE[om12short](../Token/om12short_md.md)] data warehouse connection settings in the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database. This registration enables [!INCLUDE[spfshort](../Token/spfshort_md.md)] to aggregate usage data from the data warehouses. For more information about configuring these registrations, see [Configure Usage Metering in Service Provider Foundation](../Topic/Configure-Usage-Metering-in-Service-Provider-Foundation.md).

The Usage web service returns utilization data that pertains to every subscription across services.

|Credential setting|Requirement|
|----------------------|---------------|
|Usage application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Usage group.|
|Administrators group in Computer Management|Must include the credential for the Usage application pool identity.|
|SPF\_Usage group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Usage application pool identity.|
|Database user dbo in the OpertionsManagerDW Microsoft SQL Server database on the server that is running [!INCLUDE[om12short](../Token/om12short_md.md)]|The credentials of the user who installs [!INCLUDE[om12short](../Token/om12short_md.md)] are automatically used for the login credentials for the dbo SQL Server security object. These same credentials should be used for all [!INCLUDE[spfshort](../Token/spfshort_md.md)] application pool identities.|
|Database properties for the OpertionsManagerDW SQL Server database \(right\-click\) on the server that is running [!INCLUDE[om12short](../Token/om12short_md.md)]|The OpsMgrReader database role must be included on the **Permissions** page.|

### <a name="SPF_Provider"></a>Provider web service
Resource providers for delivering infrastructure as a service \(IaaS\) use the Provider web service. The Provider web service provides a Microsoft ASP.NET web API. It is not an Open Data \(OData\) service. The Provider web service also uses the VMM and Admin web services.

|Credential setting|Requirement|
|----------------------|---------------|
|Provider application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Provider, SPF\_VMM, and SPF\_Admin groups|
|Administrators group in Computer Management|Must include the credential for the Provider application pool identity|
|SPF\_Provider group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Provider application pool identity|

## <a name="SPF_SMA"></a>Connecting to the Service Management Automation web service
You can configure events in [!INCLUDE[spfshort](../Token/spfshort_md.md)] that the [Service Management Automation](../Topic/Service-Management-Automation.md) web service will use. For you to complete this configuration, the [!INCLUDE[sma_1](../Token/sma_1_md.md)] web service must have credentials to access the required [!INCLUDE[spfshort](../Token/spfshort_md.md)] web services.

In addition, you can use Windows PowerShell cmdlets to automate runbooks. For more information, see [How to Automate a Runbook from Service Provider Foundation](../Topic/How-to-Automate-a-Runbook-from-Service-Provider-Foundation.md).

|Credential setting|Requirement|
|----------------------|---------------|
|One or all of the [!INCLUDE[spfshort](../Token/spfshort_md.md)] application pool identities as required for automation|Must also be a member of the Administrators group for the server that has [!INCLUDE[sma_1](../Token/sma_1_md.md)] installed|

## [!INCLUDE[spfshort](../Token/spfshort_md.md)] database credentials
The credentials of the user who installs [!INCLUDE[spfshort](../Token/spfshort_md.md)] are used for the login credentials for the dbo SQL Server security object for the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database. Use the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFConnectionString and T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFConnectionString cmdlets to manage the connections to the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database.

## See Also
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)

