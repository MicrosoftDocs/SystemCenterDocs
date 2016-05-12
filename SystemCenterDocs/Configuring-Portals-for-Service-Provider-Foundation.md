---
title: Configuring Portals for Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c766289-4f3c-4990-be7e-4181f99438ee
---
# Configuring Portals for Service Provider Foundation
This topic describes how to configure [!INCLUDE[spfshort](Token/spfshort_md.md)] with the following portal applications:

-   [!INCLUDE[katal_1](Token/katal_1_md.md)]

-   [!INCLUDE[conceroshort](Token/conceroshort_md.md)]

All portal and client applications use the [!INCLUDE[spfshort](Token/spfshort_md.md)] services to deliver IaaS. For more information, see [Manage Web Services and Connections in Service Provider Foundation](Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md).

## Configuring [!INCLUDE[katal_1](Token/katal_1_md.md)]
[!INCLUDE[spflong](Token/spflong_md.md)] provides services and connectivity for delivering IaaS for [!INCLUDE[katal_2](Token/katal_2_md.md)].

### <a name="SMP_Procedure"></a>To register [!INCLUDE[spfshort](Token/spfshort_md.md)] in [!INCLUDE[katal_2](Token/katal_2_md.md)]

1.  On the sever that has [!INCLUDE[spfshort](Token/spfshort_md.md)] installed, make a note of the credential used for the Admin, VMM, Usage, and Provider Application Pool identity in Internet Information Services \(IIS\). You will need this credential for registering the endpoint in [!INCLUDE[katal_2](Token/katal_2_md.md)].

2.  Continue with the procedure in [Register the Service Provider Foundation Endpoint for Virtual Machine Clouds](assetId:///197ac7a4-6ca2-46a4-855d-327979b68ea5) in the [!INCLUDE[katal_1](Token/katal_1_md.md)] documentation.

## Configuring [!INCLUDE[conceroshort](Token/conceroshort_md.md)]
If a tenant was not created, you can follow the procedures for creating a tenant that are described in [Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](Walkthrough--Creating-a-Certificate-and-User-Roles-for-Service-Provider-Foundation.md).

#### To connect to [!INCLUDE[conceroshort](Token/conceroshort_md.md)] as a Tenant

1.  The hoster administrator has to provide the tenant's ID to connect to [!INCLUDE[conceroshort](Token/conceroshort_md.md)].

    If you need to determine the ID, you can use the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFTenant cmdlet to obtain the ID as shown in the following example:

    ```
    PS C:\> Get-SCSPFTenant -Name "ADatum" | Format-List -Property ID

    Id : 4ce5713a-50a1-434b-b47a-87caad75ba72
    ```

    Copy the ID.

2.  Using the browser, connect to the [!INCLUDE[conceroshort](Token/conceroshort_md.md)] management portal.

3.  Sign in by using your Windows credentials.

4.  Under **Settings**, click **Connections**, click **Connect**, then select **Service Provider Foundation**.

5.  In the **Add an External Provider Connection** dialog box, specify the following values:

    -   **Connection name:**

        This is the name of the product or service that is used by the tenant.

    -   **Description:**

        This  description is optional.

    -   **Service location:**

        This is the [!INCLUDE[spfshort](Token/spfshort_md.md)] OData protocol URI for the VMM service, as shown the following example. The URI ends with tenant's ID:

        `https://contoso.muchspace.com:8090/SC2012R2/vmm/Microsoft.Management.Odata.svc/4ce5713a-50a1-434b-b47a-87caad75ba72`

        If you are using [!INCLUDE[spfshort](Token/spfshort_md.md)][!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)], remove the 'R2' from SC2012R2.

    -   **Certificate file:**

        This is the location that you specified for the exported certificate \(typically with a .pfx extension\). For information about how to export the private key from a certificate for this step, see the [To export the private key](Walkthrough--Creating-a-Certificate-and-User-Roles-for-Service-Provider-Foundation.md#BMK_ExportPrivate) procedure in [Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](Walkthrough--Creating-a-Certificate-and-User-Roles-for-Service-Provider-Foundation.md).

    -   **Password:**

        This is the password that was set in the steps to export the private key certificate.

For more information about how to connect a hosting provider to [!INCLUDE[conceroshort](Token/conceroshort_md.md)], see [How to Connect to a Hosting Provider in System Center 2012 SP1](assetId:///5f2729ef-9647-4f5f-bb39-27ea8fc3f0e6)

## See Also
[Portals in Service Provider Foundation](Portals-in-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](Administering-Service-Provider-Foundation.md)


