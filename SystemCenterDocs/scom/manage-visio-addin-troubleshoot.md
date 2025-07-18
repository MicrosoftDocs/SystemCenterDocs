---
title: Troubleshooting the Visio Add-in
description: This article provides information to help troubleshoot common issues with the Visio add-in for Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: troubleshooting-general
ms.assetid: c9dabbc3-0ac5-46fe-8a34-b82b67c0e6ad
---

# Troubleshooting the Visio Add-in



The following sections provide information about troubleshooting the Visio Add-in:  

-   Enabling trace logging on the data provider  

-   Known issues  

## Enable trace logging for the server data module

Use the following steps to enable trace logging for the server data module installed on the SharePoint server.  

1.  Open the Microsoft.Office.Visio.Server.OperationsManager.dll configuration file in a text editor (such as Notepad).  

2.  Change the location for log files. Look for the following:  

    ```  
    <configuration>  
       <appSettings>  
          <add key="EnableLog" value="True" />  
          <add key="LogPath" value=\\server\directory" />  
       <appSettings>  
    </configuration>  
    ```  

    For the LogPath parameter, change the value to the location where you want to save log files generated by the data provider.  

3.  Copy the configuration file to the directory on the GAC where the data module assembly is located.  

The next time a diagram is refreshed, the configuration file is checked and log files are written to the location you specific.  

Each refresh option is recorded in a separate log file. The name of the file reflects the user who attempted the refresh and the date and time the refresh was attempted (for example, "jdoe_3_25_2010_12-23-37_PM.log"). The log file contains the following:  

-   The name of the user that requested the refresh  

-   The date and time of the refresh  

-   The version of the assembly installed on the server  

-   The command string that was configured in the diagram before publishing to the server  

-   Details about the dataset to be refreshed, including table count, row count, and IDs for each row  

-   Any error conditions or exceptions that occur within the data module for each session  

For successful refresh attempts, the log file also contains the XML version of the dataset returned to Visio Services for diagram refresh purposes.  

## Known issues with the Visio Add-in  

You might see the following issues when you use the Visio Add-in for System Center 2016 - Operations Manager.  

### The font size of inserted shapes might appear too small  

When you insert a new graphic by using the **Insert Shape** option, the font size for the shape text might appear too small. The size is determined by the default font size set for a template.  

You can change the font size by selecting the shape and then choosing a different font size in the Visio toolbar.  

### Hyperlinks on subshapes aren't available  

Health Explorer and Alert View hyperlinks might not be available in Edit mode or Full Screen mode if you've grouped your shapes or added links to any shapes that were already contained within groups.  

### You receive a ConfigurationErrorsException error message  
You might see the following error message:  

```  
System.Configuration.ConfigurationErrorsException: Configuration system failed to initialize --->   
System.Configuration.ConfigurationErrorsException: Unrecognized configuration section userSettings.   
   (C:\Documents and Settings\asttest\Local Settings\Application Data\Microsoft_Corporation  
   \OpsMgrAddin.vsto_vstoloca_Path_logwdvddmizljsrbc2bvt5gtm5juzdix\12.0.6325.5000\user.config        
   line 3)  
.  
.  
.  
```  

To work around this problem, delete the configuration file identified at the top of the error message. For example, delete the following file:  

\OpsMgrAddin.vsto_vstoloca_Path_logwdvddmizljsrbc2bvt5gtm5juzdix\12.0.6325.5000\\user.config  

### You receive a MissingMethodException error message

You might see the following error message:  

```  
System.MissingMethodException: Method not found: 'System.Security.SecureString System.Windows.Controls.PasswordBox.get_SecurePassword()'.  
   at Microsoft.EnterpriseManagement.VisioAddin.EnterCredentials.get_Password()  
   at Microsoft.EnterpriseManagement.VisioAddin.SCOMHelpers.EnterCredentials(ManagementGroupConnectionSettings& connectSettings)  
   at Microsoft.EnterpriseManagement.VisioAddin.Document.ConnectToManagementGroup()  
   at Microsoft.EnterpriseManagement.VisioAddin.Document.AddDataLinkToShape()  

```  

To resolve this problem, install [Microsoft .NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22), available from https://www.microsoft.com/download/details.aspx?id=22.  

### The state graphic isn't displayed  

The state graphic doesn't appear on a stencil even though you've linked the shape with the **Link Shape to Data** option.  

Some stencils in Visio aren't defined with a wrapping group. To resolve this problem, create a group for the shape, and then use the **Link Shape to Data** option again. To create a group, right-click the shape, and select **Shape** and **Group**.  

### You see security warnings when you open a diagram  
When you open a document that you previously linked to Operations Manager, you receive multiple security warnings.  

This problem occurs because the status of the document components is set to refresh automatically. To suppress the warnings, select **Don't show this message again**.  

### You can't reinstall the Visio Add-in  
If you delete the Operations Manager Visio Add-in by using the Visio Trust Center, you can't add it again later.  

This behavior occurs by design in Visio. Before you can add the Operations Manager Visio Add-in again, uninstall it by using Add/Remove Programs (or Programs and Features) in the Control Panel, and then reinstall it.  
