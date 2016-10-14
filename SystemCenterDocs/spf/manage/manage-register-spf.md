---
title: Register the SPF endpoint in Windows Azure Pack
description: Provides information about registering the SPF endpoint in Windows Azure Pack
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/14/2016
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
ms.assetid: 38695129-ee8d-49ee-a357-b00a7659ba31
---

# Register the SPF endpoint in Windows Azure Pack
>Apples To: System Center 2016

For System Center 2016 - Service Provider Foundation (SPF) to provide services and connectivity for delivering IaaS in Windows Azure Pack,  you need to register it.

1. On the SPF server, note the credentials used for the Admin, VMM, Usage, and Provider Application Pool identity in IIS.
2. [Register the SPF endpoint with the Azure Pack management portal](https://technet.microsoft.com/library/dn457792.aspx). After it's registered you can enable the VM Clouds service from the portal.






Continue with the procedure in Register the Service Provider Foundation Endpoint for Virtual Machine Clouds in the Windows Azure Pack for Windows Server documentation.




The Service Provider Foundation setup wizard configures web services based on the provided credentials. This topic provides information about verifying and setting credentials in Computer Management, Internet Information Services \(IIS\), and other technologies if changes are required.

Note that the example URLs in this topic use port 8090, the default port, for Service Provider Foundation web services. This port may be different if another port was specified for the Service Provider Foundation installation.

## Service Provider Foundation web services
As a hosting service provider you can use Service Provider Foundation web services to provide portal applications to your tenants. Administrators can use the Service Provider Foundation Windows PowerShell cmdlets to perform essential tasks. For information about how to program applications that access the Service Provider Foundation web services, see the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).

Each web service has two locations to set credentials on the server that has Service Provider Foundation installed: the application domain pool in IIS and the respective group in Computer Management. These groups \(SPF\_Admin, SPF\_VMM, SPF\_Usage, and SPF\_Provider\) must contain a local credential \(not a domain credential\) that is also a member of the Administrators group. That credential can be the Administrator user itself, but we recommend creating another local user.

### <a name="SPF_Admin"></a>Admin web service
Hosting service providers use the Admin web service to create and manage tenants, user roles, servers, stamps, and other administrative objects. You can access the Admin web service by using the URL `https://server:8090/SC2016/Admin/Microsoft.Management.Odata.svc`

|Credential setting|Requirement|
|----------------------|---------------|
|Admin application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Admin group|
|Administrators group in Computer Management|Must include the credential for the Admin application pool identity|
|SPF\_Admin group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Admin application pool identity|

### <a name="SPF_VMM"></a>VMM web service
The VMM web service invokes Virtual Machine Manager  to perform requested operations, such as creating virtual machines, virtual networks, user role definitions, and other fabric for the cloud. This service coordinates the changes among the participants and provides the following dynamic capabilities:

-   Portal applications and other clients detect changes that Service Provider Foundation and System Center 2016 Virtual Machine Manager made.

-   System Center 2016 Virtual Machine Manager shows changes that portal applications, other clients, and Service Provider Foundation made.

-   Service Provider Foundation reflects all changes that the participants made.

You can use the T:Microsoft.SystemCenter.Foundation.Cmdlet.New-SCSPFServer PowerShell cmdlet to register an instance of System Center 2016 Virtual Machine Manager.

You can access the VMM web service by using the URL  `https://server:8090/SC2016/VMM/Microsoft.Management.Odata.svc`



|Credential setting|Requirement|
|----------------------|---------------|
|VMM application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_VMM group|
|Administrators group in Computer Management|Must include the credential for the VMM application pool identity|
|SPF\_VMM group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the VMM application pool identity|
|Administrator user role in System Center 2016 Virtual Machine Manager|Must include the credential for the VMM application pool identity as a member of the Administrator user role|

### <a name="SPF_Usage"></a>Usage web service

> [IMPORTANT]
> Service Provider Foundation provides the Usage web service to be used only by Windows Azure Pack for Windows Server or by third party billing providers. The Usage web service endpoint should not be accessed for other purposes to prevent data loss due to unnecessary or erroneous queries.

