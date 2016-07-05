---
title: How to Customize the Default Incident Form (Sample Scenario)
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2af8b9d4-f736-4f96-b058-a96b10a64aca
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
# How to Customize the Default Incident Form (Sample Scenario)
This sample scenario describes how to apply simple customizations to a default form in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)]. In this scenario, you customize the Incident form, which is the default form for interacting with incidents. You customize the form in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] and then save the customized form in a new management pack. Then, in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], you import this new management pack. Afterwards, whenever you create or view an incident, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] displays the customized form. The Incident form, System.WorkItem.Incident.ConsoleForm, is defined in the Service Manager Incident Management Library management pack.  
  
 The sample scenario for customizing the default Incident form consists of three steps.  
  
### Step 1: View the Default Incident Form  
 Before you customize the form, view the default form in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] and identify elements on the form that you want to customize. For example, you can plan to rearrange various text boxes on the form.  
  
##### To view the default incident form  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, click **Incident Management**.  
  
3.  In the **Tasks** pane, click **Create Incident**.  
  
4.  Review the **Incident** form. This form is the form that you use to create and view incidents. You can identify elements in the form that you might want to customize.  
  
### Step 2: Customize the Default Incident Form  
 Use the following procedure to customize the default Incident form in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
##### To customize the Incident form  
  
1.  Click **Start**, point to **Programs**, point to **Microsoft System Center**, point to **Service Manager 2012 Authoring**, and then click **Service Manager Authoring Tool**.  
  
2.  In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **File**, and then click **New**.  
  
3.  In the **New Management Pack** dialog box, in the **File name** box, type **MyIncidentFormCustomizations**, and then click **Save**.  
  
     Note that the **MyIncidentFormCustomizations** management pack is now listed in the **Management Pack Explorer**.  
  
4.  In the **Form Browser** pane, locate and then right\-click the **System.WorkfItem.Incident.ConsoleForm** form, which is the default Incident form, and then click **View**.  
  
     Note that the **Service Manager Incident Management Library** management pack, which contains the default Incident form, is now listed in the **Management Pack Explorer**.  
  
5.  In the authoring pane, click **Customize**.  
  
6.  In the **Target Management Pack** dialog box, select **MyIncidentFormCustomizations**, and then click **OK**.  
  
7.  Wait for the authoring pane to display the form that you are customizing. You can now add controls, such as a **Label**, a **Text Box**, or an **Image**, to the form. Ensure that the **Details** window is open and visible, so that you can browse and modify properties of the controls.  
  
8.  In the **Management Pack Explorer**, right\-click **MyIncidentFormCustomizations**, and then click **Save**.  
  
9. Exit the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
### Step 3: Use the Customized Default Incident Form  
 Use the following procedure to view and use the customized Incident form in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
##### To use the customized System.WorkItem.Incident.ConsoleForm form  
  
1.  Start the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], and then click **Administration**.  
  
2.  In the **Administration** pane, click **Management Packs**.  
  
3.  In the **Tasks** pane, click **Import**.  
  
4.  In the **Select Management Packs to Import** dialog box, click the **MyIncidentFormCustomizations.xml** management pack file. Click **Open**.  
  
5.  In the **Import Management Packs** dialog box, click **Import**, wait for the management pack to be imported, and then click **OK**.  
  
6.  Click **Incidents**, and then in the **Tasks** pane, click **Create Incident**.  
  
     Note that the **Incident** form that is displayed is your customized form.  
  
7.  Fill in the form, and then save the incident.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)