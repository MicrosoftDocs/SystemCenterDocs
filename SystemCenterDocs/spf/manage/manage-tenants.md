---
ms.assetid: 8a6608c6-5189-4e4a-a9bf-c44b3b13aa38
title: Manage tenants and user roles in SPF
description: Provides information setting up SPF tenants, and creating self-service tenant roles in VMk
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/16/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
---

#  Manage tenants and user roles in SPF
>Apples To: System Center 2016

For System Center 2016 - Service Provider Foundation (SPF) doesn't create user roles, or define their scope. To set up tenants you need a certificate public key that's used to validate claims made (or on behalf of) a tenant.

## Create a certificate

If you don't have an existing CA certificate to use, you can generate a self-signed certificate. You can to export public and private keys from the certificate, and associate the public key with a tenant.

## Obtain a self-signed certificate

Create a certificate using [makecert.exe (Certificate Creation Tool)](http://technet.microsoft.com/library/bfsktky3).  

1.  Open a command prompt as administrator.  
2.  Generate the certificate by running the following command:  

    ```  
    makecert -r -pe -n "cn=contoso.com" -b 07/12/2012 -e 09/23/2014 -ss My -sr CurrentUser -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 -sky exchange  
    ```  

3. This command puts the certificate in the Current User Certificate Store. To access it, on **Start** screen, type **certmgr.msc** and then in the **Apps** results click **certmgr.msc**.   In the **certmgr** window, click **Certificates \- Current User** > **Personal** > **Certificates** folder.  

### Export the public key

1. Right\-click the certificate > **All Tasks** >  **Export**.  
2. In **Export Private Key**, choose **No, do not export the private key** > **Next**.  
3. In **Export File Format**, select **Base\-64 encoded X.509 \(.CER\)** > **Next**.  
4. In **File to Export**, specify a path and filename for the certificate > **Next**.  
5. In **Completing the Certificate Export Wizard**, click **Finish**.  

To export using Power Shell, run:
``S C:\> $path = "C:\Temp\tenant4D.cer"  

PS C:\> $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($path)  

PS C:\> $key = [Convert]::ToBase64String($cert.RawData)``


### Export the private key

1. Right\-click the certificate > **All Tasks** >  **Export**.  
2. In **Export Private Key**, choose **Yes, export the private key** > **Next**.If this option isn't available and you generated a self-signed certificate, ensure it included the -pe option.
3. In **Export File Format**, select **Personal Information Exchange - PKCS #12 (.PFX)**. Make sure  **Include all certificates in the certification path if possible** is selected, and click **Next**.  
4. In **File to Export**, specify a path and filename for the certificate > **Next**.  
5. In **Completing the Certificate Export Wizard**, click **Finish**.  

## Create the tenant

Service Provider Foundation does not create user roles or define their scope (such as clouds), resources, or actions. Instead, the New-SCSPFTenantUserRole cmdlet creates an association for a tenant with a user role name. When that association is created, it also generates an ID that can be used for the corresponding ID for creating the role in System Center 2016 - Virtual Machine Manager.

You can also create user roles by using the Admin OData protocol service using the [Developer's Guide](https://msdn.microsoft.com/library/jj643273.aspx).

1.  Run the SPF command shell as an Administrator.  
2.  Type following command to create the tenant. This command assumes that the `$key` variable contains the public key.  

    ```  
    PS C:\> $tenant = New-SCSPFTenant -Name "contoso.cloudspace.com" -IssuerName "contoso.cloudspace.com" -Key $key  
    ```  

3.  Run this command to verify that the public key for the tenant was imported successfully:  

    ```  
    PS C:\> Get-SCSPFTrustedIssuer  
    ```  

    The next procedure uses the `$tenant` variable that you just created.  

### Create a tenant administrator role in VMM  

1.  Enter the following command and agree to this elevation for the Windows PowerShell command shell:  

    ```  
    PS C:\> Set-Executionpolicy remotesigned  
    ```  

2.  Enter the following command to import the VMM module:  

    ```  
    PS C:\> Import-Module virtualmachinemanager  
    ```  

3.  Use the Windows PowerShell T:Microsoft.SystemCenter.VirtualMachineManager.Cmdlets.New\-SCUserRole cmdlet to create the user role. This command assumes the `$tenant` variable was created as described in the [To create a tenant with the certificate's public key](#BMK_CreateTenant) procedure.  

    ```  
    PS C:\> $TARole = New-SCUserRole -Name contoso.cloudspace.com -ID $tenant.Id -UserRoleProfile TenantAdmin  

    ```  

    > [CAUTION]  
    > Note that if the user role was previously created by using the VMM Administration Console, its permissions would be overwritten by those specified by the **New\-SCSUserRole** cmdlet.  

4.  Verify that the user role was created by verifying that it is listed in the **User Roles** in **Settings** workspace in the VMM Administration Console.  

5.  Define the following for the role by selecting the role and clicking **Properties** on the toolbar:  

    -   On the **Scope** tab, select one or more clouds.  

    -   On the **Resources** tab, add any resources such as templates.  

    -   On the **Actions** tab, select one or more actions.  

    Repeat this procedure for every server assigned to the tenant.  

    The next procedure uses the `$TARole` variable that you just created.  

## Create a tenant self-service user role in VMM

1.  Enter the following command to create a self\-service user in SPF for the tenant you created.  

    ```  
    PS C:\> $TenantSSU = New-SCSPFTenantUserRole -Name ContosoCloudSpaceSSU -Tenant $tenant   
    ```  

2.  Create the corresponding tenant user role in VMM by entering the following command:  

    ```  
    PS C:\> $vmmSSU = New-SCUserRole -Name ContosoCloudSpaceVMMSSU -UserRoleProfile SelfServiceUser -ParentUserRole $TARole -ID $TenantSSU.ID  

    ```  

3.  Verify that the user role was created by verifying that it is listed in the **User Roles** in **Settings** workspace in the VMM Administration Console. Notice that the parent of the role is the tenant administrator.  

Repeat this procedure as needed for each tenant.
