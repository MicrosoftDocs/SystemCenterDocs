---
title: Woodgrove Bank customization sample scenario
description: Provides an overview and the steps needed to complete the Woodgrove Bank customization sample scenario for the Service Manager Authoring Tool.
manager: mkluck
ms.custom: na
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 03/27/2023
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea9bb90e-5a00-4346-b2a2-f6076c203778
ms.custom: engagement-fy23
---

# Woodgrove Bank customization sample scenario for the Service Manager Authoring Tool

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

To provide real-world context to the step-by-step procedures for the Service Manager Authoring Tool, we've created a fictitious scenario that takes place at a fictitious company, Woodgrove Bank.  

 The Woodgrove Bank customization scenario illustrates how Ken Myer, a server application developer for Woodgrove Bank, can easily extend the default change management process to support a new compliance change request process that the organization needs. The new compliance change request process will automatically add new computers to groups in Active Directory Domain Services (AD DS) so that the group software policies apply to the new computers.  

> [!NOTE]  
>  Some procedures in the Woodgrove Bank customization scenario rely on standard usage of the Service Manager console in Service Manager. This guide doesn't provide details for these common procedures.

 Although there are many steps in extending the change management process, Ken has to think about four main things, which are described in the following sections.  

## Create new custom activity  
 A standard change request consists of two activities: a default review activity and a default manual activity. In the new compliance change request process, Ken will perform the default review activity first, but the second activity is customized. Ken will create a new custom change request activity that uses a Windows Workflow Foundation (WF) workflow to automatically add a computer to an Active Directory group. Automating this change request process means that after the change is approved, the change will be completed without further user interaction. The custom activity is at the core of the new compliance change request process.  

## Create additional custom objects  
 Additionally, Ken will create new custom objects, such as a template, a queue, and a view, to support working with the new type of activity. If email notifications are configured in the environment, in the final steps of the scenario, Ken can configure email notifications to send confirmation email messages after the activity is complete.  

## Save custom objects in a management pack  
 Ken saves the custom objects to the Automated Activity: Add Computer to AD Group management pack so that he can transfer these objects between the Service Manager console and the Service Manager Authoring Tool.  

## Use the customized process  
 Eventually, after Ken imports the custom management pack into Service Manager and completes the creation of all the necessary custom objects, he can use the new process for compliance change requests. He creates a new compliance change request to add ADComputer1 computer to the GP_AUTHAPPS AD DS group. He can then monitor the process to confirm that the new computer is successfully added to the group.  

## Prerequisites for the customization scenario

The Woodgrove Bank customization scenario has the following prerequisites:  

- System Center - Service Manager must be installed in your environment.  
- The System Center - Service Manager Authoring Tool must be installed in your environment.  
- The Workflow Account in Service Manager must be a member of the Domain Administrators group because this scenario involves creating a workflow that adds a computer to a group in Active Directory Domain Services (AD DS). You specify the Workflow Account in the Service Manager Server Setup Wizard.  

The Authoring Tool's installation folder includes a **Samples** subfolder that contains the following files, which are required for the Woodgrove Bank customization scenario.  

|File|Description|  
|----------|-----------------|  
|Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml|A management pack that contains class definitions that are used in the Woodgrove Bank customization sample scenario.|  
|AddComputerToGroupFormAssembly.dll|The implementation of an automated activity form that is used in the Woodgrove Bank customization sample scenario.|  
|Woodgrovebank.jpg|An image that is used for form customization in the Woodgrove Bank customization sample scenario.|  
|New-mpbfile.ps1|A Windows PowerShell script that is used to bundle a management pack with its associated resource files into an .mpb file that can then be imported into Service Manager. Resource files can include items such as images and forms.|  

## Step 1 - Open the management pack

