---
title: Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b546c86-2458-4449-87ee-e48b6be4228a
author:bwren
manager:cfreemanwa
---
# Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation
This walkthrough shows how to administer important tasks for managing both certificates and user roles in [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)]. To start, we show how to generate a self\-signed certificate if you are not already working with an issuer's signed certificate. Next, we show how to obtain the certificate's public key, and how to use that key to create the tenant in [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] and user roles in [!INCLUDE[vmm12long](../../spf/Deploy/includes/vmm12long_md.md)].  
  
This walkthrough is organized into the following sections and procedures. The procedures are designed to be performed sequentially, although they contain the information that you need to run them individually as needed. These procedures are tasks for  the hoster administrator to perform.  
  
|Section|Procedures|  
|-----------|--------------|  
|[Create a certificate](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_Cert)|[To create a self-signed certificate for a tenant](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateCert)|  
|[Obtain and export keys](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_Keys)|[To export the public key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_ExportPublic)<br />[To export the private key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_ExportPrivate)<br />[To obtain the public key in Windows PowerShell](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_ObtainKey)|  
|[Create the tenant and its user roles](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_Role)|[To create a tenant with the certificate's public key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateTenant)<br />[To create a tenant administrator role in VMM](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateTARole)<br />[To create a tenant self-service user role](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateSSU)|  
  
## <a name="BMK_Cert"></a>Create a certificate  
The following procedure describes how to create a certificate for a tenant by using [makecert.exe \(Certificate Creation Tool\)](assetId:///b0343f8e-9c41-4852-a85c-f8a0c408cf0d).  
  
### <a name="BMK_CreateCert"></a>To create a self\-signed certificate for a tenant  
  
1.  Open a command prompt as administrator.  
  
2.  Generate the certificate by running the following command:  
  
    ```  
    makecert -r -pe -n "cn=contoso.com" -b 07/12/2012 -e 09/23/2014 -ss My -sr CurrentUser -sp "Microsoft RSA SChannel Cryptographic Provider" -sy 12 -sky exchange  
    ```  
  
    This command puts the certificate in the Current User Certificate Store.  
  
### <a name="BMK_AccessCert"></a>To access the certificate that you created  
  
1.  On the **Start** screen, type **certmgr.msc** and then in the **Apps** results click **certmgr.msc**.  
  
2.  In the **certmgr** window, click **Certificates \- Current User**, open the **Personal** folder, and then open the **Certificates** folder to view the certificate that you just generated.  
  
## <a name="BMK_Keys"></a>Obtain and export keys  
The procedures in this section show how to export public and private keys from certificate files. You associate a public key with a tenant in [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] to later validate claims made, or made on behalf of, a tenant. This section includes a procedure that shows how to obtain the public key directly in your PowerShell session.  
  
### <a name="BMK_ExportPublic"></a>To export the public key  
  
1.  Open your **certificates** folder to view the certificate as described in the [To access the certificate that you created](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_AccessCert) procedure.  
  
2.  Right\-click the certificate, click **All Tasks**, and then click **Export**.  
  
3.  After the Welcome page, on the **Export Private Key** page, choose **No, do not export the private key** and then click **Next**.  
  
4.  On the **Export File Format** page, select **Base\-64 encoded X.509 \(.CER\)** and then click **Next**.  
  
5.  On the **File to Export** page, specify a path and filename for the certificate and then click **Next**.  
  
6.  On the **Completing the Certificate Export Wizard** page, click **Finish**.  
  
### <a name="BMK_ExportPrivate"></a>To export the private key  
  
1.  Open your **certificates** folder to view the certificate as described in the [To access the certificate that you created](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_AccessCert) procedure.  
  
2.  Right\-click the certificate, click **All Tasks**, and then click **Export**.  
  
3.  After the **Welcome** page, on the **Export Private Key** page choose **Yes, export the private key** and then click **Next**.  
  
    If the Yes option is disabled, that is because the **makecert** command to create the certificate did not include the *\-pe* option.  
  
4.  On the **Export File Format** page, select the **Personal Information Exchange - PKCS \#12 \(.PFX\)** option, check the **Include all certificates in the certification path if possible** check box and then click **Next**.  
  
5.  On the **Security** page, select the **Password:** option, provide and confirm a password, and then click **Next**.  
  
6.  On the **File to Export** page, specify a path and filename for the certificate and then click **Next**.  
  
7.  On the **Completing the Certificate Export Wizard** page, click **Finish**.  
  
### <a name="BMK_ObtainKey"></a>To obtain the public key in Windows PowerShell  
  
1.  You can obtain the public key directly from an exported public key certificate file \(.CER\) by using the .NET Framework cryptography classes. Run the following commands to obtain the key from the certificate's public key file that you exported in the [To export the public key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_ExportPublic) procedure.  
  
    ```  
    PS C:\> $path = "C:\Temp\tenant4D.cer"  
  
    PS C:\> $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($path)  
  
    PS C:\> $key = [Convert]::ToBase64String($cert.RawData)  
  
    ```  
  
    The next procedure uses the `$key` variable that you just created.  
  
## <a name="BMK_Role"></a>Create the tenant and its user roles  
[!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] does not create user roles or define their scope \(such as clouds\), resources, or actions. Instead, the New\-SCSPFTenantUserRole cmdlet creates an association for a tenant with a user role name. When that association is created, it also generates an ID that can be used for the corresponding ID for creating the role in [!INCLUDE[vmm12med](../../spf/Deploy/includes/vmm12med_md.md)].  
  
You can also create user roles by using the Admin OData protocol service that uses the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).  
  
### <a name="BMK_CreateTenant"></a>To create a tenant with the certificate's public key  
  
1.  Run the System Center 2012 Service Provider Foundation Command Shell as Administrator.  
  
2.  Enter the following command to create the tenant. This command assumes that the `$key` variable contains the public key as obtained from the [To obtain the public key in Windows PowerShell](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_ObtainKey) procedure.  
  
    ```  
    PS C:\> $tenant = New-SCSPFTenant -Name "contoso.cloudspace.com" -IssuerName "contoso.cloudspace.com" -Key $key  
    ```  
  
3.  Verify that the public key for the tenant was imported successfully by running the following command and viewing the results:  
  
    ```  
    PS C:\> Get-SCSPFTrustedIssuer  
    ```  
  
    The next procedure uses the `$tenant` variable that you just created.  
  
### <a name="BMK_CreateTARole"></a>To create a tenant administrator role in VMM  
  
1.  Enter the following command and agree to this elevation for the Windows PowerShell command shell:  
  
    ```  
    PS C:\> Set-Executionpolicy remotesigned  
    ```  
  
2.  Enter the following command to import the [!INCLUDE[vmm12sp1_med](../../om/manage/includes/vmm12sp1_med_md.md)] module:  
  
    ```  
    PS C:\> Import-Module virtualmachinemanager  
    ```  
  
3.  Use the Windows PowerShell T:Microsoft.SystemCenter.VirtualMachineManager.Cmdlets.New\-SCUserRole cmdlet to create the user role. This command assumes the `$tenant` variable was created as described in the [To create a tenant with the certificate's public key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateTenant) procedure.  
  
    ```  
    PS C:\> $TARole = New-SCUserRole -Name contoso.cloudspace.com -ID $tenant.Id -UserRoleProfile TenantAdmin  
  
    ```  
  
    > [!CAUTION]  
    > Note that if the user role was previously created by using the [!INCLUDE[vmm12short](../../spf/Deploy/includes/vmm12short_md.md)] Administration Console, its permissions would be overwritten by those specified by the **New\-SCSUserRole** cmdlet.  
  
4.  Verify that the user role was created by verifying that it is listed in the **User Roles** in **Settings** workspace in the [!INCLUDE[vmm12short](../../spf/Deploy/includes/vmm12short_md.md)] Administration Console.  
  
5.  Define the following for the role by selecting the role and clicking **Properties** on the toolbar:  
  
    -   On the **Scope** tab, select one or more clouds.  
  
    -   On the **Resources** tab, add any resources such as templates.  
  
    -   On the **Actions** tab, select one or more actions.  
  
    Repeat this procedure for every server assigned to the tenant.  
  
    The next procedure uses the `$TARole` variable that you just created.  
  
### <a name="BMK_CreateSSU"></a>To create a tenant self\-service user role  
  
1.  Enter the following command to create a self\-service user in [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] for the tenant you created in the [To create a tenant with the certificate's public key](../Topic/Walkthrough:%20Creating%20a%20Certificate%20and%20User%20Roles%20for%20Service%20Provider%20Foundation.md#BMK_CreateTenant) procedure.  
  
    ```  
    PS C:\> $TenantSSU = New-SCSPFTenantUserRole -Name ContosoCloudSpaceSSU -Tenant $tenant   
    ```  
  
2.  Create the corresponding tenant user role in [!INCLUDE[vmm12short](../../spf/Deploy/includes/vmm12short_md.md)] by entering the following command:  
  
    ```  
    PS C:\> $vmmSSU = New-SCUserRole -Name ContosoCloudSpaceVMMSSU -UserRoleProfile SelfServiceUser -ParentUserRole $TARole -ID $TenantSSU.ID  
  
    ```  
  
3.  Verify that the user role was created by verifying that it is listed in the **User Roles** in **Settings** workspace in the [!INCLUDE[vmm12short](../../spf/Deploy/includes/vmm12short_md.md)] Administration Console. Notice that the parent of the role is the tenant administrator.  
  
Repeat this procedure as needed for the tenant.  
  
## See Also  
[Manage Certificates and User Roles in Service Provider Foundation](../../spf/Deploy/Manage-Certificates-and-User-Roles-in-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Recommended Administrator Capabilities in Service Provider Foundation](../../spf/Deploy/Recommended-Administrator-Capabilities-in-Service-Provider-Foundation.md)  
[Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md)  
  
