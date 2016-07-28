---
title: Configure Usage Metering in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64dc6b07-c226-4104-b18d-11ef2f3d4e12
author:bwren
manager:cfreemanwa
---
# Configure Usage Metering in Service Provider Foundation
This topic describes how to configure Service Provider Foundation to aggregate usage statistics for queries by the Service Provider Foundation Usage web service. For more information, see the "Usage web service" section in [Usage web service](../../spf/Deploy/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md#SPF_Usage).  

In Service Provider FoundationSystem Center 2012 SP1 , connection settings were maintained in the web.config file for the Usage service. Beginning with Service Provider FoundationSystem Center 2012 R2, these settings are stored in the  Service Provider Foundation database.  

The minimum topology for implementing usage metering collection is as follows:  

-   One server running Service Provider Foundation  

-   One server running --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- System&nbsp;Center&nbsp;2012&nbsp;- Virtual&nbsp;Machine&nbsp;Manager&nbsp;\(VMM\)  

-   One server running System Center 2012 Operations Manager  that has an Operations Manager Data Warehouse \(OMDW\) database  

-   One or more virtual machines hosted by Hyper V \(or --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- VMM\) and managed by VMM to generate usage data. These can also be the severs running Service Provider Foundation, --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- VMM, and System Center 2012 Operations Manager  themselves.  

If needed, all these components can all be on the same computer.  

## Service Provider FoundationSystem Center 2012 R2 configuration  
Use Windows PowerShell and the Service Provider Foundation cmdlets to configure usage metering as described in the following procedure. For the cmdlets, see [Service Provider Foundation cmdlet Reference](http://technet.microsoft.com/library/jj612525(v=sc.20).aspx).  

Also see the blog post [Configuring SPF and Windows Azure Pack for IaaS usage and metering](http://blogs.technet.com/b/privatecloud/archive/2013/10/01/configuring-spf-and-windows-azure-pack-for-iaas-usage-and-metering.aspx).  

-   Create an instance of a server \(using the **New\-SCSPFServer** cmdlet\) with the *ServerType* as OMDW.  

-   Use the **New\-SCSPFSetting** cmdlet to create a setting on that server \(the one created in the previous step\), that has the connection string to OperationsManagerDW database on the OMDW server.  

-   Verify that the Application Pool account under which SPF\_Usage runs has the ability to query OMDW.  

-   Verify sure that the Windows Azure Pack calling account is a member of the SPF\_User local security group on the server that has Service Provider Foundation installed.  

#### To set OMDW connection settings  

1.  Run the **New\-SCSPFSetting** command with the parameters described in the following table.  

    |New\-SCSPFSetting Parameter|Value|  
    |-------------------------------|---------|  
    |Value|Required. Must be a database connection string.|  
    |SettingType|Required. Must be **DatabaseConnectionString**.|  
    |Name|Optional. This setting is recommended. Specify a meaningful name for each setting.|  
    |Server|Associates the setting with the sever from which usage metering is to be obtained. Must be a server object obtained from the Get\-SCSPFServer cmdlet.|  

    For example:  

    ```powershell  
    PS C:\> $omdwserver = New-SCSPFServer -Name "omdw.contoso.com" -ServerType OMDW  
    PS C:\>$setting = New-SCSPFSetting -Name mysetting -SettingType DatabaseConnectionString -Value&nbsp;"Server=myomdwserver\myomdwinstance;Database=OperationsManagerDW;Trusted_Connection=True;Connect Timeout=300" -Server $omdwserver  

    ```  

The recommended connection timeout is 300 seconds, or 5 minutes. This value is also dependent on the volume of virtual machine usage metrics, SQL server edition \(Enterprise recommended\), hardware capacity, among other environment settings. You can change the connection timeout value using the next procedure in this guide.  

Use the Get\-SCSPFSetting cmdlet to make changes to a particular setting. For example, the following code associates the setting with a different server, that is stored in the `$newSvr` variable.  

```powershell  
PS C:\>$myset = Get-SCSPFSetting -Name "mySetting"  
PS C:\>$myset.Server = $newSvr  

```  

## Service Provider FoundationSystem Center 2012 SP1  configuration  
The following configuration is required to enable usage metering:  

-   A server running Service Provider Foundation that has the Windows Update package KB2785476 installed. This update is included in the Update Rollup 1 for System Center 2012 SP1. If the update was already installed automatically by Windows Update, the following directory should exist:  **C:\\inetpub\\SPF\\Usage**. If the update was not installed, see the next section of this topic.  

-   The --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-tw --- Windows Azure Pack for Windows Server and API to provision IaaS.  

-   A server running System Center 2012 Operations Manager  with the management packs installed for --- translation.priority.ht:    - ar-sa   - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - he-il   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ro-ro   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- VMM. See [Using Management Packs](assetId:///1d4f1e8c-38c3-4ee2-819f-9e47073b38e2) for more information.  

-   A server running SQL Server with the Operations Manager Data Warehouse \(OMDW\). For more information, see [How to Install the Operations Manager Reporting Server](assetId:///15404d1e-ad4b-4734-997c-c4992aba31ad).  

    You can have the database for the OMDW and the database for Service Provider Foundation on the same server.  

-   A Usage application pool identity credential that must be specified as a logon account to the OMDW databases. This account must have the db\_DataReader and OpsMgrReader user mappings on each OMDW database. This is the same account specified for the Service Provider Foundation database.  

If Windows Update is controlled by your System Administrator, the update might not have been installed automatically. If the update was not installed, you can install it from Windows Update or from the Microsoft Update Catalog. The required update for usage metering, included in the rollup, is KB2785476 for Service Provider Foundation.  

#### To install the update from Windows Update  

1.  In **Control Panel**, in Category View, select **System and Security** and then **Windows Update**.  

2.  Click **Check Online for updates from Microsoft Update**.  

3.  Click **Important updates are available**.  

4.  Verify that the Update Rollup 1 package KB2785476 is selected, and then click **OK**.  

#### To install the update manually  

1.  Go to [Microsoft Update Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=2785476) \(http:\/\/catalog.update.microsoft.com\/v7\/site\/Search.aspx?q\=2785476\).  

    The **Update for System Center 2012 SP1 Orchestrator - SPF \(KB2785476\)** should be the only item in the search results.  

2.  Click **Add**, and then click **view basket**.  

3.  Click **Download** and then following then specify options to download.  

4.  At the location of the download, double\-click the CAB file under the Update for **System Center 2012 SP1 Orchestrator \- SPF \(KB2785476\)** folder.  

5.  Double\-click the **KB2785476\_SFPUsage.msp** file to install the update.  

Verify that the update was successful by checking to see of the **C:\\inetpub\\SPF\\Usage** folder exists.  

For more information about the update, see the [Description of Update Rollup 1 for System Center 2012 Service Pack 1](http://support.microsoft.com/kb/2785682)  

> [!IMPORTANT]  
> The update sets the authentication identity for the Service Provider Foundation VMM service in the **Internet Information System \(IIS\) Manager** Application Pools to Network Service. You must change the VMM service in the application pool back to its identity when Service Provider Foundation was installed \(unless it was intended to be Network Service\). To do so, click **Advanced Settings** for the VMM application pool identity, and set the **Identity** value in the **Process Model** section of the dialog box.  

You must specify the connection strings for all of the participating OMDW databases, and then apply a SQL Server script to update the databases with the required tables and triggers to implement usage metering.  

#### To specify OMDW connection strings  

1.  Edit the **c:\\inetpub\\SPF\\Usage\\web.config** file in a text editor and locate the `<connectionStrings>` element. This element initially appears as follows:  

    ```  
    <connectionStrings>  
        <add name="OMDWConnectionString"   
             connectionString=""/>  
      </connectionStrings>  
    ```  

2.  Edit the element to contain the connection settings for each OMDW database, as shown in the following example. In this example, two virtual machines are configured for usage metering.  

    ```  
    <connectionStrings>  
    <add name="OMDWBasicPlusVMs"   
    connectionString="Server='sky200.contoso.com'";  
    Database=OMDWSPFUsage;  
    Trusted_Connection=True;  
    MultipleActiveResultSets=True;"/>  
    <add name="OMDW"   
    connectionString="Server='sky400.contoso.com'";  
    Database=OMDWSPFUsage;  
    Trusted_Connection=True;  
    MultipleActiveResultSets=True;"/>  
    </connectionStrings>  
    ```  

#### To apply the Update Rollup 1 Service Provider Foundation database update script  

1.  Copy the **c:\\inetpub\\SPF\\Usage\\KB2875476\\SPFUsageFeatureUpdate.sql** file to the server where the database for Service Provider Foundation is installed. This can be the same server.  

2.  Double\-click the **SPFUsageFeatureUpdate.sql** file to apply the rollup. SQL Server Management Studio will launch.  

3.  The following permissions must be specified for the SCSPFDB database if the application pool identity credential of the Usage endpoint and the VMM endpoint are the same. Right\-click the SCSPFDB database, click **Properties**, and then click **Permissions**. Verify that the following permissions are granted:  

    -   Connect  

    -   Delete  

    -   Insert  

    -   Select  

    -   Update  

    These permissions are required because the VMM endpoint is more restricted than what usage metering can access, and they must be compatible.  

4.  Add the following permissions to the new **OnPremServicesCollectorSessions**, **OnPremServicesSubscriberWatermarks**, and **OnPremServicesSubscriberTombstones** tables:  

    -   Delete  

    -   Insert  

    -   Select  

    -   Update  

We recommend these permissions as best practices. The permission structure that we recommend here is the minimum set that is required. You can apply a more or less restrictive permissions scheme, depending on your security policies.  

Ensure that the following authentication tasks have been completed:  

-   The application pool identity credentials for the VMM service for Service Provider Foundation is correct after installing the update package KB2785476.  

-   The application pool identity credentials for the Service Provider Foundation Admin, Provider, VMM, and Usage services should all be the same.  

-   On the computers that are running Microsoft SQL Server where the OMDW databases reside, verify that the Usage Application Pool account that you configured has logon rights and read permission.  

-   The account for SPF\_Usage in **Local Users and Groups** on the server where Service Provider Foundation is installed belongs to the Administrators account.  

## See Also  
[Usage Metering Data Model in Service Provider Foundation](../../spf/Deploy/Usage-Metering-Data-Model-in-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
