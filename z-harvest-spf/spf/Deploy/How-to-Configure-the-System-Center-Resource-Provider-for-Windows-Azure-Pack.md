---
title: How to Configure the System Center Resource Provider for Windows Azure Pack
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95bdbd33-82f5-4474-8472-f5b9dd9524ea
author:bwren
manager:cfreemanwa
---
# How to Configure the System Center Resource Provider for Windows Azure Pack
  
> [!IMPORTANT]  
> This topic should be used only for the earlier versions of [!INCLUDE[katal_1](../../orch/getstarted/includes/katal_1_md.md)] when the Service Provider Foundation could not be changed in the --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- management portal for administrators. This is no longer the case. For more information, see [Register the Service Provider Foundation Endpoint for Virtual Machine Clouds](assetId:///197ac7a4-6ca2-46a4-855d-327979b68ea5).  
  
If you want to change the location of the Service Provider Foundation server, or the username and password for the account, that has been registered with --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API, you will need to change the System Center resource provider settings by using the Management Service Configuration Windows PowerShell cmdlets.  
  
This topic describes how to update the Service Provider Foundation URLs that have been configured as endpoints by --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API.  
  
When a portal administrator registers Service Provider Foundation in the Admin Portal, the --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API uses the base URL \(for example: `https://spfserver.constoso.skyspace.com:8090/`\) to create the following endpoints:  
  
-   AdminEndpoint  
  
-   TenantEndpoint  
  
-   NotificationEndPoint \(Use by the Provider service in Service Provider Foundation\)  
  
-   UsageEndPoint  
  
    The usage endpoint is registered separately in --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API but takes the same base URL. For more information about configuring usage metering, see [Configure Usage Metering in Service Provider Foundation](../../spf/Deploy/Configure-Usage-Metering-in-Service-Provider-Foundation.md).  
  
If you changed the location of your Service Provider Foundation server, you will need to change the URL, username and password for each of these endpoints. The HealthCheckNotificationEndpoint is reserved for future use and is not configured.  
  
The username and passwords for the Admin, Tenant, and Notification endpoints must be for the account specified on the Service Provider Foundation server  in the **Local Users and Groups** for the local SPF\_Admin, SPF\_VMM, and SPF\_Provider groups. For more information, see the section "Verify local user credentials for portal access" in [Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md#LocalCreds).  
  
For more information about registering Service Provider Foundation in --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API, see the 'Provision Virtual Machine Clouds' section of [Provisioning Services](http://msdn.microsoft.com/library/jj838661.aspx).  
  
### To change Service Provider Foundation endpoints  
  
1.  On the server that has the Service Management Admin API installed, run the Management Service Configuration PowerShell console.  
  
2.  If needed, import the module:  
  
    ```  
    PS C:\> Import-Module -name MgmtSvcConfig  
    ```  
  
3.  Verify that you have the Admin API:  
  
    ```  
    PS C:\> Get-MgmtSvcNamespace  
    ```  
  
    Results should include 'AdminAPI'.  
  
4.  Get the XML of the current System Center resource provider to review and save for your records:  
  
    ```  
    PS C:\> Get-ResourceProvider -name systemcenter -As XmlString | out-file 'c:\temp\resourceproviderSC2012.xml'   
    ```  
  
5.  Get the System Center resource provider as an object variable named `$rp`.  
  
    ```  
    PS C:\> $rp = Get-ResourceProvider -name systemcenter  
    ```  
  
6.  Create variables for the username and password to your Service Provider Foundation server:  
  
    ```  
    PS C:\> $username = 'Administrator'  
    PS C:\> $pwd = '00cc7urPWD'  
    ```  
  
7.  Display the settings for the Admin endpoint:  
  
    ```  
    PS C:\> $rp.AdminEndpoint  
    ```  
  
8.  Set the following properties to their new values. Also specify 'Basic' for the AuthenticationMode to ensure that it does not get cleared as credentials are changed.  
  
    ```  
    PS C:\> $rp.AdminEndpoint.ForwardingAddress = 'https://spfserver2.contoso.skyspace.com:8090/'  
    PS C:\> $rp.AdminEndpoint.AuthenticationMode = 'Basic'  
    PS C:\> $rp.AdminEndpoint.AuthenticationUserame = $username  
    PS C:\> $rp.AdminEndpoint.AuthenticationPassword = $pwd  
    ```  
  
9. Display the settings for the Tenant endpoint:  
  
    ```  
    PS C:\> $rp.TenantEndpoint  
    ```  
  
10. Set the properties:  
  
    ```  
    PS C:\> $rp.TenantEndpoint.ForwardingAddress = 'https://spfserver2.contoso.skyspace.com:8090/SC2012/VMM/'  
    PS C:\> $rp.TenantEndpoint.AuthenticationMode = 'Basic'  
    PS C:\> $rp.TenantEndpoint.AuthenticationUserame = $username  
    PS C:\> $rp.TenantEndpoint.AuthenticationPassword = $pwd  
    ```  
  
11. Display the settings for the Notification endpoint:  
  
    ```  
    PS C:\> $rp.NotificationEndpoint  
    ```  
  
12. Set the properties:  
  
    ```  
    PS C:\> $rp.NotificationEndpoint.ForwardingAddress = 'https://spfserver2.contoso.skyspace.com:8090/provider/'  
    PS C:\> $rp.NotificationEndpoint.AuthenticationMode = 'Basic'  
    PS C:\> $rp.NotificationEndpoint.AuthenticationUserame = $username  
    PS C:\> $rp.NotificationEndpoint.AuthenticationPassword = $pwd  
    ```  
  
13. If you registered the Usage endpoint you will also need to change it. Display the settings for the Usage endpoint:  
  
    ```  
    PS C:\> $rp.UsageEndpoint  
    ```  
  
    If nothing was returned or the XML appears as shown below, skip the next step that sets properties and instead register the Usage endpoint with the new URL in the Admin Portal when you are ready.  
  
    ```  
    <UsageEndpoint i:nil="true" />  
  
    ```  
  
14. Set the properties:  
  
    ```  
    PS C:\> $rp.UsageEndpoint.ForwardingAddress = 'https://spfserver2.contoso.skyspace.com:8090/'  
    PS C:\> $rp.UsageEndpoint.AuthenticationMode = 'Basic'  
    PS C:\> $rp.UsageEndpoint.AuthenticationUserame = $username  
    PS C:\> $rp.UsageEndpoint.AuthenticationPassword = $pwd  
    ```  
  
15. You can now update the endpoints by adding the  
    resource provider object with the \-*Force* parameter so that the System Center resource provider is overwritten with the updated values. Type:  
  
    ```  
    PS C:\>Add-ResourceProvider -ResourceProvider $rp -Force  
    ```  
  
## See Also  
[Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md)  
[Portals in Service Provider Foundation](../../spf/Deploy/Portals-in-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
  