The Usage web service uses registrations of instances of System Center 2016 Operations Manager  data warehouses \(that System Center 2016 Virtual Machine Manager hosts\) for collecting metrics on tenant virtual machine usage and other fabric usage. Usage data is collected for processes such as billing chargeback features.

You can use Windows PowerShell cmdlets to register System Center 2016 Operations Manager data warehouse connection settings in the Service Provider Foundation database. This registration enables Service Provider Foundation to aggregate usage data from the data warehouses. For more information about configuring these registrations, see [Configure Usage Metering in Service Provider Foundation](../manage/Configure-Usage-Metering.md).

The Usage web service returns utilization data that pertains to every subscription across services.

|Credential setting|Requirement|
|----------------------|---------------|
|Usage application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Usage group.|
|Administrators group in Computer Management|Must include the credential for the Usage application pool identity.|
|SPF\_Usage group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Usage application pool identity.|
|Database user dbo in the OpertionsManagerDW Microsoft SQL Server database on the server that is running System Center 2016 Operations Manager |The credentials of the user who installs System Center 2016 Operations Manager  are automatically used for the login credentials for the dbo SQL Server security object. These same credentials should be used for all Service Provider Foundation application pool identities.|
|Database properties for the OpertionsManagerDW SQL Server database \(right\-click\) on the server that is running System Center 2016 Operations Manager |The OpsMgrReader database role must be included on the **Permissions** page.|

### <a name="SPF_Provider"></a>Provider web service
Resource providers for delivering infrastructure as a service \(IaaS\) use the Provider web service. The Provider web service provides a Microsoft ASP.NET web API. It is not an Open Data \(OData\) service. The Provider web service also uses the VMM and Admin web services.

|Credential setting|Requirement|
|----------------------|---------------|
|Provider application pool identity in IIS|Must also be a member of the Administrators group and the SPF\_Provider, SPF\_VMM, and SPF\_Admin groups|
|Administrators group in Computer Management|Must include the credential for the Provider application pool identity|
|SPF\_Provider group in Computer Management|Must include a local user who is also a member of the Administrators group and the credential for the Provider application pool identity|

## <a name="SPF_SMA"></a>Connecting to the Service Management Automation web service
You can configure events in Service Provider Foundation that the Service Management Automation web service will use. For you to complete this configuration, the Service Management Automation web service must have credentials to access the required Service Provider Foundation web services.

In addition, you can use Windows PowerShell cmdlets to automate runbooks. For more information, see [How to Automate a Runbook from Service Provider Foundation](../Manage/How-to-Automate-a-Runbook.md).

|Credential setting|Requirement|
|----------------------|---------------|
|One or all of the Service Provider Foundation application pool identities as required for automation|Must also be a member of the Administrators group for the server that has Service Management Automation installed|

### Service Provider Foundation database credentials
The credentials of the user who installs Service Provider Foundation are used for the login credentials for the dbo SQL Server security object for the Service Provider Foundation database. Use the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFConnectionString and T:Microsoft.SystemCenter.Foundation.Cmdlet.Set\-SCSPFConnectionString cmdlets to manage the connections to the Service Provider Foundation database.

### Next steps

The following topics provide how to instructions for using SPF.

- [Configure usage metering](/manage/Configure-Usage-Metering.md)
- [How to automate a runbook](/manage/How-to-Automate-a-Runbook.md)
- [How to configure the System Center resource provider for Windows Azure Pack](/manage/how-to-configure-the-system-center-resource-provider-for-windows-azure-pack.md)
- [How to create and SSL certificate](/manage/how-to-create-an-ssl-certificate.md)
- [Importing gallery items](/manage/importing-gallery-items.md)
- [Parameters for runbooks](/manage/parameters-for-runbooks.md)
- [Walkthrough: Creating a certificate and user roles](/manage/walkthrough-creating-a-certificate-and-user-roles.md)
