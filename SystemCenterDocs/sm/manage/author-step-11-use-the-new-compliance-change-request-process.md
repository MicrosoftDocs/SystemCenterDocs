---
title: Step 11 - Use the New Compliance Change Request Process
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09ee5ec3-4d9f-4b5f-b4c4-4a63f52cf794
---

# Step 11 - Use the New Compliance Change Request Process

>Applies To: System Center 2016 - Service Manager

In this final step of the Woodgrove Bank customization scenario for System Center - Service Manager, Ken tests the new change request process and uses all its related customized objects. Ken creates a compliance change request to add the new ADComputer1 computer to the GP\_AUTHAPPS group in Active&nbsp;Directory Domain Services \(AD&nbsp;DS\). Ken follows the process in the Service Manager console as it changes status while progressing from the first activity to the next.  

### To create a compliance change request  

1.  Start the Active Directory Users and Groups tool by using the **Start Active Directory Users and Computers** task. Note that it does not contain the **ADComputer1** computer that you are about to add.  

2.  In the Service Manager console, click **Work Items**, and then in the **Work Items** pane, expand **Change Management**.  

3.  In the **Tasks** pane, click **Create Change Request**, and then select **Apply AppLocker Software Policy to Computer**. In the Change Request form, note the icon that was previously added.  

4.  On the **General** tab, in the **Name** box, type **New Compliance Change Request**, and then set **Area** to **Compliance**.  

5.  Click the **Activities** tab, and in the **Process activities** area, open the **Add Computer to Group** activity.  

6.  On the **Activity Form** page, in the **Computer name** box, type **ADComputer1**. Click **OK** on the **Activity** form, and then click **OK** on the **Change** form.  

7.  In the **Change Management** pane, expand **Change Management**, and then click **Compliance Change Requests**. Wait approximately 10 to 20 seconds until the new change request appears in the **Compliance Change Requests View** pane. \(You might have to refresh the view\).  

8.  Use the **Start AD Users and Computers** task to start the Active Directory Users and Computers tool. In the tool, create the **GP\_AUTHAPPS** group. \(In the previous steps in the scenario, you configured the change request process to add computers to this group.\) When the state of the change request changes to **In Progress**, open it, select the **Review Activity: Approve Change Request** activity, and approve it. Then, click **Submit and Close**.  

9. Wait approximately 5 to 10 seconds, and notice that the status of the activity changed to **Completed**. Also, notice that the status of the next activity has changed to **In Progress**, which means that the second activity has started to run. The activity rule has been triggered, and the custom workflow has started.  

     To check the status of the **AddComputerToADGroupWF** workflow, select **Administration**. In the **Administration** pane, expand **Workflows**, and then select **Status**. In the **Status** pane, click **AddComputerToADGroupWF**.  

10. Use the **Start AD Users and Computers** task to start the Active Directory Users and Computers tool, and notice that the **GP\_AUTHAPPS** Active&nbsp;Directory group now contains the new **ADComputer1** computer. At this point, any policies that are configured to be applied to computers in this Active&nbsp;Directory group apply to the computer that was added.  

     Notice that the status of the automated activity has now also changed to **Completed**, due to the last step in the **AddComputerToADGroupWF** workflow.  

11. Start Microsoft Outlook and locate the email notification that was sent to the process manager about the new computer that was added to the Active&nbsp;Directory group.  
