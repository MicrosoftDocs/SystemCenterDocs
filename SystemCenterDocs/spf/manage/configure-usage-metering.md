---
title: Configure Usage Metering in Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64dc6b07-c226-4104-b18d-11ef2f3d4e12
author: bwren
manager: cfreeman
---
# Configure Usage Metering in Service Provider Foundation
>Apples To: System Center 2016

This topic describes how to configure Service Provider Foundation to aggregate usage statistics for queries by the Service Provider Foundation Usage web service. For more information, see the "Usage web service" section in [Usage web service](../Manage/Manage-Web-Services-and-Connections.md#SPF_Usage).  

Connection settings are stored in the Service Provider Foundation database.  

The minimum topology for implementing usage metering collection is as follows:  

-   One server running Service Provider Foundation  

-   One server running System Center 2016 - Virtual Machine Manager \(VMM\)  

-   One server running System Center 2016 Operations Manager  that has an Operations Manager Data Warehouse \(OMDW\) database  

-   One or more virtual machines hosted by Hyper V (or VMM), and System Center 2016 Operations Manager themselves.  

If needed, all these components can all be on the same computer.  

## Service Provider Foundation System Center 2016 configuration  
Use Windows PowerShell and the Service Provider Foundation cmdlets to configure usage metering as described in the following procedure. For the cmdlets, see [Service Provider Foundation cmdlet Reference](http://technet.microsoft.com/library/jj612525.aspx).  

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
    PS C:\>$setting = New-SCSPFSetting -Name mysetting -SettingType DatabaseConnectionString -Value "Server=myomdwserver\myomdwinstance;Database=OperationsManagerDW;Trusted_Connection=True;Connect Timeout=300" -Server $omdwserver  

    ```  

The recommended connection timeout is 300 seconds, or 5 minutes. This value is also dependent on the volume of virtual machine usage metrics, SQL server edition \(Enterprise recommended\), hardware capacity, among other environment settings. You can change the connection timeout value using the next procedure in this guide.  

Use the Get\-SCSPFSetting cmdlet to make changes to a particular setting. For example, the following code associates the setting with a different server, that is stored in the `$newSvr` variable.  

```powershell  
PS C:\>$myset = Get-SCSPFSetting -Name "mySetting"  
PS C:\>$myset.Server = $newSvr  

```  

## Service Provider Foundation System Center 2016 configuration  
The following configuration is required to enable usage metering:  

-   A server running Service Provider Foundation.  

-   The Windows Azure Pack for Windows Server and API to provision IaaS.  

-   A server running System Center 2016 Operations Manager with the management packs installed for VMM. See [Using Management Packs](http://technet.microsoft.com/en-us/library/hh212709.aspx) for more information.  

-   A server running SQL Server with the Operations Manager Data Warehouse \(OMDW\). For more information, see [How to Install the Operations Manager Reporting Server](http://technet.microsoft.com/en-us/library/hh298611.aspx).  

    You can have the database for the OMDW and the database for Service Provider Foundation on the same server.  

-   A Usage application pool identity credential that must be specified as a logon account to the OMDW databases. This account must have the db\_DataReader and OpsMgrReader user mappings on each OMDW database. This is the same account specified for the Service Provider Foundation database.  

## See Also  
[Usage Metering Data Model in Service Provider Foundation](../Manage/configure-usage-metering.md)    
[Deploying Service Provider Foundation](../Deploy/Deploying-Service-Provider-Foundation.md)  
