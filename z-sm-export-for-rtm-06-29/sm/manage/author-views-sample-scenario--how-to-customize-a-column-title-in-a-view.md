---
title: Views Sample Scenario: How to Customize a Column Title in a View
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a48640f-1ecf-4636-912e-42d9000cebc7
 

















---
# Views Sample Scenario: How to Customize a Column Title in a View
System Center 2012 - Service Manager contains predefined views that you can use to display information and status of various work items and configuration items in the Service Manager console. Views are defined in unsealed management packs, allowing for some customizations of views.  
  
 For example, you can use the following procedure to customize a column title of a predefined view to reflect processes that are used in your organization.  
  
 Another customization to a view is adding a column to a predefined view. For more information about adding a column to an existing view, see the [Editing a View in a Management Pack](http://go.microsoft.com/fwlink/p/?LinkID=204706) blog.  
  
### To customize a column title in a view  
  
1.  Locate and export the management pack that contains the view that you want to customize, as follows:  
  
    1.  In the Service Manager console, click **Administration**.  
  
    2.  In the **Administration** pane, select **Management Packs**.  
  
    3.  In the **Management Packs** view, click **Sealed** to sort the column by sealed and unsealed management packs. Select the management pack that contains the view that you want to customize. It must be an unsealed management pack, such as **Service Manager Incident Management Configuration Library**.  
  
    4.  In the **Tasks** pane, click **Export**.  
  
    5.  In the **Browse For Folder** dialog box, select a folder to store the exported management pack, and then click **OK**.  
  
2.  Open the exported management pack in an XML editor, such as Notepad or Microsoft Visual Studio.  
  
3.  Update the management pack, as follows:  
  
    1.  In the **\<LanguagePacks\>** section of the file, locate the **DisplayString** for the column that you want to customize.  
  
         This example shows the code for the **My Incidents** view:  
  
        ```  
        System.WorkItem.Incident.AssignedToMe.View  
        ```  
  
         and the code for the **Category** column in that view:  
  
        ```  
        System.WorkItem.Incident.AssignedToMe.View.Header_Category  
        ```  
  
         and the **DisplayString** for the **Category** column in the **My Incidents** view:  
  
        ```  
        <DisplayString ElementID="System.WorkItem.Incident.AssignedToMe.View.Header_Category">  
            <Name>Category</Name>  
            <Description>Category</Description>  
        </DisplayString>  
        ```  
  
    2.  Replace the column title inside the **\<Name\>\<\/Name\>** tags and inside the **\<Description\>\<\/Description\>** tags with the custom column title. For example, replace **Category** with **My Organization’s Category**.  
  
4.  Save the custom management pack.  
  
5.  Import the custom management pack in Service Manager:  
  
    1.  In the **Administration** pane, select **Management Packs**.  
  
    2.  In the **Tasks** pane, click **Import**.  
  
    3.  In the **Select Management Pack to Import** dialog box, select a folder in which you stored the custom management pack, and then click **Open**.  
  
    4.  In the **Import Management Pack** dialog box, click **Import**. Wait for the import to complete, and then click **OK**.  
  
 In the Service Manager console, select the view that you customized to see the new column title.  
  
## See Also  
 [Authoring for System Center 2012 \- Service Manager](../../../sm/manage/author/Authoring-for-System-Center-2012---Service-Manager.md)
