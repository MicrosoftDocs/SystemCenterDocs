---
title: How to Create a New Workflow
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65d851f2-a784-47de-89b5-fbde64325bf9
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
# How to Create a New Workflow
Use the Create Workflow Wizard to create a new workflow in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)]. After you create the workflow, you can populate the workflow with activities, as described in [Adding or Removing Workflow Activities](../../../sm/manage/author/Adding-or-Removing-Workflow-Activities.md).  
  
> [!IMPORTANT]  
>  All workflows run under the security context of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Workflow account.  
  
 The following procedures guide you through the process of creating a new workflow:  
  
-   If you want to create a workflow that runs according to a schedule or a fixed time interval, use the procedure "To create a new workflow triggered by a timer or schedule."  
  
-   If you want to create a workflow that runs in response to a change in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, use the procedure "To create a new workflow triggered by a database change." In the Woodgrove Bank customization scenario, Ken uses this procedure to create a workflow named **AddComputertoADGroupWF**.  
  
> [!IMPORTANT]  
>  After you have completed the wizard, you cannot change the type of trigger that the workflow uses. For example, after you create a workflow that uses a timer trigger, you cannot change it to use a database trigger instead.  
  
### To create a new workflow triggered by a timer or schedule  
  
1.  In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], open the management pack where you want to store this workflow.  
  
2.  In the **Management Pack Explorer**, right\-click **Workflows**, and then click **Create**.  
  
3.  On the **General** page of the Create Workflow Wizard, enter a name for the workflow. The name must include only alphanumeric or underscore characters, have 50 or fewer characters, and start with an alphabetical or underscore character, and it cannot have spaces. For example, enter **AddComputerToADGroupWF**.  
  
4.  If you want to add a description of the workflow, type it in the **Description** box. Note that, although there is no limit on the length of this text, some views \(such as the list of the workflow's properties on the **Summary** page of the wizard\) might only display the first 200 characters.  
  
5.  If you want to change the default values for the workflow retry interval and the maximum time to run, on the **General** page, click **Advanced**. In the **Advanced** dialog box, set new values for **Interval** and for **Maximum time to run the workflow**, and then click **OK**. Note that the value for the maximum time to run must be more than 60 seconds, but less than 24 hours.  
  
6.  On the **Trigger Condition** page, if you want the trigger to run at a specific time or at a specific interval, use the default setting **Timer**, and then click **Next**.  
  
7.  On the **Trigger Criteria** page, configure the interval at which to run the workflow \(either **Weekly** or **Other Interval**\):  
  
    1.  To set the workflow to run on specific days of the week, click **Weekly**. Use the **Start time** dial control to set a start time for the rule. To set the hour, minutes, or 00:00\-24:00 values, click the value, and then click the up arrow or down arrow. Then, select the check boxes for each day that you want the rule to run.  
  
        > [!NOTE]  
        >  The time that you set is the time on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] server that runs the workflow, not the local time on the server that runs the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
         \-or\-  
  
         To set the workflow to repeat after a specific time, click **Other Interval**. In the **Frequency** box, enter an integer value, and then select the type of interval \(**Days**, **Hours**, **Minutes**, or **Seconds**\).  
  
    2.  After you have set the interval for the workflow, click **Next**.  
  
8.  On the **Summary** page, review the settings for the new workflow, and then click **Create**. After the wizard is completed, click **Close**.  
  
### To create a new workflow triggered by a database change  
  
1.  In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], open the management pack where you want to store this workflow.  
  
2.  In the **Management Pack Explorer**, right\-click **Workflows**, and then click **Create**.  
  
3.  On the **General** page of the **Create Workflow** wizard, enter a name for the workflow. The name must include only alphanumeric or underscore characters, have 50 or fewer characters, and start with an alphabetical or underscore character, and it cannot have spaces. For example, enter **AddComputerToADGroupWF**.  
  
4.  If you want to add a description of the workflow, type it in the **Description** box. Note that, although there is no limit on the length of this text, some views \(such as the list of the workflow's properties on the **Summary** page of the wizard\) might only display the first 200 characters.  
  
5.  If you want to change the default values for the workflow retry interval and the maximum time to run, on the **General** page, click **Advanced**. In the **Advanced Workflow Limits** dialog box, set new values for these options, and then click **OK**. Note that the value for the maximum time to run must be more than 60 seconds, but less than 24 hours.  
  
6.  On the **Trigger Condition** page, click **Run only when a database object meets specified conditions**, and then click **Next**.  
  
7.  On the **Trigger Criteria** page, to select a **Class name**, click **Browse**. In the **Class Property** dialog box, select the class of object with which the workflow will interact, and then click **OK**. For example, select **Automated Activity: Add Computer To AD Group**.  
  
8.  To select a **Change event**, click the drop\-down list, select one of the options, and then click **Next**. For example, click the drop\-down list, and then click **When an instance of the class is updated**.  
  
9. Optionally, under **Add Criteria to this trigger**, click **Additional Criteria** to set advanced criteria, such as when the activity status changes from **Pending** to **In Progress**.  
  
10. On the **Summary** page, review the settings for the new workflow, and then click **Create**. After the wizard is completed, click **Close**.  
  
## See Also  
 [Step 3: Create the WF Workflow](../Topic/Step%203:%20Create%20the%20WF%20Workflow.md)   
 [Managing Workflows](../../../sm/manage/author/Managing-Workflows.md)