---
title: "Run .Net Script | Microsoft Docs"
ms.custom: ""
ms.date: "07/25/2019"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad8a97f1-9c63-4824-890d-02af0021115b
caps.latest.revision: 29
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Run .Net Script
The Run .Net Script activity runs scripts written in VB.NET, JScript, C#, and Windows PowerShell. This activity is compatible with .NET CLR version 2.0 and later. Use the Run .Net Script activity to run scripts that parse data or run functions against available APIs.  

## Configuring the Run .Net Script Activity  
 Before you configure the Run .Net Script activity, you need to determine the following:  

- The code you want to run.  

- The libraries you want to use.  

- The data you want to publish.  

  Use the following information to configure the Run .Net Script activity.  

> [!NOTE]
>  You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Type**|Select the script language. Use the ellipsis **(...)** button to browse for the language.|  
|**Script**|Type the code that will run when the activity runs.|  

### Advanced Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Namespace**|Add a Namespace for each .NET namespace that will be used within your code. This allows you to call the code without using fully qualified names for each of the classes. Orchestrator recommends adding System namespace to every Run .Net Script activity.|  
|**References**|Add each of the Assembly (DLL) references that contain the libraries that you want to use. Add the **System.dll** located in the **Windows\Microsoft.NET\Framework\\<.NET Version>** directory.|  

###  <a name="BKMK_PublishedData"></a> Published Data  
 Add the published data items that you want this activity to publish. Every published data item that you add will be available on the Data bus. It is important to determine if a published data item will be multi-valued. The Run .Net Script activity automatically correlates multi-valued data from different items by aligning them. For example, if you choose to publish two items labeled “Name” and “Email” as Collections, the Run .Net script will try to line up each item in the Name collection with each item in the Email collection. If the collections are not equally sized, then the Run .Net Script activity will create blank values for the collection that has fewer items. For a list of data items and the corresponding description published by this activity, see the following Published Data table.  

### Published Data Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Name**|Enter the **Name** of the published data. This will be the name that appears when other activities subscribe to the data published by the Run .Net Script activity.|  
|**Type**|You can select **Date/Time**, **Integer**, or **String**. If the type you want is not available, select **String**. Use the **ToString** method of the activity to assign a value to this published data.|  
|**Collection**|If your data is multi-valued data, select **Collection**. When using a collection you must use the **Add** method to add items to the collection. If you are not using the collection you can use the assignment operator **(=)** to assign the value.|  
|**Variable name**|Use unique naming to make sure that your variable name does not collide with existing variables within your script or with classes and keywords available in .NET. We recommend prefixing variables with “OPD_”. For example, if you want to name your variable “myString”, you would name it “OPD_myString”.<br /><br /> The Run .Net Script activity will automatically create a .NET Property for this item. If this variable is a collection it will be created using a List\<T>, where T is the **Type** that you selected. If it is not a collection the property will be created using a **String**, **Integer**, or **Date/Time** based on the **Type** that you selected.|  

### Published Data  

|Item|Description|  
|----------|-----------------|  
|Standard Error|Any standard error output published by the Run .Net Script activity.|  
|Namespaces|The namespaces used.|  
|Standard Output|The standard output published by the Run .Net Script activity.|  
|References|The Assemblies used in the activity.|  
|Script Body|The script that was run.|  
|Script Language|The language that was selected for the script.|

## Execute 64-bit PowerShell cmdlets with Run .NET Script activity

You can run 64-bit Windows PowerShell in Orchestrator Run.Net Script activity. Use the following steps:

1.	Create a Run .Net Script activity from the **System activities group**.
2.	In **Details** > **Type**, select  **PowerShell** as the language.
3.	In  **Script**, enclose your PowerShell commands in the following code:  

    ```
    Invoke-Command -ScriptBlock {YOUR CODE} -ComputerName localhost

    ```

4.	Click **Finish**.

    ![.Net Script Activitiy](../standard-activities/media/run-net-script-activity/run-net-script.png)

5. To verify the PowerShell version, use the    following  script in .Net Script activity and publish the 64 bit and PowerShell version variable.

    ```

    $Result = Invoke-Command -ComputerName localhost {
    $Is64BitProcess = [Environment]::Is64BitProcess
    $PSVersion = $PSVersionTable.PSVersion
    RETURN $Is64BitProcess, $PSVersion
    }

    $64bit = $Result[0]
    $PSVersion = $Result[1]
    )
    ```

    ![.Net Script Activitiy](../standard-activities/media/run-net-script-activity/Run-net-script-ps-version.png)
