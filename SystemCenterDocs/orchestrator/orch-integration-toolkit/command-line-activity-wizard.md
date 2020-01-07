---
title: Orchestrator Integration Toolkit Command Line Activity Wizard
description: This article provides details about the Orchestrator Integration Toolkit Command Line Activity Wizard.
author: rayne-wiselman
manager: carmonm
ms.date: 02/02/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
ms.author: raynew
---

# Command Line Activity Wizard

The Command-Line Activity Wizard enables you to quickly create new activities in Orchestrator by encapsulating commands, arguments and parameters into a Microsoft .NET assembly (.DLL). The wizard automatically creates C# source code using the Orchestrator SDK and compiles it for you. Using this assembly, you can utilize the .NET Integration Pack (part of the Integration Toolkit) to test out your activities, and then use the Integration Pack Wizard to package the assembly into a custom Integration Pack that can be distributed and deployed just like other Integration Packs.  

 An assembly can contain one or more activities (commands), and the activities can be one or more of the available command types (Command, Command Line, PowerShell or SSH command). You define the activity name, command structure, input parameters and even published data (output).  

## Overview of Activities in Orchestrator  
 An activity is a single functional part of an Orchestrator runbook. Activities are what do the actual work within runbooks, and are joined together using links that can be defined with conditions to create workflow branches. When building a runbook using the Runbook Designer, you drag and drop activities from the Activities pane into the runbook, then link them together to form the workflow. As the runbook runs, it invokes each activity in sequence according to the way they were linked. Each activity performs a specific duty, and can collect input data from the Orchestrator data bus, and publish its output to the same data bus. Each activity has the ability to draw published data from any of the activities that ran prior to it in the runbook, and publishing output data allows following activities to access it.  

 Activities range from very simple to very complex. You can create an activity using the Command-Line Activity Wizard that does nothing but echoes text to an output property. You can also create a single activity that performs a complex, multi-step action such as virtual machine deployment. It’s up to you to define what each activity will do. However, your goal should be to define activities that encapsulate single sets of functionality that allow for easy re-use in many different types of situations. The key is flexibility. It’s better to create a set of ten different activities that each do something specific, and be able to use those activities in 20 different ways, rather than create 20 different activities to solve the specific individual scenarios. More information about best practices is covered later in this document.  

## Creating a New Activity Assembly  

#### To create a new command-line activity assembly  

1.  Click **Start > All Programs > Microsoft System Center 2012 > Orchestrator > Integration Toolkit > Orchestrator Command-Line Activity Wizard**  

2.  Click **Next**.  

3.  On the **Assembly Details** page, enter a value for **Name** that begins with a letter and is followed by zero or more alphanumeric characters. This name is used as a C# namespace identifier for the assembly and your activities.  

4.  In **Assembly file**, enter a path and filename of the assembly file that will be created by this wizard. If this file already exists, you will be prompted to overwrite the file.  

5.  Click the **Assembly information** button. You can enter information here that will become the properties of the assembly file, visible in Windows Explorer via file properties. The property values are defined in the table below. This information is optional and not required to build an assembly.  

    |||  
    |-|-|  
    |Property|Description|  
    |Title|Specifies a title for the assembly, which appears as the “File description” property in Windows Explorer properties|  
    |Description|Specifies an optional description for the assembly, which does not appear in Windows Explorer properties|  
    |Product|Specifies a product name for the assembly, which appears as the “Product name” property in Windows Explorer properties|  
    |Company|Specifies a company name for the assembly, which does not appear in Windows Explorer properties|  
    |Copyright|Specifies a copyright notice for the assembly, which appears as “Copyright” in Windows Explorer properties|  
    |Trademark|Specifies a trademark for the assembly, which appears as “Legal trademarks” in Windows Explorer properties|  
    |Version|Specifies the assembly version and file version. These appear in Windows Explorer properties as **File version** and **Product version**.<br /><br /> The version number has four parts, as follows:<br /><br /> <major version\>.<minor version\>.<build number\>.<revision\>|  