The primary goal of the Woodgrove Bank customization scenario is to create a new custom activity that triggers a Windows Workflow Foundation (WF) workflow that automatically adds a computer to a group in Active Directory Domain Services (AD DS).  

 To create this new activity, in this step of the scenario, Ken must extend the Service Manager class library by adding a new activity class that is derived from the base **Activity** class. This custom class includes all the properties of the base activity class and two new properties—**ComputerName** and **GroupName**. These new properties identify the computer you're adding and the Active Directory group to which you're adding the computer. Ken also needs to define the **System.AddComputerForm** form that will represent the new **Automated Activity: Add Computer to AD Group** activity.  

 The necessary class activity and its associated form are already defined in the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack. Therefore, to start the Woodgrove Bank customization scenario, Ken opens the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack in the Service Manager Authoring Tool. Then, Ken explores the **Automated Activity: Add Computer to AD Group** class in the **Class Browser** pane.  

 Ken uses the Authoring Tool to complete the following procedure to open the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack that defines the **Automated Activity: Add Computer to AD Group** activity and its associated form.  

### Open the management pack  

1.  Start the Authoring Tool.  
2.  Select **File**, point to **Open**, and select **File**.  
3.  In the **Open File** dialog, select the **Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml** file to open the management pack.  

### Explore the "Automated Activity: Add Computer to AD Group" class  

1.  In the Authoring Tool, if the **Class Browser** isn't visible, select **View**, and select **Class Browser**.  
2.  Locate and expand the **Automated Activity: Add Computer to AD Group** class, and then view the class properties, such as **ComputerName** and **GroupName**.  

## Step 2 - Customize the default change request form

The second step in the Woodgrove Bank customization scenario is to customize the default Change Request form, which is Microsoft.EnterpriseManagement.ServiceManager.ChangeManagement.Forms.ChangeRequestForm. Ken wants to rearrange some fields on the form and then add the Woodgrove Bank logo. Before Ken starts, he views the fields in the form to see how the values change according to the properties that are selected.  

 Next, Ken opens the **ServiceManager.ChangeManagement.Library.mp** management pack file in the Service Manager Authoring Tool, he customizes the form, and then saves the management pack file. Later, he must import the customized management pack into the Service Manager console.  

### View the System.AddComputerForm form  

1.  In the Authoring Tool, expand **Forms** in the **Management Pack Explorer** pane. Select and hold the **System.AddComputerForm** form, and select **Customize** to open the form in the authoring pane.  
2.  In the authoring pane, ensure that the **Details** pane is visible. If it isn't visible, select **View**, and select **Details Window**.  
3.  Select a field on the form. Note that the properties in the **Details** pane are updated according to the class property that is bound to the field that you selected. Note the **Binding Path** entry in the **Details** pane. This entry indicates the property that the field in the form represents.  

### Customize the default Change Request form  

1.  In the Authoring Tool, select **File**, point to **Open**, and select **File**. In the **Open File** dialog, locate the **ServiceManager.ChangeManagement.Library.mp** management pack. For example, the path to the management pack might be as follows:  
     D:\Program Files (x86)\Microsoft System Center\Service Manager  Authoring\Library\ServiceManager.ChangeManagement.Library.mp.  
     Select the management pack, and select **Open**.  
2.  In the **Management Pack Explorer**, select the **Service Manager Change Management Library (sealed)** management pack, and then expand **Forms**. Right-click the form that ends with **ChangeRequestForm**, and select **Customize**.  
3.  In the **Target Management Pack** dialog, select the **WoodGrove Automated Activity - Add Computer To AD Group** management pack, and select **OK**.  
     A new form item now appears in the **Automated Activity - Add Computer To AD Group** management pack. The name of the new form is **Microsoft.EnterpriseManagement.ServiceManager.ChangeManagement.Forms.ChangeRequestForm (Customized)**.  
4.  Right-click the new form item, and select **Customize** to open it in the authoring pane.  
5.  In the authoring pane, customize the look of the form by dragging fields and rearranging their location on the form.  
6.  Select **View**, and select **Form Customization Toolbox**.  
7.  Drag the **Image** icon from the **Form Customization Toolbox** to the form.  
8.  In the **Insert Image** dialog, specify the path of the **Woodgrovebank.jpg** file.  
9. Select **File**, and select **Save All** to save the custom management pack.  

## Step 3 - Create the WF workflow

