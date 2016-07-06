---
title: How to Add Permissions for Standard Reports
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c04e33d3-ceb3-497d-b4da-cffd7402c02a
translation.priority.mt: 
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
# How to Add Permissions for Standard Reports
By default, all [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] users have access to reports through the Reporting workspace. However, before users who do not have administrator permissions can view the Reporting workspace, you must add permissions through SQL Server Reporting Services \(SSRS\).  
  
 You can grant access at the root level, which enables a user to view the Reporting workspace and all the reports in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. You can also grant restricted access to specific report folders, such as the Incident report folder, or to individual reports.  
  
 The following procedure describes how to grant SSRS access for all the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] reports to an Active Directory group \(woodgrove\\SCSMReportAccess\).  
  
### To add SSRS permissions  
  
1.  On the computer on which SRSS is installed, start Report Manager. For example, open http:\/\/\<ReportServerName\>:80\/Reports.  
  
2.  Locate the folder or report for which you want to grant access permission. For example, locate the SystemCenter and ServiceManager root folders.  
  
3.  Click **Security**.  
  
4.  Click **Edit Item Security**.  
  
5.  The following message appears: "Item security is inherited from a parent item. Do you want to apply security settings for this item that are different from those of the Home parent item?"  
  
     Click **OK**.  
  
6.  Click **New Role Assignment**.  
  
7.  Type the name of the Active Directory group or user in the **Group or user name** box. For example, type **woodgrove\\SCSMReportAccess**.  
  
8.  Set the roles for the group or user. Select the **Browser** check box to grant access to run reports.  
  
9. Click **OK**.  
  
## See Also  
 [Using and Managing Standard Reports](../../../sm/manage/operate/Using-and-Managing-Standard-Reports.md)