6.  Click **OK** when you are done entering assembly information.  

7.  Click **Next**. The **Commands** page displays.  

8.  Add one or more commands by following the instructions provided in [Adding Commands to an Assembly](command-line-activity-wizard.md#adding-commands-to-an-assembly).  

9. When you have completed the definition of your activity, click **OK**. The dialog closes and your new activity is added to the list on the **Commands** page. If you need to go back and edit a command, select the command in the list and click Edit. If you need to delete a command, select the command in the list and click **Remove**.  

10. When you are finished adding and modifying commands, click **Next**. The assembly file specified at the start of the wizard is compiled, and when the process is complete, the final wizard page displays.  

11. If you wish to immediately build an Integration Pack from this new assembly, click the **Build Integration Pack** button, which launches the Integration Pack Wizard and pre-loads the information from the assembly. Then, follow the instructions in [Creating a New Integration Pack](integration-pack-wizard.md#creating-a-new-integration-pack) to create the Integration Pack.  

12. If you wish to test your assembly using the Invoke .NET activity or just skip the IP build process for now, click **Finish**.  

## Adding commands to an assembly  

#### To add a command to an assembly  

1.  On the **Commands** page, you can define one or more commands (which become activities) which will be added to the assembly. To add a new command, click **Add**.  

2.  The **Add/Edit Command** dialog displays and contains three tabs: **General**, **Arguments** and **Published Data**. Enter a **Name** for the command. This becomes the name displayed in the Runbook Designer for the activity. You can optionally enter a **Description** for the command as well.  

3.  The **Mode** property selector contains four options: Run Command, Run Windows PowerShell, Run Program, and Run SSH Command. If you selected the **Run Program** mode, the **Program** field becomes active. Click the ellipsis button (...) and browse for the program that you want to run.  

    > [!NOTE]
    >  The program selected in a Run Program command will be invoked on the Runbook Server where the runbook containing this activity is being run. Therefore, this program must exist on all Runbook Servers where you expect to run the runbook.  

4.  Click the **Arguments** tab.  

5.  In the **Command Line** field, type the command or command line parameters needed by your activity. If your command will take parameters that you want users to specify, you will need to add them in the **Parameters** list below, and then use the **Insert** button to add them to the command line.  

    > [!IMPORTANT]
    >  If you specified **Run Windows PowerShell** for the **Mode** and you are referencing a PowerShell script included with your Integration Pack, you must precede the name of the script with dot and slash characters to refer to the local directory. For example, .\MyScript.ps1 would be specified for a script named MyScript.ps1. This is because the script file will be copied to the default directory for the Integration Pack. When Windows PowerShell runs a script from the local directory, it must specify this notation.  

6.  To provide parameters for a command line, click **Add**. The **Add/Edit Parameter** dialog appears.  

7.  In the Name field, type a name for the parameter that you are adding. This is the display name of the parameter shown in the Properties list of the activity.  

8.  From the Usage mode drop-down list, select the mode that you will use for the parameter. The Usage mode has two choices:  

    |Usage Mode|Description|  
    |----------------|-----------------|  
    |Command Argument|Select to use this argument as parameter within your command line (using the **Insert** button). For example, a command argument parameter named “Folder” could be placed in the command line like this:<br /><br /> `Dir $(folder)` **Note:**  If command line arguments contain spaces (such as folder names), you may need to enclose them in quotes for the command to work properly. For example: `Dir "$(folder)"`|  
    |Environment Variable|Select to use this argument as an environment variable that will be set before the command line is run. It can be used as a command line parameter or as an environment variable within a script that is run.<br /><br /> For example, an environment variable parameter named “Folder” could be placed in the command line like this:<br /><br /> `Dir %Folder%` **Important:**  The environment variable name already exists in either user or system environments, the command will fail with an error message similar to the following: **Item has already been added. Key in dictionary: 'folder'  Key being added: 'folder'** You can determine what environment variables exist on a local or remote computer by clicking **Start > Run**, then typing `MSINFO32.EXE`. Then select **Software Environment > Environment Variables**. To select another computer, press **<CTRL+R>**, select **Remote Computer on the Network** and enter the computer name, then click **OK**.|  

9. From the **Display style** drop-down list, select the style that you will use to display the parameter. The display style determines how the user will interact with the input when it is presented to them. The choices are described below:  

    |||  
    |-|-|  
    |Text|The user will be presented with a free-form text box for entering a value|  
    |Encrypted Text|The user will be presented with a masked text box. The data in this field will be encrypted within the database and will not be shown in any logs|  
    |True/False|The user can select True or False from a popup dialog|  
    |Text with Selection|The user can select from a group of **Options** that you specify|  
    |Date/Time|The user can select the value using a Date/Time Picker control|  
    |File|The user can select the value using a File Browser control|  
    |Folder|The user can select the value using a Folder Browser control|  
    |Computer|The user can select the value using a Computer Browser control|  

10. If the parameter requires or you wish to provide a default value, type it in the **Default value** field.  

11. If you selected **Text with Selection**, the **Options** field is enabled. To add option values that the user can select from, click the ellipsis button beside the **Options** field and enter them. Each option is listed on a separate line. When finished adding options, click **OK**.  

12. When you are finished with the parameter definition, click **OK**.  

13. If defined as a **Command Parameter**, the parameter can now be added to the command line by placing the cursor at the desired insertion point in the command line, then clicking the **Insert** button and selecting the parameter name. If defined as an **Environment Variable**, you must manually type in the variable (in the format **%variable%**) if you want it in the command line.  

14. If you chose the **Run Program** or **Run Command Line** modes, the checkbox for **Include working directory parameter** is enabled.  

15. Click the **Published Data** tab. Settings on this tab allow you to publish output data to the Orchestrator data bus so that other activities can use the information.  

16. To add a new published data property, click **Add**.  

17. If you selected the **Run Command**, **Run Program**, or **Run SSH Command** option from the **Mode** drop-down list on the **General** tab of the **Add/Edit Command** dialog, the following items appear on the **Add/Edit Published Data** dialog:  

    |||  
    |-|-|  
    |Name|The display name of the Published Data item that you are creating|  
    |Source|The source of the Published Data item. You can choose from **Standard Output Stream** or **Standard Error Stream** from the command line|  
    |Mode|The mode that you want to use to select the data published.<br /><br /> Use **Match Pattern** to determine if a given pattern is found within the Source.  This will return **True** or **False**.<br /><br /> Use **Extract Group** to retrieve each item of data that matches the Pattern that you specify|  
    |Pattern|The regular expression that applies to the Mode setting|  
    |Description|The description text that displays next to the published data property in the Runbook Designer. (optional)|  

18. If you selected the **Run Windows PowerShell** option from the **Mode** drop-down list on the **General** tab of the **Add/Edit Command** dialog, the following items appear on the **Add/Edit Published Data** dialog:  

    |||  
    |-|-|  
    |Name|The display name of the Published Data item that you are creating|  
    |Property|The name of the Windows PowerShell property that will be saved to the Published Data item. This property must be contained in an object output to the PowerShell pipeline during the script and must not be an object (should be able to be converted to a string).|  
    |Description|The description text that displays next to the published data property in the Runbook Designer. (optional)|  

19. Click **OK** to finish adding the Published Data item. Repeat steps 16-18 for each Published Data item you wish to add.  

20. Click **OK** to close the Add/Edit Command dialog and return to the Commands dialog.  

## Testing an Activity Assembly  
 After you have created an assembly, you can test it using the Invoke .NET activity (contained in the Integration Toolkit IP for .NET) to verify that it works as expected before converting it into a custom Integration Pack.  

#### To test and assembly  

1.  Open the Runbook Designer.  

2.  Create a new runbook.  

3.  In the **Activities** pane, click the **Integration Toolkit** category to expand it, and drag an **Invoke .NET** activity in to the new runbook.  

4.  Double-click the Invoke .NET object to view the **Properties** dialog.  

5.  In the **Assembly** field, browse for the assembly file that you created using the Command-Line Activity Wizard (or via custom development using the SDK) by clicking the ellipsis button (...) to the right of the field. Select the file, then click **Open**.  

6.  Click the ellipsis button to the right of the **Class** field to view a list of the individual commands in the assembly. Select a command class, and click **OK**. Parameters for this class appear on the **Properties** tab of the dialog.  

7.  The **Setup** field is used only by custom-developed classes using the Orchestrator SDK with the OrchestratorData attribute. For more information about the SDK, see [System Center Orchestrator Integration Toolkit SDK](https://msdn.microsoft.com/library/hh855054.aspx).  

8.  Click the **Properties** tab.  

9. Provide the information for each of the properties as necessary.  

10. Click **Finish** to save the settings and return to the runbook.  

11. Click **Runbook Tester** in the toolbar in the Runbook Designer. The Runbook Tester starts.  

12. Click **Run to Breakpoint** in the toolbar. The runbook starts and your activity runs. Results of the activity are shown in the **Run Log** pane.  

13. Click **Show Details** under the activity name in the Run Log pane to see the detailed results, including the input properties and published data.  

## QIK CLI Activity Migration  
 If you have an assembly that was created using the Opalis 6.3 QIK CLI Wizard, you will need to convert it to be compatible with Orchestrator before it can be used either in an Orchestrator Integration Pack or used directly in runbooks via the Invoke .NET activity. The conversion process is simple and only takes a few seconds per assembly.  

> [!IMPORTANT]
>  The install for the Orchestrator Integration Toolkit will not fail if Microsoft .NET Framework 3.5, Service Pack 1 is not installed, but different operations in the Command-Line Activity Wizard will fail if it is not present. Ensure that Microsoft .NET Framework 3.5, Service Pack 1 is installed before using the CLI.  

#### To convert an Opalis QIK CLI Assembly  

1.  Launch the Orchestrator Command-Line Activity Wizard by clicking Start > All Programs > Microsoft System Center 2012 > Orchestrator > Command-Line Activity Wizard  

2.  When the wizard loads, click the **Load existing assembly** button on the first page.  

3.  Select your existing assembly file and then click **Open**. The name and file location of the assembly is shown.  

4.  Modify the file path so that the changes will be saved to a new file. You can also change the name of the assembly if necessary.  

5.  If you need to make further changes to the assembly information details, click the **Assembly information** button and make those changes. Click **OK** when done to return to the Assembly Details page.  

6.  Click **Next** to go to the Commands page. You should see a list of commands that were previously defined in the assembly. Review the commands if necessary and click **Next** to continue to the **Building Assembly** page.  

7.  Your new assembly will be built for you and saved using the path and filename you defined previously.  

8.  You can now use your new Orchestrator-compatible assembly in runbooks with the Invoke .NET activity, or you can build an Integration Pack from this assembly by clicking the **Build Integration Pack** button. If you do not wish to build an IP at this time, click **Close** to end the wizard.  

## Orchestrator Resources  
 In addition to this online reference provided for System Center 2012 Orchestrator, there are a number of resources that can provide additional information on building runbooks, using the Integration Toolkit, and best practices.  

|||  
|-|-|  
|Resource|Location|  
|System Center Home|[https://www.microsoft.com/en-us/cloud-platform/system-center](https://www.microsoft.com/en-us/cloud-platform/system-center)|  
|System Center documentation|[https://docs.microsoft.com/system-center/](https://docs.microsoft.com/en-us/system-center/)|  
|Orchestrator Team Blog on TechNet|[https://blogs.technet.microsoft.com/orchestrator/](https://blogs.technet.microsoft.com/orchestrator/)|  
|Orchestrator Community Releases on CodePlex|[https://archive.codeplex.com/?p=orchestrator](https://archive.codeplex.com/?p=orchestrator)|  
|Orchestrator Community Forums on TechNet|[https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator](https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator)|
