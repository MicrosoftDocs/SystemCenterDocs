---
title: How to Configure Concurrent Sessions and Calls
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76911720-30ec-497b-9dc5-3e8efc1417b6
---
# How to Configure Concurrent Sessions and Calls
By limiting the number of concurrent calls and sessions on the Web Content Server in [!INCLUDE[smlong12](../Token/smlong12_md.md)], you can limit the number of resources used by the [!INCLUDE[smssp](../Token/smssp_md.md)]. Use the following procedure to configure the number of concurrent calls and sessions. For more information, see the MSDN article [<serviceThrottling>](http://go.microsoft.com/fwlink/p/?LinkID=166610) to specify the throttling mechanism of a Windows Communication Foundation \(WCF\) service.

### To configure concurrent calls and sessions

1.  Log in to the computer hosting the Web Content Server with administrative privileges.

2.  Using a text editor of your choosing \(for example, Notepad\), open the Web.config file in the %inetroot%\\inetpub\\wwwroot\\System Center Service Manager Portal\\servicehost folder.

3.  Locate the <serviceBehaviors> section, as shown in the following example:

    ```
    <system.serviceModel>
    <behaviors>
    <serviceBehaviors>
    <behavior name="DefaultHttpServiceBehavior">
    <serviceMetadata httpGetEnabled="true"/>
    <serviceDebug includeExceptionDetailInFaults="true"/>
    <dataContractSerializer maxItemsInObjectGraph="2147483647"/>
    </behavior>
    <behavior name="DefaultHttpsServiceBehavior">
    <serviceMetadata httpsGetEnabled="true"/>
    <serviceDebug includeExceptionDetailInFaults="true"/>
    <dataContractSerializer maxItemsInObjectGraph="2147483647"/>
    </behavior>
    </serviceBehaviors>
    </behaviors>
    ```

4.  Add the line <serviceThrottling maxConcurrentCalls\="160" maxConcurrentSessions\="10000"\/> in both the DefaultHttpServiceBehavior and DefaultHttpsServiceBehavior sections, as shown in the following example:

    ```
    <system.serviceModel>
    <behaviors>
    <serviceBehaviors>
    <behavior name="DefaultHttpServiceBehavior">
    <serviceMetadata httpGetEnabled="true"/>
    <serviceThrottling maxConcurrentCalls="160" maxConcurrentSessions="10000"/>
    <serviceDebug includeExceptionDetailInFaults="true"/>
    <dataContractSerializer maxItemsInObjectGraph="2147483647"/>
    </behavior>
    <behavior name="DefaultHttpsServiceBehavior">
    <serviceMetadata httpsGetEnabled="true"/>
    <serviceDebug includeExceptionDetailInFaults="true"/>
    <serviceThrottling maxConcurrentCalls="160" maxConcurrentSessions="10000"/>
    <dataContractSerializer maxItemsInObjectGraph="2147483647"/>
    </behavior>
    </serviceBehaviors>
    </behaviors>
    ```

5.  Close your text editor, and save the changes.

## See Also
[Managing the System Center 2012 - Service Manager Self-Service Portal](../Topic/Managing-the-System-Center-2012---Service-Manager-Self-Service-Portal.md)

