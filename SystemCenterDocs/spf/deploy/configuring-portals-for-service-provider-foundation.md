---
title: Configuring Portals for Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: service-provider-foundation
ms.tgt_pltfrm: na
ms.date: 10-12-2016
ms.topic: article
ms.assetid: 4c766289-4f3c-4990-be7e-4181f99438ee
author: bwren
ms.author: raynew
manager: cfreeman
---

# Configuring Portals for Service Provider Foundation
>Apples To: System Center 2016

This topic describes how to configure Service Provider Foundation with the following portal applications:  

-  Windows Azure Pack for Windows Server   

-   App Controller   

All portal and client applications use the Service Provider Foundation services to deliver IaaS. For more information, see [Manage Web Services and Connections in Service Provider Foundation](../Manage/Manage-Web-Services-and-Connections.md).  

## Configuring Windows Azure Pack for Windows Server   
Service Provider Foundation provides services and connectivity for delivering IaaS for Windows Azure Pack.  

### <a name="SMP_Procedure"></a>To register Service Provider Foundation in Windows Azure Pack  

1.  On the sever that has Service Provider Foundation installed, make a note of the credential used for the Admin, VMM, Usage, and Provider Application Pool identity in Internet Information Services \(IIS\). You will need this credential for registering the endpoint in Windows Azure Pack.  

2.  Continue with the procedure in [Register the Service Provider Foundation Endpoint for Virtual Machine Clouds](https://technet.microsoft.com/en-us/library/dn457792.aspx) in the Windows Azure Pack for Windows Server documentation.  

## Configuring App Controller   
If a tenant was not created, you can follow the procedures for creating a tenant that are described in [Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](../Manage/Walkthrough-Creating-a-Certificate-and-User-Roles.md).  

#### To connect to App Controller as a Tenant  

1.  The hoster administrator has to provide the tenant's ID to connect to App Controller .  

    If you need to determine the ID, you can use the T:Microsoft.SystemCenter.Foundation.Cmdlet.Get\-SCSPFTenant cmdlet to obtain the ID as shown in the following example:  

    ```  
    PS C:\> Get-SCSPFTenant -Name "ADatum" | Format-List -Property ID  

    Id : 4ce5713a-50a1-434b-b47a-87caad75ba72  
    ```  

    Copy the ID.  

2.  Using the browser, connect to the App Controller management portal.  

3.  Sign in by using your Windows credentials.  

4.  Under **Settings**, click **Connections**, click **Connect**, then select **Service Provider Foundation**.  

5.  In the **Add an External Provider Connection** dialog box, specify the following values:  

    -   **Connection name:**  

        This is the name of the product or service that is used by the tenant.  

    -   **Description:**  

        This  description is optional.  

    -   **Service location:**  

        This is the Service Provider Foundation OData protocol URI for the VMM service, as shown the following example. The URI ends with tenant's ID:  

        `https://contoso.muchspace.com:8090/SC2016/vmm/Microsoft.Management.Odata.svc/4ce5713a-50a1-434b-b47a-87caad75ba72`  

    -   **Certificate file:**  

        This is the location that you specified for the exported certificate (typically with a .pfx extension). For information about how to export the private key from a certificate for this step, see the [Walkthrough: Creating a Certificate and User Roles for Service Provider Foundation](../Manage/Walkthrough-Creating-a-Certificate-and-User-Roles.md).  

    -   **Password:**  

        This is the password that was set in the steps to export the private key certificate.  

For more information about how to connect a hosting provider to App Controller, see [How to Connect to a Hosting Provider in System Center 2016](http://technet.microsoft.com/en-us/library/jj605416.aspx)  

## See Also  
[Portals in Service Provider Foundation](../Get-Started/Portals-in-Service-Provider-Foundation.md)  
