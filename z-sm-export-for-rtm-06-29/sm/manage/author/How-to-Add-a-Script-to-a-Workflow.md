---
title: How to Add a Script to a Workflow
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ad6b643-91de-478d-8d48-440297b81037
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
# How to Add a Script to a Workflow
The Activity Library includes specialized activities that incorporate [!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] scripts, VBScript scripts, or command\-line scripts into workflows. Use a script activity to import the content of the script and to define the parameters that the script requires to run. The [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] creates a task in the management pack to manage the script and store the script content and parameters.  
  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] does not verify the script parameters; therefore, you have to ensure that the script logic handles validation. Also, when you create an incident with an extended property and do not provide a value for the extended property, the value of the parameter is not parsed, and it is passed as $Data\/Property.  
  
 Script activities run as a separate process from the workflows; however, they also run under the security context of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Workflow account.  
  
 Use the following procedure to add a script to a workflow.  
  
### To add a script to a workflow  
  
1.  In the **Management Pack Explorer**, expand **Workflows**, right\-click the workflow that you want, and then click **Edit**. This opens the workflow in the authoring pane.  
  
2.  In the **Activities Toolbox** pane, locate the activity group **Script Activities** and its subgroup **Generic Script Activities**. Drag the script activity that you want to use to a position between the workflow start and workflow end icons or between two existing activities.  
  
3.  Set the script activity properties:  
  
    1.  In the **Details** pane, click any of the properties in the **Activity Inputs** category, and then click the ellipses \(**…**\) button that appears next to the property.  
  
    2.  In the **Configure a Script Activity** dialog box, click **Import Script**. In the **Import** dialog box, select the script file that you want to use, and then click **Open**.  
  
        > [!CAUTION]  
        >  After you import a script for a script activity, if you click **Import Script** again, any new script that you import completely replaces the previous script.  
  
    3.  Click **Script Properties**. To create a parameter for the script, click **New**, and in the **Name** column, type a name.  
  
        > [!NOTE]  
        >  For VBScript script and command script activity, there is no **Name** column.  
  
    4.  To set a value for the parameter, in the **Value** column, type a constant value. If appropriate for the parameter, type switch characters such as ‘\/t’, which is typical for command scripts.  
  
    5.  To bind the parameter to another property so that the parameter obtains its value from that property, click the corresponding ellipses \(**…**\) button. In the **Bind ‘Parameter’ to Activity Property** dialog box, select the property that you want to use.  
  
    6.  If you are working with a script that requires [!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] snap\-ins in order to run, in the **Windows PowerShell snap\-ins** box, type the names of the snap\-ins, separated by semicolons.  
  
    7.  Click **OK** to close the **Configure a Script Activity** dialog box.  
  
## See Also  
 [The Activity Library](../../../sm/manage/author/The-Activity-Library.md)   
 [Adding or Removing Workflow Activities](../../../sm/manage/author/Adding-or-Removing-Workflow-Activities.md)