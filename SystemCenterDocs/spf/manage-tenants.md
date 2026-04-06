---
title: Manage Tenants and User Roles in SPF
description: Provides information setting up SPF tenants, and creating self-service tenant roles in VMM
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/21/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: service-provider-foundation
ms.custom: UpdateFrequency2, engagement-fy24
ms.update-cycle: 1095-days
---

#  Manage tenants and user roles in SPF

This article provides information setting up SPF tenants, and creating self-service tenant roles in VMM.

System Center - Service Provider Foundation (SPF) doesn't create user roles or define their scope. To set up tenants, you need a certificate public key that's used to validate claims made on behalf of a tenant.

## Create a certificate

If you don't have an existing CA certificate to use, you can generate a self-signed certificate. You can export public and private keys from the certificate and associate the public key with a tenant.

## Obtain a self-signed certificate

To create a certificate using `makecert.exe` (Certificate Creation Tool), follow these steps:

1.  Open a command prompt as administrator.  
2.  Generate the certificate by running the following command:  

    ```  
    makecert -r -pe -n "cn=contoso.com" -b 07/12/2012 -e 09/23/2014 -ss My -sr CurrentUser -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 -sky exchange  
    ```  

3. This command puts the certificate in the Current User Certificate Store. To access it, on the **Start** screen, enter **certmgr.msc** and then in the **Apps** results, select **certmgr.msc**. In the **certmgr** window, select **Certificates \- Current User** > **Personal** > **Certificates** folder.  

### Export the public key

To export the public key, follow these steps:

1. Right-click the certificate > **All Tasks** >  **Export**.  
2. In **Export Private Key**, choose **No, do not export the private key** > **Next**.  
3. In **Export File Format**, select **Base\-64 encoded X.509 \(.CER\)** > **Next**.  
4. In **File to Export**, specify a path and filename for the certificate > **Next**.  
5. In **Completing the Certificate Export Wizard**, select **Finish**.  

To export using PowerShell, run:

```
``S C:\> $path = "C:\Temp\tenant4D.cer"  

PS C:\> $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($path)  

PS C:\> $key = [Convert]::ToBase64String($cert.RawData)``
```

### Export the private key

To export the private key, follow these steps:

1. Right-click the certificate > **All Tasks** >  **Export**.  
2. In **Export Private Key**, choose **Yes, export the private key** > **Next**. If this option isn't available and you generated a self-signed certificate, ensure it included the -pe option.
3. In **Export File Format**, select **Personal Information Exchange - PKCS #12 (.PFX)**. Ensure **Include all certificates in the certification path if possible** is selected and select **Next**.  
4. In **File to Export**, specify a path and filename for the certificate > **Next**.  
5. In **Completing the Certificate Export Wizard**, select **Finish**.  

## Create the tenant

Service Provider Foundation doesn't create user roles or define their scope (such as clouds), resources, or actions. Instead, the `New-SCSPFTenantUserRole` cmdlet creates an association for a tenant with a user role name. When that association is created, it also generates an ID that can be used for the corresponding ID for creating the role in System Center 2016 - Virtual Machine Manager.

You can also create user roles by using the Admin OData protocol service using the [Developer's guide](/previous-versions/system-center/developer/jj643273(v=msdn.10)).

To create a tenant, follow these steps:

1.  Run the SPF command shell as an Administrator.  
2.  Enter the following command to create the tenant. This command assumes that the `$key` variable contains the public key.  

    ```  
    PS C:\> $tenant = New-SCSPFTenant -Name "contoso.cloudspace.com" -IssuerName "contoso.cloudspace.com" -Key $key  
    ```  

3.  Run this command to verify that the public key for the tenant was imported successfully:  

    ```  
    PS C:\> Get-SCSPFTrustedIssuer  
    ```  

    The next procedure uses the `$tenant` variable that you created.  

### Create a tenant administrator role in VMM  

To create a tenant administrator role in VMM, follow these steps:

1.  Enter the following command and agree to this elevation for the Windows PowerShell command shell:  

    ```  
    PS C:\> Set-Executionpolicy remotesigned  
    ```  

2.  Enter the following command to import the VMM module:  

    ```  
    PS C:\> Import-Module virtualmachinemanager  
    ```  

3.  Use the Windows PowerShell `T:Microsoft.SystemCenter.VirtualMachineManager.Cmdlets.New\-SCUserRole` cmdlet to create the user role. This command assumes the `$tenant` variable that was created as described in the procedure above.  

    ```  
    PS C:\> $TARole = New-SCUserRole -Name contoso.cloudspace.com -ID $tenant.Id -UserRoleProfile TenantAdmin  

    ```  

    > [!CAUTION]  
    > Note that if the user role was previously created by using the VMM Administration Console, its permissions would be overwritten by those specified by the `New\-SCSUserRole` cmdlet.  

4.  Verify that the user role was created by verifying that it's listed in the **User Roles** in **Settings** workspace in the VMM Administration Console.  

5.  Define the following for the role by selecting the role and selecting **Properties** on the toolbar:  

    -   On the **Scope**, select one or more clouds.  

    -   On the **Resources**, add any resources such as templates.  

    -   On the **Actions**, select one or more actions.  

    Repeat this procedure for every server assigned to the tenant.  

    The next procedure uses the `$TARole` variable that you created.  

## Create a tenant self-service user role in VMM

To create a tenant self-service user role in VMM, follow these steps:

1.  Enter the following command to create a self\-service user in SPF for the tenant you created:  

    ```  
    PS C:\> $TenantSSU = New-SCSPFTenantUserRole -Name ContosoCloudSpaceSSU -Tenant $tenant   
    ```  

2.  Create the corresponding tenant user role in VMM by entering the following command:  

    ```  
    PS C:\> $vmmSSU = New-SCUserRole -Name ContosoCloudSpaceVMMSSU -UserRoleProfile SelfServiceUser -ParentUserRole $TARole -ID $TenantSSU.ID  

    ```  

3.  Verify that the user role was created by verifying that it's listed in the **User Roles** in **Settings** workspace in the VMM Administration Console. Notice that the parent of the role is the tenant administrator.  

Repeat this procedure as needed for each tenant.
