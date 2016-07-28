---
title: Post-Installation Tasks for Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f61c476-ccfd-4067-a3ef-3b8fd525b030
author:bwren
manager:cfreemanwa
---
# Post-Installation Tasks for Service Provider Foundation
After installing, review [Manage Web Services and Connections in Service Provider Foundation](../../spf/Deploy/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md) for important information about web services, credentials, and connections for using Service Provider Foundation.  
  
As the administrator for a hosting provider, there are a few key tasks that you need to perform after you install Service Provider Foundation. You need to populate the Service Provider Foundation database sufficiently to start managing tenants. There are three ways to get started:  
  
-   Portal applications  
  
    If you installed Service Provider Foundation to use with [!INCLUDE[katal_1](../../orch/getstarted/includes/katal_1_md.md)], you can register the Service Provider Foundation web service endpoint and start provisioning virtual machine clouds and create plans for tenants. For more information, see [Register the Service Provider Foundation Endpoint for Virtual Machine Clouds](assetId:///197ac7a4-6ca2-46a4-855d-327979b68ea5).  
  
    If you installed Service Provider Foundation to use with [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)], you can connect to hosting provider. For more information, see [How to Connect to a Hosting Provider in System Center 2012 SP1](assetId:///5f2729ef-9647-4f5f-bb39-27ea8fc3f0e6).  
  
    For detailed information about using portals, see [Portals in Service Provider Foundation](../../spf/Deploy/Portals-in-Service-Provider-Foundation.md).  
  
-   Service Provider Foundation Cmdlets  
  
    These Windows PowerShell cmdlets are suited for performing administrative tasks efficiently. For more information see [Service Provider Foundation cmdlet Reference](http://technet.microsoft.com/library/jj612525(v=sc.20).aspx). For the most current help in the console, run the following command.  
  
    ```powershell  
    PS C:\> update-help -module spfadmin  
    ```  
  
-   Program applications that consume Service Provider Foundation web services  
  
    See the [Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700).  
  
## Populating the database  
  
> [!NOTE]  
> If you installed Service Provider Foundation to use with [!INCLUDE[katal_1](../../orch/getstarted/includes/katal_1_md.md)], all virtual machines and clouds defined in [!INCLUDE[vmmblue_1](../../om/manage/includes/vmmblue_1_md.md)] will automatically appear on the **VM Clouds** tab on the --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- management portal for administrators. There is no need to use Windows PowerShell to define them.  
  
A basic, general procedure for populating the SCSPF database using cmdlets is as follows:  
  
```powershell  
PS C:\> # Create a server.  
PS C:\> $server = New-SCSPFServer -Name "server23G.contoso.com" -ServerType VMM  
PS C:\> # Create a stamp. A stamp is a logical container for a tenant's association with one or more servers.  
PS C:\> $stamp = New-SCSPFStamp -Name "StampA" -Servers $server  
PS C:\> # Create a tenant. A tenant is your paying customer or business unit.  
PS C:\> $tenant = New-SCSPFTenant -Name "jonathan@treyresearch.net"  
PS C:\> # Associate the stamp to the tenant. You can set the stamp to the tenant and also to a different server if needed.  
PS C:\> Set-SCSPFStamp -Stamp $stamp -Tenants $tenant  
```  
  
## See Also  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Architecture Overview of Service Provider Foundation](../../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
[Integrating Service Management Portal and API with System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=298454)  
  
