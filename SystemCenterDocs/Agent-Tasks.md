---
title: Agent Tasks
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6269883-c45e-4102-a2ba-fa19739e06c7
---
# Agent Tasks
*Agent tasks* in [!INCLUDE[om12long]./Token/om12long_md.md)] are run on the agent computer where the target object is managed. An agent task can be a script or an executable program run from a command line. If an executable program is used, the application must be installed on the agent computer.

Agent tasks are useful for performing actions on the agent computer or for retrieving information for the user. They provide the following capabilities:

-   Run a script or command locally on the agent computer without logging on to the computer interactively.

-   Run a script or command on multiple agents with a single action.

-   Run a script or command by using local user credentials with permissions not available to the user.

**Agent Task**

![/Image/AuthGuide_22_TaskAgent.gif)

## Credentials
Tasks run under the credentials of the Default Action Account on the agent computer. This account typically has sufficient privileges for accessing most application components, even if the user running the task does not have these user rights. If the task is required to perform an action requiring other credentials, such as accessing an external data source, then you can specify credentials when you run the task.

## Output
Any output sent to the standard out stream \(StdOut\) from the script or command is provided to the user as Task Output in the Operations Console. Command line programs will typically output information to this stream. Scripts should output information by using commands such as WScript.Echo to provide this information.

## Create Agent Task Wizard Options
When you run the **Create Agent Task** wizard, you have to provide values for the options in the following tables. Each table represents a single page in the wizard.

### General Properties
The following options are available on the **General Options** page of the wizard.

|Option|Description|
|----------|---------------|
|Task Name|The name used for the task. This name is displayed in the **Actions** pane in the Operations console.|
|Description|Optional description of the task.|
|Task target|Target class of the task. The task will be displayed in the **Actions** pane when an instance of the target class is selected. Properties from the target object are available to use in the parameter of the task<br /><br />You do not specify a target for Alert and Event command line tasks. They are available to all alerts and events regardless of the class that created them.|

### Command Line
The following options are available on the **Command Line** page of the wizard. This page is only available for a command line agent task.

|Option|Description|
|----------|---------------|
|Application|Path and name of the application to run.|
|Parameters|Parameters to add to the command line. This can be a combination of static text and variables for the properties of the target class or one of its parent classes.<br /><br />If a variable used for a parameter could resolve to text containing a space, you should enclose the variable in quotations \(""\). If there are no quotations and the text includes a space, then it will be seen as multiple parameters.|
|Working directory|The default directory to use when the application is run.|
|Timeout|The number of seconds that the application is allowed to run. If it has not completed within this time, the application will be ended and an error returned.|

### UNIX\/Linux Shell Command
The following options are available on the Shell Command Details page of the wizard. This page is only available for an **UNIX\/Linux Shell Command** agent task.

|Option|Description|
|----------|---------------|
|Command|The shell command to execute. This can be the full path to a program or script, a command, or a one\-line sequence of multiple commands \(using pipeline operators\).|
|Run As Profile|Either the **UNIX\/Linux Action Account** or **UNIX\/Linux Privileged Account** profile. Select the profile that associates the required account credentials with the task target. The associated account will be used to execute the command.|
|Timeout \(seconds\)|The number of seconds that the command can run before the agent stops it. This prevents problem commands from running continuously and putting excess overhead on the agent computer.|

### Script
The following options are available on the **Script** page of the wizard. This page is only available for a script agent task.

