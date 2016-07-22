---
title: Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b107f28-932b-4dce-85b6-b5b6bb083f7e


















---
# Step 1: Open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP Management Pack
The primary goal of the Woodgrove Bank customization scenario is to create a new custom activity that triggers a Windows Workflow Foundation \(WF\) workflow that automatically adds a computer to a group in Active&nbsp;Directory Domain Services \(AD&nbsp;DS\).  
  
 To create this new activity, in this step of the scenario Ken must extend the System Center 2012 - Service Manager class library by adding a new activity class that is derived from the base **Activity** class. This custom class includes all of the properties of the base activity class and two new properties, **ComputerName** and **GroupName**. These new properties identify the computer you are adding and the Active&nbsp;Directory group to which you are adding the computer. Ken also needs to define the **System.AddComputerForm** form that will represent the new **Automated Activity: Add Computer to AD Group** activity.  
  
 The necessary class activity and its associated form are already defined in the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack. Therefore, to start the Woodgrove Bank customization scenario, Ken opens the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack in the System Center 2016 - Service Manager Authoring Tool. Then, Ken explores the **Automated Activity: Add Computer to AD Group** class in the **Class Browser** pane.  
  
 Ken uses the Authoring Tool to complete the following procedure to open the **Woodgrove.AutomatedActivity.AddComputerToADGroupMP** management pack that defines the **Automated Activity: Add Computer to AD Group** activity and its associated form.  
  
### To open the Woodgrove.AutomatedActivity.AddComputerToADGroupMP management pack  
  
1.  Start the Authoring Tool.  
  
2.  Click **File**, point to **Open**, and then click **File**.  
  
3.  In the **Open File** dialog box, click the **Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml** file to open the management pack.  
  
### To explore the "Automated Activity: Add Computer to AD Group" class  
  
1.  In the Authoring Tool, if the **Class Browser** is not visible, click **View**, and then click **Class Browser**.  
  
2.  Locate and expand the **Automated Activity: Add Computer to AD Group** class, and then view the class properties, such as **ComputerName** and **GroupName**.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)