In this step of the Woodgrove Bank customization scenario, Ken creates the workflow that supports the custom activity for change requests. To design the Windows Workflow Foundation (WF) workflow, Ken considers the following factors:  

- **When should the workflow run?** The workflow should start when the applicable change request is approved.  
- **What does the workflow need to do?** The workflow needs to add a computer to a group in Active Directory Domain Services (AD DS), and then change the status of the automated activity to **Complete**.  
- **What information does the workflow need?** The change request provides information about the specific computer and group to use. Properties of the workflow activities can retrieve the change request information from the Service Manager activity that is associated with the change request.  

  To create and implement his new workflow, Ken follows the steps in the rest of this section. He uses the **Woodgrove.AutomatedActivity.AddComputerToGroupMP** management pack, as described in [Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack](). These procedures assume that this management pack is still open in the Service Manager Authoring Tool.  

### Create a New Workflow  
 Ken uses this procedure to create a workflow named **AddComputerToADGroupWF** in the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack.  

#### To create the new workflow  

1.  If the Authoring Tool isn't open, start the Authoring Tool: On your desktop, select **Start**, select **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  
2.  If the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack isn't open, open it: On the **File** menu, point to **Open**, and select **File**. In the **Open File** dialog, select **Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml**, and select **Open**.  
3.  In the **Management Pack Explorer**, select and hold **Workflows**, and select **Create**.  
4.  On the **General** page of the Create Workflow Wizard, in the **Name** box, enter **AddComputerToADGroupWF**, and select **Next**.  
5.  On the **Trigger Condition** page, select **Run only when a database object meets specified conditions**, and select **Next**.  
6.  On the **Trigger Criteria** page, under **Class name**, select **Browse**.  
7.  In the **Class Property** dialog, select **Automated Activity: Add Computer To AD Group**, and select **OK** to return to the **Trigger Criteria** page.  
8.  Under **Change event**, in the list, select **When an instance of the class is updated**, and select **Additional Criteria**.  
9. In the **Pick additional criteria** dialog, select the **Change To** tab, select the **Status** property of **Automated Activity: Add Computer To AD Group** class, and select **Add**.  
10. Under **Criteria**, select **[Activity] Status** equals **In Progress**, and then, in the **Pick additional criteria** dialog, select **OK**.  
11. On the **Trigger Criteria** page of the Create Workflow Wizard, select **Next**.  
12. On the **Summary** page, review the settings for the new workflow, and select **Create**. After the wizard has completed, select **Close**.  
13. In the **Management Pack Explorer**, right-click the management pack, and select **Save**.  

For general information about these steps, see [How to Create a New Workflow](manage-workflows-auth-tool.md) and [How to Save and Build a Workflow](manage-workflows-auth-tool.md).  

### Add the Workflow Activities  
Ken uses this procedure to add the WF activities **Add AD DS Computer to Group** and **Set Activity Status to Completed** to his workflow.  

#### Add WF activities to the workflow  

1.  In the **Management Pack Explorer**, expand **Workflows**, select and hold **AddComputerToADGroupWF**, and select **Edit**.  
2.  In the **Activities Toolbox** pane, locate the **Active Directory Activities** group.  
3.  Drag **Add AD DS Computer to Group** to the authoring pane, and drop it between the Workflow Start and End icons.  
4.  Drag **Set Activity Status to Completed**, and drop it between the previous activity and the End icon.  
For general information about these steps, see [How to Add an Activity to a Workflow](add-workflow-activities.md).  

### Configure the Activity Properties  

Ken uses this procedure to set the **Computer Name** and **Group Name** properties of the **Add AD DS Computer to Group** activity to retrieve the values of the **Automated Activity: Add Computer To AD Group** properties **Computer Name**, **Group Name**, and **Activity ID** from the change request. In addition, he sets the **Computer Domain name** property of the **Add AD DS Computer to Group** activity to a constant value.  

#### Configure the activity properties  

