---
title: Computer Groups
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e085a23-5fae-4592-a08c-55cefb2a2926
author: cfreemanwa
ms.author: raynew
ms.date: 10/12/2016
manager: carmonm
---
# Computer Groups

System Center 2016 - Orchestrator is designed to interact with all of your data center systems. Computer groups let you target selected activities against a set of similar computer systems instead of a single computer. By configuring the activities in your runbook to use a computer group, you have the flexibility to add computers dynamically by adding them to the computer group.  

You can create computer groups by using Active Directory queries, and you can manage the list of computers in a group outside of Orchestrator. For example, if you have a computer group that is created from an Active Directory query that retrieves all instances of Microsoft SQL Server, when an instance of SQL Server is added to your Active Directory system, it is automatically included in that group.  

## Managing Computer Groups  
To use computer groups in your activities, create a computer group, and then add computers to it.  

You can also organize your computer groups into folders. Use the following steps to create a new folder.  

#### To create a folder  

1.  In the **Connections** pane in the Runbook Designer, click the **Computer Groups** folder or a subfolder.  

2.  Right-click to select **New**, and then click **Folder**.  

Use the following procedure to add a computer group. To add computers by using an Active Directory query or a System Center 2016 Configuration Manager collection, use the Active Directory Integration Pack or the Integration Pack for System Center 2016 Configuration Manager.  

#### To add a computer group  

1.  In the **Connections** pane, right-click the **Computer Groups** folder or a subfolder.  

2.  Select **New**, and then click **Computer Group** to open the **New Computer Group** dialog box.  

3.  In the **New Computer Group** dialog box, on the **General** tab, in the **Name** and **Description** boxes, type a name and description of the computer group.  

4.  Click the **Contents** tab. The list displays all the computer entries that make up this computer group.  

5.  Click **Add** to open the **Add Computer to Computer Group** dialog box.  

6.  Enter the name of the computer that you are adding, or click the ellipsis **\(...\)** button next to the **Computer** box, and then select the applicable computer. Click **OK** to add the computer.  

7.  To add more computers to the group, repeat the previous two steps.  

#### To modify settings  

1.  To modify the settings of an entry you added, click the entry on the **Contents** tab, and then click **Modify**.  

2.  To remove an entry on the **Contents** tab, click the entry, and then click **Remove**.  

## Using a Computer Group in an Activity  
Any standard activity that requires you to identify a **Computer** name in the **Configuration Properties** dialog box, such as the **Send Event Log Message** activity, can use a computer group. Other activities can use the **Computer Group** where you define a remote system or computer.  

Use the following procedure to use a computer group.  

#### To use a computer group  

1.  Right-click the applicable activity from your runbook, select **Properties** on the menu, and then select the **Details** tab to open the **Activities Properties** dialog box.  

2.  In the **Computer** box, right-click to open a menu, select **Subscribe**, and then select **Computer Group** to open the **Select Computer Group** dialog box.  

3.  Select the computer group, and then click **OK**.  

    A placeholder `{computer group name}` is inserted next to the computer name in the **Computer** box.  

    When the activity runs, it runs on each computer in the group.  

## See Also  
[Data Manipulation](../orch/manage/data-manipulation.md)  
