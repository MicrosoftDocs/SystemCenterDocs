---
title: High-Level Steps of the Woodgrove Bank Customization Scenario
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ead9979-d43b-489a-a793-fad3d8803bf6
 

















---
# High-Level Steps of the Woodgrove Bank Customization Scenario
The steps of the Woodgrove Bank customization scenario are as follows. Details about each of those steps are provided in subsequent topics. For background information about this scenario, see [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md).  
  
## Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack  
 Ken has to create a class that represents the new custom activity, and a matching form to use to access that new class. He starts by opening the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack that contains the definitions for the following class and form:  
  
-   The **Automated Activity: Add Computer To AD Group** custom class that represents the new automatic activity. This activity adds a new computer to a specified group in Active&nbsp;Directory Domain Services \(AD&nbsp;DS\).  
  
-   The form that represents the **Automated Activity: Add Computer To AD Group** class. Ken can use this form to enter information about the computer that is being added and the Active&nbsp;Directory group to which the computer should be added.  
  
 Instead of creating these necessary objects, you can import a pre\-defined management pack as part of the Woodgrove Bank customization scenario.  
  
 For more information about how to open the management pack, see [Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack](../Topic/Step%201:%20Open%20the%20Woodgrove.AutomatedActivity.AddComputerToADGroupMP%20Management%20Pack.md).  
  
## Step 2: Customize the Default Change Request Form  
 Often, customers want to adapt default forms to their organizations' preferences. In this scenario, Ken adds an image that represents the company logo to the default change request form and then rearranges the layout of the fields on the form.  
  
 For more information about how to customize the default change request form, see [Step 2: Customize the Default Change Request Form](../Topic/Step%202:%20Customize%20the%20Default%20Change%20Request%20Form.md).  
  
## Step 3: Create the WF Workflow  
 Ken creates the **AddComputerToADGroupRule** workflow that automatically adds the specified computer to the specified Active&nbsp;Directory group after the compliance change request is approved.  
  
 For more information about how to create the workflow rule and the Windows Workflow Foundation \(WF\) Workflow, see [Step 3: Create the WF Workflow](../Topic/Step%203:%20Create%20the%20WF%20Workflow.md).  
  
## Step 4: Move the Assembly Files to the Service Manager Console  
 Ken moves the workflow assembly file and the form assembly file to the Service Manager Program folder.  
  
 For more information about how to move the assembly files to the Service Manager console, see [Step 4: Move the Assembly Files to the Service Manager Console](../Topic/Step%204:%20Move%20the%20Assembly%20Files%20to%20the%20Service%20Manager%20Console.md).  
  
## Step 5: Bundle and Import the Custom Management Pack to Service Manager  
 Ken edits the custom management pack file to define the criteria that control when the workflow runs. Then, he has to bundle and import the custom management pack.  
  
 For more information about how to bundle and import the custom management pack into Service Manager, see [Step 5: Bundle and Import the Custom Management Pack to Service Manager](../Topic/Step%205:%20Bundle%20and%20Import%20the%20Custom%20Management%20Pack%20to%20Service%20Manager.md).  
  
## Step 6: Extend the Change Area Enumeration List  
 Ken adds the new **Compliance** list item that represents the new type of change request.  
  
 For more information about how to extend the change area enumeration list, see [Step 6: Extend the Change Area Enumeration List](../Topic/Step%206:%20Extend%20the%20Change%20Area%20Enumeration%20List.md).  
  
## Step 7: Create a New Task  
 Ken creates the **Start AD Users and Computers** task that starts the **AD Users and Computers** administration tool from the Service Manager console. Ken can conveniently monitor the Active Directory group to which the new computer is being added.  
  
 For more information about how to create a new task, see [Step 7: Create a New Task](../Topic/Step%207:%20Create%20a%20New%20Task.md).  
  
## Step 8: Create a New View  
 Ken creates the **Compliance Change Requests** view, which displays change requests of the new type. This includes all change requests in which **Area** \= **Compliance**.  
  
 For more information about how to create a new view, see [Step 8: Create a New View](../Topic/Step%208:%20Create%20a%20New%20View.md).  
  
## Step 9: Create a New Change Request Template  
 Create a new **Apply AppLocker Software Policy to Computer** change request template for the new compliance change request type.  
  
 For more information about how to create a new change request template, see [Step 9: Create a New Change Request Template](../Topic/Step%209:%20Create%20a%20New%20Change%20Request%20Template.md).  
  
## Step 10: Create a Notification Template and Subscription \(Optional\)  
 Ken creates the **Computer was added to AppLocker Policy Group** notification subscription that sends an email notification message to Ken when the status of an **Automated Activity: Add Computer To AD Group** activity is updated. This message notifies Ken that the workflow process is completed.  
  
 For more information about how to create a notification template and subscription \(optional\), see [Step 10: Create a Notification Template and Subscription \(Optional\)](../Topic/Step%2010:%20Create%20a%20Notification%20Template%20and%20Subscription%20\(Optional\).md).  
  
## Step 11: Use the New Compliance Change Request Process  
 To test the new process, Ken creates a new compliance change request to add the **ADComputer1** computer to the **GP\_AUTHAPPS** group. Next, he submits and approves the new change request. Finally, Ken verifies in AD&nbsp;DS that the new computer has been added to the appropriate Active Directory group.  
  
 For more information about how to use the new compliance change request process, see [Step 11: Use the New Compliance Change Request Process](../Topic/Step%2011:%20Use%20the%20New%20Compliance%20Change%20Request%20Process.md).  
  
> [!NOTE]  
>  The example companies, organizations, products, domain names, email addresses, logos, people, places, and events depicted herein are fictitious. No association with any real company, organization, product, domain name, email address, logo, person, place, or event is intended or should be inferred.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)