1.  In the **Details** pane, select **Computer Name**, select the ellipsis button (**...**), select **Use a class property**, select **ComputerName**, and select **OK**.  
2.  In the **Details** pane for the **Add AD DS Computer to Group** activity, select **Group Name**, select the ellipsis button (**...**), select **Use a class property**, select **GroupName**, and select **OK**.  
3.  In the **Details** pane, select **Computer Domain name**, and in the text box, enter **woodgrove.com**.  
4.  In the authoring pane, select the **Set Activity Status to Completed** activity.  
5.  Select **Activity ID**, and select the ellipsis button (**...**) that appears next to the property. On the left side of the dialog, select **Use a class property**, and then, in the property list, select **ID (Internal)**. Select **OK**.  
6.  In the **Management Pack Explorer**, right-click the management pack, and select **Save**.  

For general information about these steps, see [How to Set an Activity Property to Use a Value from the Trigger Class](configure-activities-information.md) and [How to Set an Activity Property to a Constant Value](configure-activities-information.md).  

## Step 4 - Move the assembly files to the Service Manager console

In this step of the Woodgrove Bank customization scenario, in System Center - Service Manager Ken must move the workflow assembly file and the form assembly file to the Service Manager program directory to use the workflow with the Service Manager console.  

For general information about deploying a workflow to Service Manager, see [How to Deploy a Workflow to Service Manager](deploy-workflow.md).  

### Move the assembly files  

1.  In Windows Explorer, open the folder in which you saved the management pack, and copy the **AddComputerToADGroupWF.dll** and **AddComputerToGroupFormAssembly.dll** files.  
2.  Open the Service Manager installation folder (for example, C:\Program Files\Microsoft System Center\Service Manager), and paste the copied files in that folder.  

## Step 5 - Bundle and import the custom management pack to Service Manager

In this step of the Woodgrove Bank customization scenario, Ken needs to bundle the management pack file with all the necessary resource files and then import the bundled file into Service Manager. When Service Manager imports a management pack, it validates the XML code in the management pack file and then imports the management pack only if it's valid.  

### Bundle the management pack file with its associated resource files  

1.  Ensure that the Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml file and its associated resource files, such as the Woodgrovebank.jpg image file and the AddComputerToGroupFormAssembly.dll file, are in the same folder. For example, put all the files in the AuthoringSample folder.  
2.  Copy the folder that contains the files to the Service Manager management server.  
3.  Bundle the files using the Windows PowerShell cmdlet [New\-SCSMManagementPackBundle](/previous-versions/system-center/powershell/system-center-2012-r2/hh316263(v=sc.20)). For example:  

    ```  
    New-SCSMManagementPackBundle -Name AddComputerToGroup.mpb -ManagementPack Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml   
    ```  

### Import the management pack into Service Manager  

1.  In the Service Manager console, select **Administration**.  
2.  In the **Administration** pane, expand **Administration**, and select **Management Packs**.  
3.  In the **Tasks** pane, under **Management Packs**, select **Import Management Pack**.  
4.  In the **Select Management Packs to Import** dialog, select **AddComputerToGroup.mpb**.  
5.  In the **Import Management Packs** dialog, select **Add**, select **Import**, and select **OK**.  

## Step 6 - Extend the change area enumeration list

In this step of the Woodgrove Bank customization scenario, Ken extends the **Change Area Enumeration** list by adding a new **Compliance** list item that represents the new change request type.  

The following procedure provides only high-level steps for creating a new list item in the Service Manager console. For the complete procedure for creating a new list item, see [How to Add a List Item](group-queue-lists.md).  

### Create a new list item  

1.  In the Service Manager console, select **Change Area Enumeration** as the list to edit.  
2.  Specify **Compliance** as the new value to add to this list.  

## Step 7 - Create a new task

When Ken works with a compliance change request, he needs to easily access the Active Directory Users and Computers administrative tool.  

 In this step of the Woodgrove Bank customization scenario, to make it easy to access the tool, Ken creates a new task, **Start Active Directory Users and Computers**. He saves this task to the **Woodgrove Automated Activity - Add Computer To Group** management pack. He can later use the new task to start the tool.  

 The following procedure provides only the high-level steps for creating a new task in the Service Manager console. For the complete procedure for creating a new task, see [How to Create a Task](troubleshoot-with-tasks.md).  

