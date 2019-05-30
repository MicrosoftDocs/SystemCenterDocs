---
title: Orchestrator Integration Toolkit Integration Pack Wizard
description: This article provides details about the Orchestrator Integration Toolkit Command Line Activity Wizard.
author: rayne-wiselman
manager: carmonm
ms.date: 02/02/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
ms.author: raynew
---

# Integration Pack Wizard

The Integration Pack Wizard (IP Wizard) allows you to create a new Integration Pack from an existing assembly created by the Command-Line Activity Wizard or created via the Orchestrator SDK. The IP Wizard packages the assemblies, dependent files, and required metadata into an .OIP file that can be deployed via the Orchestrator Deployment Manager. With the IP Wizard, you can create professional-looking Integration Packs with full branding and custom icons, or simply package up command-line activities so they can be more easily deployed.  

## Deciding when to create an integration pack  
 When creating custom activities for use in Orchestrator, it’s important to decide when it’s appropriate to use activities individually with the Toolkit’s .NET Integration Pack activities, and when it’s appropriate to create and deploy an Integration Pack.  

 When you only have one or a few activities, or when you’re in the development phase and creating many changes in an activity, you should just use the assemblies with the Toolkit IP activities to test the operation of those activities. Packaging, registering, deploying, uninstalling, and upgrading Integration Packs incurs a lot of overhead in the process of development that may not be needed or wanted. Additionally, because deploying an IP involves installing a Windows Installer file and making changes to the database, doing this frequently can cause unexpected results, so it’s recommended that you use a virtual machine and revert it frequently to ensure a clean test environment.  

 If you have a group of activities to test, or you’re further along in the development cycle and want to test the entire end-to-end process of installation, upgrade, uninstallation, and using finished activities, then creating an Integration Pack is the right path to choose. The Integration Pack provides a more user-friendly experience, including activities that appear in the Activities pane of the Runbook Designer, and a complete installation experience. Integration Packs also allow for deployment of the activities to multiple Runbook Servers or Runbook Designers across the organization, or to external customers.  

