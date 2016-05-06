---
title: How to Modify a Master Page File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1045902a-3383-4ba9-b788-4ac757d506f7
---
# How to Modify a Master Page File
You can edit some web elements of the [!INCLUDE[smssp](../Token/smssp_md.md)] using Microsoft SharePoint Designer 2010. You can use SharePoint Designer 2010 to modify SharePoint master pages and style sheets. However, customization is limited in this example to formatting. In any of the following example modifications, you can choose customizations that better fit your organization.

> [!NOTE]
> You should have SharePoint Designer 2010 installed before you use the following procedure. However, you can download SharePoint Designer 2010 from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=234803) if you do not already have it installed.

### To modify a master page file

1.  Start a browser, and connect to the [!INCLUDE[smssp](../Token/smssp_md.md)] home page, for example, http:\/\/<WebServerName>:82\/SMPortal.

2.  In the upper left corner, click **Site Actions**, and then select **Edit in SharePoint Designer**.

3.  In the navigation pane, select **Master Pages**, and then in the **Master Pages** list, select **SMPortalPage.master**.

4.  In the **Customization** area, click **Edit file** to open it in the **Advanced Editor**.

5.  Select the title in the design window, and then in the **Tag Properties** pane, under **Appearance**, expand **Font**.

6.  Click the box to the right of **Name**, and then select **Times New Roman**.

7.  In the lower\-left portion of SharePoint Designer 2010, click **Split** to show both the preview pane and the XHTML view of the master file.

8.  Click the **Layout** menu tab, and then click **Manage Layers**.

9. In the **Layers** list, select **s4\-workspace**. The XHTML view appears and selects the corresponding code.

10. At the top of the selected code, right click the code **<div id\=”s4\-worksapce”>**, and then click **Follow Code Hyperlink** to open the CSS file that is associated with the master file.

11. In the CSS file, look for the section labeled `Body{` near the top of the XHTML code, and then under `height:100%`, insert a new line and type **background\-color:\#006600**.

12. Save the CSS and SMPortalPage.master files that you have updated, and then close SharePoint Designer 2010.

13. Refresh your view of the [!INCLUDE[smssp](../Token/smssp_md.md)] to view the changes that you have made.

## See Also
[Managing the System Center 2012 - Service Manager Self-Service Portal](../Topic/Managing-the-System-Center-2012---Service-Manager-Self-Service-Portal.md)