|Option|Description|
|----------|---------------|
|File Name|Name of the script. Must end in a .vbs or .js extension depending on whether your script is written in VBScript or JScript.|
|Timeout|The number of seconds that the script can run before the agent stops it. This prevents problem scripts from running continuously and putting excess overhead on the agent computer.|
|Script|The body of the script.|
|Parameters|Click to provide values for any arguments in the script. For more information, see [Script Arguments](./Script-Monitors-and-Rules.md#ScriptArguments).|

## Creating Agent Tasks

### Command Line Agent Tasks
*Command line agent tasks* run a command line application or batch file using a target class. They are listed in the **Actions** pane of the Operations console when an instance of the target class is selected. You can specify the path to the application and the working directory. This application must be installed on the agent computer when the task is run. You can also use $Target variables from the target class or one of its parents to be included on the command line. Any output from the application sent to the console are delivered back to the user in the **Task Status** dialog box in the Operations console when the task is run.

The following procedure creates a console task to run the **netstat** utility to list the ports that the agent computer is listening on.

##### To create a command line agent task

1.  Select the **Authoring** workspace.

2.  In the Authoring pane, expand **Management Pack Objects**.

3.  Right click **Tasks** and select **Create a New Task** to open the **Create Task Wizard**.

4.  On the **Task Type** page, do the following:

    1.  Under **Agent Tasks**, select **Command line**.

    2.  In the **Select destination management pack** dropdown, select the management pack file to store the task. For more information about management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

    3.  Click **Next**.

5.  On the **General Properties** page, do the following:

    1.  Under **Task Name**, type **Netstat**. This is the text that will be displayed in the **Actions** pane.

    2.  Click the Select button to open the **Select Items to Target** dialog box.

    3.  Select **Windows Computer** and click **OK**.

    4.  Click **Next**.

6.  On the **Command Line** page, do the following:

    1.  In the **Application** box, type **%windir%\\system32\\netstat.exe**.

    2.  Click **Create**.

### UNIX\/Linux Shell Command Agent Tasks
*UNIX\/Linux Shell Command* tasks run a command line application or script using a target class. They are listed in the **Actions** pane of the Operations console when an instance of the target class is selected. You can specify the path to a script or command, a command to run, or a one\-line sequence of multiple commands \(using pipeline operators\). Any output from the application sent to the console are delivered back to the user in the **Task Status** dialog box in the Operations console when the task is run.

The following procedure creates a console task to run the **netstat** utility to list the ports that the agent computer is listening on.

##### To create an UNIX\/Linux Shell Command agent task

1.  Select the **Authoring** workspace.

2.  In the Authoring pane, expand **Management Pack Objects**.

3.  Right click **Tasks** and select **Create a New Task** to open the **Create Task Wizard**.

4.  On the **Task Type** page, do the following:

    1.  Under **Agent Tasks**, select **Run an UNIX\/Linux Shell Command**.

    2.  In the **Select destination management pack** dropdown, select the management pack file to store the task. For more information about management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

    3.  Click **Next**.

5.  On the **General Properties** page, do the following:

    1.  Under **Task Name**, type **Netstat**. This is the text that will be displayed in the **Actions** pane.

    2.  Click the Select button to open the **Select Items to Target** dialog box.

    3.  Select **UNIX\/Linux Computer** and click **OK**.

    4.  Click **Next**.

6.  On the **Shell Command Details** page, do the following:

    1.  In the **Command** box, type **netstat**.

    2.  Select the **Run As profile** to use.

    3.  Input the task timeout in seconds.

    4.  Click **Create**.

### Script Agent Tasks
*Script agent tasks* run a Windows script using a target class. They are listed in the **Actions** pane of the Operations console when an instance of the target class is selected. The script can perform some action or it can collect information that is delivered back to the user in the **Task Status** dialog box. To return information to the user, you can use any script command that will display information on the command line. For VBScript, this will typically be the **WScript.Echo** command.

The following procedure creates an agent script task to reboot the target computer. It accepts two parameters. The first is the name of the computer that it retrieves from the **Principal Name** property of the target. The second is a flag that specifies that the reboot should be performed. This value defaults to **false**, and the user must change it to **true** when they run the task or the reboot will not be performed. This provides an additional safety to the task to prevent an operator from accidentally performing a reboot.

##### To create a command line agent task

1.  Select the **Authoring** workspace.

2.  In the Authoring pane, expand **Management Pack Objects**.

3.  Right click **Tasks** and select **Create a New Task** to open the **Create Task Wizard**.

4.  On the **Task Type** page, do the following:

    1.  Under **Agent Tasks**, select **Run a script**.

    2.  In the **Select destination management pack** dropdown, select the management pack file to store the task. For more information about management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

    3.  Click **Next**.

5.  On the **General Properties** page, do the following:

    1.  Under **Task Name**, type **Reboot Computer**. This is the text that will be displayed in the **Actions** pane.

    2.  Click the Select button to open the **Select Items to Target** dialog box.

    3.  Select **Windows Computer** and click **OK**.

    4.  Click **Next**.

6.  On the **Script** page, do the following:

    1.  In the **File Name** box, type **RebootComputer.vbs**.

    2.  Leave the default of 1 minute for the **Timeout**.

    3.  Copy the following script and past into the **Script** box.

        ```vbs
        sComputer = WScript.Arguments(0)
        bConfirmFlag = cbool(WScript.Arguments(1))

        Set colOS = GetObject("winmgmts:{impersonationLevel=impersonate,(Shutdown)}//" & sComputer).ExecQuery("select * from Win32_OperatingSystem where Primary=true")

        If bConfirmFlag Then
            For each objOS in colOS
        objOS.Reboot()
            Next
        Else
        WScript.Echo "Confirm flag set to false. Computer will not be rebooted."
        End If

        ```

    4.  Click **Parameters** to open the **Parameters** dialog box.

    5.  Click Target and then select **Principal Name**.

    6.  Type a space after the computer name variable and then type **false**. The final parameter line should look similar to the following:

        **$Target\/Property\[Type\="MicrosoftWindowsLibrary7585000\!Microsoft.Windows.Computer"\]\/PrincipalName$ false**

    7.  Click **OK**.

    8.  Click **Create**.

## See Also
[Tasks](./Tasks.md)
[Console Tasks](./Console-Tasks.md)