### Create a new task  

1.  In the Service Manager console, specify the task name: **Start Active Directory Users and Computers**.  
2.  Specify the target class: **Change Request**.  
3.  Specify the management pack in which to save this customization: **Service Manager Change Management Configuration Library**.  
4.  Specify the display category for the task: **Change Management Folder Tasks**.  
5.  Specify the command: **%systemroot%\system32\mmc.exe**.  
6.  Clear the **Show output when this task is run** checkbox.  

## Step 8 - Create a new view

To continue with the customizations in the Woodgrove Bank scenario, in this step, Ken creates the **Compliance Change Requests** view that will display only change requests of the **Compliance** type. Ken saves the new view to the **Service Manager Change Management Configuration Library** management pack. Users can monitor these change requests in the Service Manager console.  

### Create a new view  

1.  In the Service Manager console, select **Work Items**.  
2.  In the **Work Items** pane, expand **Change Management**.  
3.  In the **Tasks** pane, select **Create View**.  
4.  In the **General** section of the **Create View** dialog, enter **Compliance Change Requests** in the **Name** box.  
5.  Select the **Criteria** section.  
6.  Next to the **Search for objects of a specific class** list, select **Browse**.  
7.  In the **Select a Class** dialog, under **Name**, select **Change Request**. In the **Available Properties** list, select **Area**, and select **Add**.  
8.  At the end of the **Criteria** section, in the **Criteria** definition area, select the **Area** criterion, and in the empty box, set the value to **Compliance**. When the criterion is complete, it resembles **[Change Request] Area equals Compliance**.  
9. Select **Display**, and in the **Columns to display** list, select **Status**, **Classification Category**, and **Description**. Then, select **OK**.  

## Step 9 - Create a new change request template

In this step of the Woodgrove Bank customization scenario, Ken creates a template for the new compliance change request type; the template is named **Apply AppLocker Software Policy to Computer**. The new template helps ensure consistency among all the change requests of this type, and it helps ensure the correct workflow behavior.  

 The following procedure provides only the high-level steps for creating a new template in the Service Manager console. For the complete procedure for creating a new template, see [How to Create Change Request Templates](./change-activity-mgt.md).  

### Create a new template  

1.  In the Service Manager console, specify the following as the name of the template: **Apply AppLocker Software Policy to Computer**.  
2.  Set the class to **Change Request**.  
3.  Set the management pack to **WoodGrove Automated Activity: Add Computer to AD Group**.  
4.  When the change request form is displayed, note the customizations in the form, such as the image that was previously added and the new layout of the fields.  
5.  On the **General** tab on the form, set **Area** to **Compliance**.  
6.  On the **Activities** tab, add a review activity named **Review and Approve Adding Computer to Group**, and then set the reviewer to an appropriate user.  
7.  Add the new activity **Automated Activity: Add Computer AD Group**.  
8.  Set **Group** to **GP_AUTHAPPS**.  
9. Save the template.  

## Step 10 - Optionally create a notification template and subscription

If System Center - Service Manager is configured with a Simple Mail Transfer Protocol (SMTP) server, as part of the Woodgrove Bank customization scenario, Ken can configure an email notification that will be sent to him when a new computer is added to the compliance group. This is an optional step.  

The following procedure provides only the high-level steps for creating the **Computer Added to AppLocker Policy Notification Template** email notification template and subscription in the Service Manager console. For the complete procedure for creating a notification template, see [How to Create Notification Templates](./notifications.md).  

### Create an email notification template and subscription  

