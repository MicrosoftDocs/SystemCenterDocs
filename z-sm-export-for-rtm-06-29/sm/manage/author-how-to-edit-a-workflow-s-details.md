---
title: How to Edit a Workflow&#39;s Details
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3db924e-853c-49dd-a555-b4d237c4781d


















---
# How to Edit a Workflow&#39;s Details
Use this procedure to edit workflow details in the System Center 2016 - Service Manager Authoring Tool.  
  
### To edit workflow details  
  
1.  In the **Management Pack Explorer**, expand **Workflow**, right\-click the workflow, and then click **Details**. If you are already editing the workflow, right\-click the authoring pane background, and then click **Details**.  
  
2.  If you want to edit the workflow description, in the **Details** pane, click the **Description** box and type a new description, or click the ellipsis \(**...**\) button to open the **Workflow Properties** dialog box. Click the **Description** box, and then edit the description.  
  
3.  If you want to edit any of the other workflow details, in the **Details** pane, click any of the details, and then click the ellipsis \(**...**\) button to open the **Workflow Properties** dialog box. You can edit the following details:  
  
    -   **Name**: On the **General** tab, click **Name**, and then edit the workflow name.  
  
    -   **Retry and timeout limits**: On the **General** tab, click **Advanced**, and then edit the appropriate values.  
  
    -   **Trigger condition for a timer\-based workflow**: On the **Scheduler** tab, edit the appropriate values.  
  
    -   **Trigger condition for a query\-based workflow**: On the **Trigger** tab, edit the appropriate values.  
  
        > [!IMPORTANT]  
        >  If you change the trigger class of the workflow while the workflow is open in the authoring pane, any activity details that were set to use values from properties of the trigger class are cleared. The workflow does not run until you reset those activity details to use values from the new trigger class.  
  
    > [!IMPORTANT]  
    >  You cannot change the type of trigger that the workflow uses. For example, after you create a workflow that uses a timer trigger, you cannot change it to use a query trigger instead.  
  
## See Also  
 [Managing Workflows](../../../sm/manage/author/Managing-Workflows.md)
