---
title: How to Set an Activity Property to Use a Value from the Trigger Class
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c712a56-66f4-4b8d-91ba-dcf4107e1ee9


















---
# How to Set an Activity Property to Use a Value from the Trigger Class
Use this procedure in the System Center 2016 - Service Manager Authoring Tool to set a property to retrieve its value from the Service Manager class used to trigger the workflow. You cannot use this method with a workflow that has a Timer trigger.  
  
 In the Woodgrove Bank customization scenario, Ken uses this procedure to set the **Computer Name** and **Group Name** properties of the **Add AD DS Computer to Group** activity to retrieve the values of the **Automated Activity: Add Computer To AD Group** properties **Computer Name**, **Group Name**, and **Activity ID** from the change request.  
  
### To configure activity properties to retrieve data from a trigger class  
  
1.  In the authoring pane, click the activity you want. The **Details** pane becomes active and displays the properties for this activity. For example, click the **Add AD DS Computer to Group** activity or the **Set Activity Status to Completed** activity.  
  
2.  In the **Details** pane, click the property you want to set, and then click the ellipsis \(**...**\) button that appears next to the property.  
  
     For example, for the **Add AD DS Computer to Group** activity, click **Group Name**, and then click the ellipsis \(**...**\) button.  
  
3.  On the left side of the **Define input for the activity addADDSComputerToGroup1** dialog box, click **Use a class property**. Selecting this option produces a list of the properties that are available in the trigger class.  
  
4.  Select the class property that you want to use for this activity property.  
  
     For example, for the **Add AD DS Computer to Group** activity, do the following:  
  
    1.  In the **Details** pane for the **Add AD DS Computer to Group** activity, click **Group Name**, click the ellipsis \(**...**\) button, click **Use a class property**, click **GroupName**, and then click **OK**.  
  
    2.  In the **Details** pane, click **Computer Name**, click the ellipsis \(**...**\) button, click **Use a class property**, click **ComputerName**, and then click **OK**.  
  
     For the **Set Activity Status to Completed** activity, click **Activity ID**, and then click the ellipsis \(**...**\) button that appears next to the property. In the **Define input for the activity setActivityStatusToCompleted1** dialog box, click **Use a class property**, and then in the property list, click **ID \(Internal\)**. Click **OK**.  
  
## See Also  
 [Step 3: Create the WF Workflow](../Topic/Step%203:%20Create%20the%20WF%20Workflow.md)   
 [Configuring the Way Activities Manage and Pass Information](../../../sm/manage/author/Configuring-the-Way-Activities-Manage-and-Pass-Information.md)