## Creating a new integration pack  
 The Integration Pack Wizard allows you to create Integration Packs from existing Orchestrator-compatible assemblies and dependent files. If you have not yet created an Orchestrator-compatible assembly, see the [Command Line Activity Wizard](command-line-activity-wizard.md#creating-a-new-activity-assembly).  

 Note: The Integration Toolkit no longer includes the binaries for the Windows Installer XML (WiX) Toolset, used by the IP Wizard for creating the Windows Installer files within Integration Packs. This set of tools is now a prerequisite installation, required prior to installing the Toolkit. However, if WiX is subsequently uninstalled, the Integration Pack wizard will display an error message directing you to download and install WiX. The Integration Toolkit supports version 3.5 of the WiX Toolset. The WiX Toolset can be downloaded from http://wix.codeplex.com.  

#### To create a new integration pack  

1. Start the Integration Pack Wizard. Click **Start > All Programs > Microsoft System Center 2012 > Orchestrator > Integration Toolkit > Orchestrator Integration Pack Wizard**. The welcome page displays.  

2. If you have an existing Integration Pack that you want to update, click **Import Integration Pack**. See [Updating an Existing Integration Pack](integration-pack-wizard.md#updating-an-existing-integration-pack) for more information about that process. To create a new Integration Pack, click Next.  

   > [!IMPORTANT]
   >  If you want to upgrade an existing IP, you must click **Import Integration Pack**. If you click **Next**, the IP you create will have a new unique product ID and new unique IDs for all activities, even if you re-use a previous assembly and use the same product and filenames.  

3. On the **Product Details** page, enter or modify the information as needed to customize the information about your Integration Pack. The table below describes the fields and their descriptions:  


   |                |                                                                                                                                                                                                                                                                                                                                                                                                        |
   |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |   Field Name   |                                                                                                                                                                                              Description                                                                                                                                                                                               |
   |  Product name  |                                                                                                                                                                         The name of the IP that displays in Deployment Manager                                                                                                                                                                         |
   | Category name  |                                                                                                                                                   The text that displays as the category title for the IP in the Activities pane of Runbook Designer                                                                                                                                                   |
   |    Company     |                                                                                                                                                    The name of your company. This information is displayed in Add/Remove Programs under “Publisher”                                                                                                                                                    |
   |   EULA file    |                                                                                                            An RTF-formatted text file with a file name extension of .EULA. Displayed to the user during registration using Deployment Manager, and requires acceptance before registration.                                                                                                            |
   | Resource file  |                                                                                 An assembly containing icons and other resources, used to provide the category and activity icons. By default, the standard Toolkit resource file is used (Microsoft.SystemCenter.Orchestrator.Integration.Toolkit.Wizard.Images.dll)                                                                                  |
   |    Version     |                                                                                                                                The version number of the Integration Pack which will be displayed in Deployment Manager and used to determine if the IP is an upgrade.                                                                                                                                 |
   | Enable upgrade | If you imported an existing Integration Pack, this check box is selected by default, enabling this Integration Pack to upgrade an existing installed version. If you clear this check box, new product and activity IDs will be created for the IP and it will not upgrade an existing version. If you want to enable side-by-side installation of multiple versions of your IP, clear this check box. |
   |  Description   |                                                                                                                                                                            A detailed description of your Integration Pack                                                                                                                                                                             |
   | Category Icon  |                                                                                                                           The default category icon is displayed. If you wish to choose another icon, click the **Modify** button and select a new icon, then click **OK**.                                                                                                                            |


4. When you are done entering product information, click **Next**. The Activities page is displayed. The Activities page is where you will reference the assembly or assemblies that contain the activities you’ve defined using the Command-Line Activity Wizard or created using the Orchestrator SDK.  

5. To add a new activity to the IP, click **Add**.  

6. To open and add the assembly file, click the ellipsis **(…)** button to the right of **Library**. Browse to the desired assembly file, select it, and click **Open**. The file name and path are displayed in the Library field.  

7. To select an activity from the assembly, click the **Class** drop-down arrow and select the appropriate activity name from the list. The name and description defined in the activity are shown in the **Display Name** and **Description** fields.  

8. If desired, modify the display name and description of the activity.  

9. The default activity icon is displayed for the activity. If a different icon is desired, click **Modify** and select another icon from the browser, then click **OK**.  

10. Click **OK** to save the activity definition. The activity name and description now appear in the Activities list.  

11. Continue adding activities to the list as needed. When you are finished adding activities, click **Next**. The Dependencies and Included Files page displays.  

12. On this page, you can define a list of additional files that you want packaged with your Integration Pack. These files could be additional assemblies required by your activities, scripts, documentation, or other files you want deployed to Runbook Servers and Runbook Designers along with your activities. Click **Add** and then select the file(s) you need and then click **OK** to add files to the list.  

13. When you are done adding files to the list, click **Next**. The Orchestrator Integration Pack File page displays.  

14. In the textbox provided, enter the path and filename of the Integration Pack to be created. If you enter a filename that already exists, it will be overwritten. Ensure that you have sufficient access to write to the path specified or the process will fail. If no path is specified, the OIP file will be created in the Documents folder (C:\users\\<your username\>\Documents). Click **Next** to start building the IP.  

    > [!IMPORTANT]
    >  The characters in the filename must be valid for the language that is installed on your operating system.  

    > [!IMPORTANT]
    >  Specify a name for the Integration Pack that is not common to ensure that it does not match the name of another Integration Pack. Orchestrator cannot install two Integration Packs with the same name.  

15. When the IP has been successfully built, the final page of the wizard will display the path and filename of the new OIP file. Click Finish to exit the wizard. If there was an error, you can click **Back** and correct any information as necessary and then retry the build process.  

    For information on deploying your Integration Pack, see the article, [How to add an Integration Pack](../how-to-add-an-integration-pack.md).  

## Updating an existing integration pack  
 The Orchestrator Integration Pack Wizard allows you to import an existing Integration Pack so that you can make changes and repackage it as a new version. If you want to ensure that changes to an existing IP are an upgrade to the IP and not creating a new Integration Pack, you need to ensure that you import the existing IP into the Integration Pack Wizard and also ensure that the “Enable Upgrade” checkbox is checked. Failing to do either of these things will cause the IP to be created with a new product ID and new activity IDs, which will create a side-by-side installation of the new version, instead of replacing or upgrading the previous installed version.  

 This process of creating and upgrading an IP is not recommended during initial product development when you are still developing activities and changes are constant. Instead, it is better to utilize the activities in the Integration Toolkit’s .NET Integration Pack for testing the activities outside of an IP. For more information, see [Deciding When to Create an Integration Pack](integration-pack-wizard.md#deciding-when-to-create-an-integration-pack).  

### Helpful IP Upgrade Tips  

#### Updating underlying assemblies  
 When you create an Integration Pack, metadata about the IP is stored in the package so that it can be read by the wizard during subsequent upgrades. When you update certain items such as activities or the underlying assemblies for those activities, you need to rebuild the IP. However, if you modify the activity settings and select a new assembly file, it will reset the fields on the Activity Information page, requiring you to re-enter the information.  

 If you are modifying the underlying assembly of one or more activities in an IP, perhaps to add parameters or change Published Data, but you don’t wish to change any of the other settings relative to the IP, simply save your new assembly to the same path and filename as the previous assembly (which is shown in the Library field of the Activity Information dialog). Then just import the existing IP into the wizard and run through the process of creating the IP without modifying any of the activity information.  

## QIK Integration Pack Migration  
 If you created an Integration Pack using the Opalis QIK Wizard, you will need to convert it to be compatible with Orchestrator before it can be imported and used by Orchestrator.  

 Prior to converting an IP, the following steps must be completed:  

-   If the activities in your IP were created using the QIK CLI Wizard and you have not already converted them to be compatible with Orchestrator, you must follow the steps outlined in QIK CLI Activity Migration before continuing. If you do not have a separate copy of the assembly containing the activities, you will need to install the IP to an Opalis 6.3 server first and then locate the assembly in the following directory: “C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions\Support\Quick Integration Kit 3”.  

-   If the activities in your IP were custom-developed using C# using the Opalis API and you have not already converted them to be compatible with Orchestrator, you must follow the steps outlined in Migrating QIK API Custom Activities before continuing.  

    > [!NOTE]
    >  Java-based activities using the Opalis API for Java are no longer supported by the Integration Toolkit or by Orchestrator.  

-   If your IP contains dependent or other included files, those file must be available to repackage into the new IP. If you do not have a separate copy of these files, you will need to install the IP to an Opalis 6.3 server first and then locate the files in the following directory: “C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions\Support\Bin”.  

-   If your IP contains a custom resource file used for activity and category icons, that file must be available for the new IP. If you do not have a separate copy of this file, you will need to install the IP to an Opalis 6.3 server first and then locate the file in the following directory: “C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions”.  

-   If your IP used the standard icons provided by QIK for the category or activity icons and you wish to continue using those icons instead of using the new icons provided in Orchestrator, you will need to obtain the Opalis.QIK.Wizard.Images.dll file and use it as you would a custom resource file. If you do not have a separate copy of this file, you will need to install the IP to an Opalis 6.3 server first and then locate the file in the following directory: “C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions”.  

> [!NOTE]
>  For the easiest conversion process, you should place all of these files in the locations they were in when the IP was originally packaged before starting the IP Wizard. The IP Wizard references these files by their original paths. Selecting a new path is possible for all files, but selecting a new path for assemblies containing the activities will result in some of the details of the activity to be reset, requiring you to re-enter the information. By using the original paths for the files, the existing information is simply re-used without having to re-enter it.  

#### To convert an Opalis-compatible Integration Pack  

1. Start the Integration Pack Wizard  

2. Click **Import Integration Pack**.  

3. Select the existing OIP file and click **Open**.  

4. You will see a warning message indicating the IP is not compatible with Orchestrator. Click **OK**.  

5. Modify the product details as necessary to reflect any changes. Note that the version number of the IP is automatically incremented and the “Upgrade” checkbox is checked. Click **Next**.  

6. On the Activities page, go through each activity and ensure that the information is completed correctly. If the assembly for the activity has not been migrated or is not in the same location as it was when the IP was created, the **Class** field will be empty. To prevent having to retype any information, you should replace the assembly before starting the wizard.  

7. When you are done editing activities, click **Next**.  

8. Ensure dependent files are still in the same location as shown, or remove them and add new dependent files. Click **Next**.  

9. Enter a path and filename for the new IP file. Do not use the same name as the previous IP so that you can ensure that you retain a copy of the previous IP. Click **Next** to build the IP.  

   You now have an IP that is compatible with Orchestrator and can be registered and deployed using Orchestrator Deployment Manager.  

## Integration Packs – Known Issues  

### Filename length limitation  
 When including assemblies in your Integration Pack, they are automatically added to the registry by the installer. Due to the limitation in the registry key name length, the combined path and filename of an assembly cannot exceed 234 characters. Given the default path where assemblies within an IP are placed, the maximum filename length of an included assembly file cannot exceed 80 characters. If an assembly with a filename exceeding 80 characters is included in the installation, the installation will fail.  

## Orchestrator Resources  
 In addition to this online reference provided for System Center 2012 Orchestrator, there are a number of resources that can provide additional information on building runbooks, using the Integration Toolkit, and best practices.  

|||  
|-|-|  
|Resource|Location|  
|System Center Home|[https://www.microsoft.com/en-us/cloud-platform/system-center](https://www.microsoft.com/en-us/cloud-platform/system-center)|  
|System Center documentation|[https://docs.microsoft.com/en-us/system-center/](https://docs.microsoft.com/en-us/system-center/)|  
|Orchestrator Team Blog on TechNet|[https://blogs.technet.microsoft.com/orchestrator/](https://blogs.technet.microsoft.com/orchestrator/)|  
|Orchestrator Community Releases on CodePlex|[https://archive.codeplex.com/?p=orchestrator](https://archive.codeplex.com/?p=orchestrator)|  
|Orchestrator Community Forums on TechNet|[https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator](https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator)|

## See Also  
 [Orchestrator Integration Packs](https://www.microsoft.com/en-us/search/result.aspx?q=Orchestrator+Integration+Toolkit)   
 [Integration Toolkit Documentation](orchestrator-integration-toolkit-overview.md)   
 [Orchestrator SDK](https://msdn.microsoft.com/en-us/library/hh855054.aspx)