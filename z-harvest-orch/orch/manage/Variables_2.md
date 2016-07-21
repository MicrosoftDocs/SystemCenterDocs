---
title: Variables_2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21c02bba-dc10-4f9a-9d19-2ea9b3d34cf9
author:bwren
manager:cfreemanwa
---
# Variables_2
When building runbooks in [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)], some settings are the same across activities. Variables let you specify a value that activities use in any runbook.  
  
> [!IMPORTANT]  
> The access permissions for variables can be modified, but the runbook server does not enforce these permissions.  
  
> [!IMPORTANT]  
> Be aware that in [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)], variables that reference system variables, for example **%ProgramFiles%**, return values from a 32\-bit runtime environment. This is because [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] is a 32\-bit application.  
  
> [!NOTE]  
> [!INCLUDE[orchshort](../../om/manage/includes/orchshort_md.md)] does not support moving multiple variables with multiple\-selection. To move more than one variable to another folder, you must move each variable individually.  
  
Use the following procedures to create, insert, and organize variables.  
  
### To create a variable  
  
1.  In the **Connections** pane in the Runbook Designer, expand the **Global Settings** folder, and then click the **Variables** folder.  
  
2.  Right\-click the **Variables** folder or a subfolder of the **Variables** folder to select **New**, and then click **Variable** to open the **New Variable** dialog box.  
  
3.  In the **Name** box, type a name for the variable.  
  
4.  In the **Description** box, type a description that explains the purpose of the variable.  
  
5.  In the **Value** box, type the value of the variable. This value replaces the placeholder in those activities where the variable is inserted.  
  
6.  If you want the variable to be encrypted \(for example, to store a password for use in other runbook activities\), select the **Encrypted Variable** check box.  
  
    For more information about best practices for using encrypted variables, see [Orchestrator Data Encryption](assetId:///4064c993-59b3-483c-8488-6f28298fb00a).  
  
7.  Click **Finish**.  
  
> [!IMPORTANT]  
> [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] does not let you combine an encrypted variable with plain text as a parameter value in a runbook.  
  
### To insert a variable in an activity  
  
1.  Right\-click the applicable activity from your runbook to select **Properties**, and then click the **Details** tab to open the activities properties dialog box.  
  
2.  In a text box, to open a menu, right\-click to select **Subscribe**, and then click **Variable** to open the **Select a Variable** dialog box.  
  
3.  Select the variable name, and then click **OK**.  
  
    A placeholder `{variable}` is inserted next to the computer name in the **Computer** box.  
  
    When the activity runs, the placeholder is replaced with the value of the variable.  
  
### To organize variables  
  
1.  You can group variables into folders to organize them. To create a folder, right\-click the **Variables** folder to select **New**, and then click **Folder**.  
  
2.  To move a variable to a different folder, right\-click the variable, and then click **Move** to open the **Select a Folder** dialog box.  
  
3.  Select the destination folder, and then click **OK**. The variable is moved to the new folder location.  
  
## Special Variables  
You can specify special formats of variables to provide dynamic information to your runbooks. Specify the value of the variable to invoke this behavior.  
  
**NOW\(\)**: When the variable is resolved, it is set to the current date and time. You can pass arguments to this function to return specific portions of the date or time. For example, NOW\(hour\) returns the current hour. The following are the valid arguments for the NOW\(\) function: day, dayofweek, dayofyear, month, year, hour, minute, second, millisecond.  
  
**%ENVVAR%**: This variable returns the value of the environment variable between the percent \(%\) symbols. The environment variable is based on the runbook server computer where the runbook is running, and it is not case\-sensitive. All system variables can be resolved. Any user variables are resolved in the context of the service account on the runbook server. If the environment variable does not exist, the text specified within the variable is returned as\-is \(that is, if you type %ENVVAR% and no environment variable named ENVVAR exists, the text '%ENVVAR%' is returned\).  
  
## See Also  
[Data Manipulation](../../orch/manage/Data-Manipulation.md)  
  