1.  In the Service Manager console, create a new notification email template. In the **Administration** pane, select **Notifications**, and select **Templates**. In the **Tasks** pane, select **Create E-mail Template**, and then complete the Create E-Mail Notification Template Wizard.  
2.  On the **General** page, specify the **Name** to be **AppLocker Policy Notification Template**, and specify the **Class** as **Automated Activity: Add Computer to AD Group**. Specify **Management pack** to be **Woodgrove Automated Activity - Add Computer To Group**.  
3.  On the **Template Design** page, in the **Subject** box, enter **Computer**, and select **Insert**. In the **Property Picker** dialog, select **ComputerName**. Add the following text to the **Subject** box: **was added to the AppLocker Policy Group**. Add any text in the **MessageBody** box, and save the template.  
4.  In the **Administration** pane, select **Notifications**, and select **Subscriptions**. In the **Tasks** pane, select **Create Subscription**, and then complete the Create E-Mail Notification Subscription Wizard.  
5.  In the **Name** box, enter **Computer Added to AppLocker Policy Notification**.  
6.  In the **Class** box, enter **Automated Activity: Add Computer to AD Group**.  
7.  Specify **Notification condition** to be **When an object of the selected type is updated**.  
8.  Specify **Management pack** to be **Woodgrove Automated Activity - Add Computer To Group**.  
9. On the **Additional Criteria** page, add criteria in which **Status** equals **Completed**.  
10. On the **Template** page, specify **E-mail template** to be the previously created template, **Computer added to AppLocker Policy Notification**.  
11. On the **Recipient**  page, add recipients from your organization.  

## Step 11 - Use the new compliance change request process

In this final step of the Woodgrove Bank customization scenario for System Center - Service Manager, Ken tests the new change request process and uses all its related customized objects. Ken creates a compliance change request to add the new ADComputer1 computer to the GP_AUTHAPPS group in Active Directory Domain Services (AD DS). Ken follows the process in the Service Manager console as it changes status while progressing from the first activity to the next.  

### Create a compliance change request  

1.  Start the Active Directory Users and Groups tool by using the **Start Active Directory Users and Computers** task. Ensure that it doesn't contain the **ADComputer1** computer that you're about to add.  
2.  In the Service Manager console, select **Work Items**, and then in the **Work Items** pane, expand **Change Management**.  
3.  In the **Tasks** pane, select **Create Change Request**, and then select **Apply AppLocker Software Policy to Computer**. In the Change Request form, note the icon that was previously added.  
4.  On the **General** tab, in the **Name** box, enter **New Compliance Change Request**, and then set **Area** to **Compliance**.  
5.  Select the **Activities** tab, and in the **Process activities** area, open the **Add Computer to Group** activity.  
6.  On the **Activity Form** page, in the **Computer name** box, enter **ADComputer1**. Select **OK** on the **Activity** form, and select **OK** on the **Change** form.  
7.  In the **Change Management** pane, expand **Change Management**, and select **Compliance Change Requests**. Wait approximately 10 to 20 seconds until the new change request appears in the **Compliance Change Requests View** pane. (You might have to refresh the view).  
8.  Use the **Start AD Users and Computers** task to start the Active Directory Users and Computers tool. In the tool, create the **GP_AUTHAPPS** group. (In the previous steps in the scenario, you configured the change request process to add computers to this group.) When the state of the change request changes to **In Progress**, open it, select the **Review Activity: Approve Change Request** activity, and approve it. Then, select **Submit and Close**.  
9. Wait approximately 5 to 10 seconds, and notice that the status of the activity changed to **Completed**. Also, notice that the status of the next activity has changed to **In Progress**, which means that the second activity has started to run. The activity rule has been triggered, and the custom workflow has started.  
     To check the status of the **AddComputerToADGroupWF** workflow, select **Administration**. In the **Administration** pane, expand **Workflows**, and then select **Status**. In the **Status** pane, select **AddComputerToADGroupWF**.  
10. Use the **Start AD Users and Computers** task to start the Active Directory Users and Computers tool, and notice that the **GP_AUTHAPPS** Active Directory group now contains the new **ADComputer1** computer. At this point, any policies that are configured to be applied to computers in this Active Directory group apply to the computer that was added.  
     Notice that the status of the automated activity has now also changed to **Completed** due to the last step in the **AddComputerToADGroupWF** workflow.  
11. Start Microsoft Outlook and locate the email notification that was sent to the process manager about the new computer that was added to the Active Directory group.  


## Next steps

- [Customize a column title in a view for the authoring views sample scenario](customize-column-title.md).