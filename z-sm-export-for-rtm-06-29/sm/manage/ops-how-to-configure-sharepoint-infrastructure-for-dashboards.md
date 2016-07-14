---
title: How to Configure SharePoint Infrastructure for Dashboards
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1a98298-29f0-4e58-9809-9ba8368bc77c


















---
# How to Configure SharePoint Infrastructure for Dashboards
Before you can create and deploy dashboards for use on the Self-Service Portal in System Center 2012 - Service Manager, you must configure Microsoft SharePoint 2010 and then install Dashboard Designer.  
  
### To configure SharePoint infrastructure for dashboards  
  
1.  Open your web browser, navigate to your top\-level site in SharePoint 2010, click **Site Actions**, and then click **Site Settings**.  
  
2.  Under **Site Collection Administration**, click **Site collection features**. On the **Features** page, click **Activate** next to **SharePoint Server Publishing Infrastructure** and **PerformancePoint Services Site Features**.  
  
3.  Enable the new features at the parent **Site** level by opening the site that you want to be the parent of your Business Intelligence site. Then, under **Site Actions**, click **Site Settings**. Under **Site Actions**, click **Manage site features**. Click **Activate** next to **SharePoint Server Publishing Infrastructure** and **PerformancePoint Services Site Features**.  
  
4.  Next, add a Business Intelligence Center site by opening the site that you want to be the parent of the new site. Click **Site Actions**, and then click **New Site**. On the **New SharePoint Site** page, select the **Business Intelligence Center** site template, type a title and a URL name, and then click **Create**.  
  
5.  As an option, you can create the Business Intelligence Center Site under the  Service Manager Self\-Service Portal Site. To do this, apply the SMPortalTheme: click **Site Actions**, click **Site Settings**, and then under **Look and Feel**, click **Site theme**. Click **Specify a theme**, click **SMPortalTheme**, and then click **Apply**.  
  
6.  Next, configure the PerformancePoint Unattended Service Account by opening the SharePoint Central Administration page. Then, under **Application Management**, click **Manage service applications**. Click **PerformancePoint Service Application**, and then click **PerformancePoint Service Application Settings**. Type your credentials in the **Secure Store and Unattended Service Account** area, and then click **OK**.  
  
7.  If an error message appears that says “The Unattended Service Account cannot be set for the service application,” you can resolve this problem by doing the following:  
  
    1.  Navigate to the **SharePoint 2012 Central Administration** page, and then under **Application Management**, click **Manage service applications**.  
  
    2.  Click **Secure Store Service**, and then click **Generate New Key**.  
  
    3.  Type a pass phrase, and then click **OK**.  
  
8.  On the new Business Intelligence Center site page that you created, move your mouse over the **Monitor Key Performance** area of the page, and then click **Start using PerformancePoint Services**.  
  
9. If an error message appears that says “An error occurred during the processing of \<FolderPath\>\/\<PageName\>.aspx. Code blocks are not allowed in this file,” you can resolve this problem by inserting the following information into the Web.config file between the PageParserPaths tags of your SharePoint site:  
  
    ```  
    <PageParserPaths>  
    <PageParserPath VirtualPath=”<FolderPath>/<PageName>.aspx” CompilationMode=”Always” AllowServerSideScript=”true”/>  
    </PageParserPaths>  
  
    ```  
  
10. On the new page, **click Run Dashboard Designer**, and then in the **Application Run – Security Warning** dialog box, click **Run** to install PerformancePoint Dashboard Designer. Later, you can start Dashboard Designer from the **Start** menu.  
  
## See Also  
 [Creating and Deploying Dashboards](../../../sm/manage/operate/Creating-and-Deploying-Dashboards.md)
