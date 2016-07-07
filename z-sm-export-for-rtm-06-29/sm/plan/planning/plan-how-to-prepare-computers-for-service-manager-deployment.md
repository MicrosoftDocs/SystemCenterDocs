---
title: How to Prepare Computers for Service Manager Deployment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01284a71-2aaa-4d77-a1d8-b2e0ad80e197
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Prepare Computers for Service Manager Deployment
Use the following procedures to prepare computers for deployment of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
### To prepare computers for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] deployment  
  
1.  Make sure that no Operations Manager 2007 parts are installed on the computers that will host either [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or the data warehouse.  
  
2.  Create an Active Directory group of users that will be assigned to the role of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrators of both the data warehouse and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management groups. For example, create the group **SM\_Admins**.  
  
    > [!NOTE]  
    >  This group of users must be in the same domain that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] is in. Users from any other domain—even child domains—are not supported.  
  
3.  Create the accounts that are necessary for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. For information about the account that is used to run Setup and for the accounts you will have to provide during the setup of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], see [Account Considerations for Running Setup](../../../sm/plan/planning/Account-Considerations-for-Running-Setup.md).  
  
    > [!NOTE]  
    >  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] accounts must be in the same domain that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] is in. Accounts from any other domain—even child domains—are not supported.  
  
4.  Make sure that the Structured Query Language \(SQL\) instances that are used for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] databases are using port number 1433.  
  
5.  If you are installing the databases on a remote computer running Microsoft SQL Server, the user who is running Setup must be a domain user with local administrator permissions on the SQL Server computer.  
  
6.  On computers that will host the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], under **Internet Options**, **Local Area Network \(LAN\) Settings**, select **Bypass proxy server for local addresses**.  
  
7.  Open a browser, and then enter the following two URLs:  
  
    -   http:\/\/\<computer hosting SSRS\>\/reports  
  
    -   http:\/\/\<computer hosting SSRS\>\/reportserver  
  
     If either connection attempt fails or returns an error—for example, **HTTP Error 404.0 Not Found**—complete the steps in the procedure “To configure the reporting server.” Otherwise, continue with the installation of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
### To configure the reporting server  
  
1.  By using an account that has administrator rights, log on to the computer that will host SQL Server Reporting Services \(SSRS\).  
  
2.  Click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, point to **Configuration Tools**, and then click **Reporting Services Configuration Manager**.  
  
3.  In the **Reporting Services Configuration Connection** dialog box, make sure that the information in **Server Name** and **Report Server Instance** is correct, and then click **Connect**.  
  
4.  In the **Connect** pane, click **Web Service URL**.  
  
5.  In the **Report Server Web Service Virtual Directory** area, in the **Virtual Directory** text box, make sure that the entry is **ReportServer**, and then click **Apply**.  
  
6.  In the **Connect** pane, click **Report Manager URL**.  
  
7.  In the **Report Manager Site Identification** area, in the **Virtual Directory** text box, make sure that the entry reads **Reports**, and then click **Apply**.  
  
8.  In the **Connect** pane, click the top entry \(\<server\>\\\<instance\>\).  
  
9. In the **Current Report Server** area, click **Stop**, and then click **Start**.