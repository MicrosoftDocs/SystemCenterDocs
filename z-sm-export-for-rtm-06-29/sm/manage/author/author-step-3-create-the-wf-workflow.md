---
title: Step 3: Create the WF Workflow
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1428abc-8b07-4a4e-8dc1-5f49d3eef021
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
# Step 3: Create the WF Workflow
In this step of the Woodgrove Bank customization scenario, Ken creates the workflow that supports the custom activity for change requests. To design the Windows Workflow Foundation \(WF\) workflow, Ken considers the following factors:  
  
-   **When should the workflow run?** The workflow should start when the applicable change request is approved.  
  
-   **What does the workflow need to do?** The workflow needs to add a computer to a group in Active Directory Domain Services \(AD DS\), and then change the status of the automated activity to "Complete."  
  
-   **What information does the workflow need?** The change request provides information about the specific computer and group to use. Properties of the workflow activities can retrieve the change request information from the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity that is associated with the change request.  
  
 To create and implement his new workflow, Ken follows the steps in the rest of this section. He uses the **Woodgrove.AutomatedActivity.AddComputerToGroupMP** management pack, as described in [Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack](../Topic/Step%201:%20Open%20the%20Woodgrove.AutomatedActivity.AddComputerToADGroupMP%20Management%20Pack.md). These procedures assume that this management pack is still open in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)].  
  
## Creating a New Workflow  
 Ken uses this procedure to create a workflow named **AddComputerToADGroupWF** in the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack.  
  
#### To create the new workflow  
  
1.  If the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] is not open, start the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)]: On your desktop, click **Start**, click **Service Manager Authoring Tool**, and wait for the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to open.  
  
2.  If the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack is not open, open it: On the **File** menu, point to **Open**, and then click **File**. In the **Open File** dialog box, click **Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml**, and then click **Open**.  
  
3.  In the **Management Pack Explorer**, right\-click **Workflows**, and then click **Create**.  
  
4.  On the **General** page of the Create Workflow Wizard, in the **Name** box, type **AddComputerToADGroupWF**, and then click **Next**.  
  
5.  On the **Trigger Condition** page, click **Run only when a database object meets specified conditions**, and then click **Next**.  
  
6.  On the **Trigger Criteria** page, under **Class name**, click **Browse**.  
  
7.  In the **Class Property** dialog box, click **Automated Activity: Add Computer To AD Group**, and then click **OK** to return to the **Trigger Criteria** page.  
  
8.  Under **Change event**, in the list, select **When an instance of the class is updated**, and then click **Additional Criteria**.  
  
9. In the **Pick additional criteria** dialog box, click the **Change To** tab, select the **Status** property of **Automated Activity: Add Computer To AD Group** class, and then click **Add**.  
  
10. Under **Criteria**, select **\[Activity\] Status** equals **In Progress**, and then, in the **Pick additional criteria** dialog box, click **OK**.  
  
11. On the **Trigger Criteria** page of the Create Workflow Wizard, click **Next**.  
  
12. On the **Summary** page, review the settings for the new workflow, and then click **Create**. After the wizard has completed, click **Close**.  
  
13. In the **Management Pack Explorer**, right\-click the management pack, and then click **Save**.  
  
 For general information about these steps, see [How to Create a New Workflow](../../../sm/manage/author/How-to-Create-a-New-Workflow.md) and [How to Save and Build a Workflow](../../../sm/manage/author/How-to-Save-and-Build-a-Workflow.md).  
  
## Adding the Workflow Activities  
 Ken uses this procedure to add the WF activities **Add AD DS Computer to Group** and **Set Activity Status to Completed** to his workflow.  
  
#### To add WF activities to the workflow  
  
1.  In the **Management Pack Explorer**, expand **Workflows**, right\-click **AddComputerToADGroupWF**, and then click **Edit**.  
  
2.  In the **Activities Toolbox** pane, locate the **Active Directory Activities** group.  
  
3.  Drag **Add AD DS Computer to Group** to the authoring pane, and drop it between the Workflow Start and End icons.  
  
4.  Drag **Set Activity Status to Completed**, and drop it between the previous activity and the End icon.  
  
 For general information about these steps, see [How to Add an Activity to a Workflow](../../../sm/manage/author/How-to-Add-an-Activity-to-a-Workflow.md).  
  
## Configuring the Activity Properties  
 Ken uses this procedure to set the **Computer Name** and **Group Name** properties of the **Add AD DS Computer to Group** activity to retrieve the values of the **Automated Activity: Add Computer To AD Group** properties **Computer Name**, **Group Name**, and **Activity ID** from the change request. In addition, he sets the **Computer Domain name** property of the **Add AD DS Computer to Group** activity to a constant value.  
  
#### To configure the activity properties  
  
1.  In the **Details** pane, click **Computer Name**, click the ellipsis button \(**...**\), click **Use a class property**, click **ComputerName**, and then click **OK**.  
  
2.  In the **Details** pane for the **Add AD DS Computer to Group** activity, click **Group Name**, click the ellipsis button \(**...**\), click **Use a class property**, click **GroupName**, and then click **OK**.  
  
3.  In the **Details** pane, click **Computer Domain name**, and in the text box, type **woodgrove.com**.  
  
4.  In the authoring pane, click the **Set Activity Status to Completed** activity.  
  
5.  Click **Activity ID**, and click the ellipsis button \(**…**\) that appears next to the property. On the left side of the dialog box, click **Use a class property**, and then, in the property list, click **ID \(Internal\)**. Click **OK**.  
  
6.  In the **Management Pack Explorer**, right\-click the management pack, and then click **Save**.  
  
 For general information about these steps, see [How to Set an Activity Property to Use a Value from the Trigger Class](../../../sm/manage/author/How-to-Set-an-Activity-Property-to-Use-a-Value-from-the-Trigger-Class.md) and [How to Set an Activity Property to a Constant Value](../../../sm/manage/author/How-to-Set-an-Activity-Property-to-a-Constant-Value.md).  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)