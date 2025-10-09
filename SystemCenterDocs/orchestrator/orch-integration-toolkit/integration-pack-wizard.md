---
title: Orchestrator Integration Toolkit Integration Pack Wizard
description: This article provides details about the Orchestrator Integration Pack Wizard.
author: Jeronika-MS
ms.author: v-gajeronika 
ms.date: 04/17/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
ms.custom: engagement-fy24
---

# Integration Pack Wizard

The Integration Pack Wizard (IP Wizard) allows you to create a new Integration Pack from an existing _Integration assembly_. _Integration assemblies_ can be authored using the Command-Line Activity Wizard (`CLIActivityWizard`) or using the Orchestrator SDK. The IP Wizard (`IPWizard`) packages the assemblies, dependent files, and required metadata into a `.OIP` file that can be deployed via the Orchestrator Deployment Manager.
You can create professional-looking Integration Packs with full branding and custom icons, or simply package up command-line activities so that they can be more easily deployed using the IP Wizard.

## Decide when to create an integration pack  

It’s important to decide whether it’s appropriate to use activities individually with the Toolkit’s **.NET Integration Pack** activities, or it's better to create and deploy all the activities in an Integration Pack.  

When you only have few activities or when you’re in the development phase and creating many changes in an activity, you should just use the assemblies with the Toolkit **.NET Integration Pack** activities to execute those activities in Runbooks. Packaging, registering, deploying, uninstalling, and upgrading of Integration Packs incur large overhead in the process of development.

If you have a group of activities to test or you’re further along in the development cycle and want to test the entire end-to-end process of installation or upgrade, then creating an Integration Pack is the better approach. The Integration Pack provides a more user-friendly experience and a complete installation experience. Integration Packs also allow for deployment of the activities to multiple Runbook Servers or Runbook Designers across the organization or to external customers.  

## Create a new integration pack  

The Integration Pack Wizard allows you to create Integration Packs from the existing Orchestrator-compatible assemblies and dependent files. If you haven't yet created an Orchestrator-compatible assembly, see the [Command Line Activity Wizard](command-line-activity-wizard.md#create-a-new-activity-assembly).  

> [!NOTE]
> The Integration Toolkit no longer includes the binaries for the Windows Installer XML (WiX) Toolset, which is used by the IP Wizard for creating custom Integration Packs. Please install the latest version (v3.11) of the [WiX Toolset][wix-official] prior to using the IP Wizard.

[wix-official]: https://wixtoolset.org/

To create an integration pack, follow these steps:

1. Start the Integration Pack Wizard. Select **Start > Orchestrator Integration Pack Wizard**. The welcome page displays.  

2. If you've an existing Integration Pack that you want to update, select **Import Integration Pack**. For more information, see [Update an Integration Pack](integration-pack-wizard.md#update-an-existing-integration-pack). To create an Integration Pack, select **Next**.  

   > [!IMPORTANT]
   > If you want to upgrade an existing IP, you must select **Import Integration Pack**. If you select **Next**, the IP you create will have a new unique product ID and new unique IDs for all activities, even if you re-use a previous assembly and use the same product and filenames.  

3. On the **Product Details** page, enter or modify the information as needed to customize the information about your Integration Pack. The table below describes the fields and their descriptions:  

   |    Field Name            |     Description                                                                                                                                                                                                                                                                                                                                                                                                   |
   |----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  Product name  |                                                                                                                                                                         The name of the IP that displays in Deployment Manager                                                                                                                                                                         |
   | Category name  |                                                                                                                                                   The text that displays as the category title for the IP in the Activities pane of Runbook Designer                                                                                                                                                   |
   |    Company     |                                                                                                                                                    The name of your company. This information is displayed in Add/Remove Programs under “Publisher”                                                                                                                                                    |
   |   EULA file    |                                                                                                            An RTF-formatted text file with a `.EULA` extension. The EULA is displayed to the user during registration using Deployment Manager and requires acceptance before registration.                                                                                                            |
   | Resource file  |                                                                                 An assembly containing icons and other resources used to provide the category and activity icons. By default, the standard Toolkit resource file is used (Microsoft.SystemCenter.Orchestrator.Integration.Toolkit.Wizard.Images.dll)                                                                                  |
   |    Version     |                                                                                                                                The version number of the Integration Pack, which will be displayed in Deployment Manager and used to determine if the IP is an upgrade.                                                                                                                                 |
   | Enable upgrade | If you imported an existing Integration Pack, this checkbox is selected by default, enabling this Integration Pack to upgrade an existing installed version. If you clear this checkbox, new product and activity IDs will be created for the IP (it will not upgrade an existing version). If you want to enable side-by-side installation of multiple versions of your IP, clear this checkbox. |
   |  Description   |                                                                                                                                                                            A detailed description of your Integration Pack                                                                                                                                                                             |
   | Category Icon  |                                                                                                                           The default category icon is displayed. If you wish to choose another icon, select the **Modify** button and select a new icon, and then select **OK**.                                                                                                                            |

4. When you're done entering product information, select **Next**. The Activities page is displayed. The Activities page is where you'll reference the assembly or assemblies that contain the activities you’ve defined using the Command-Line Activity Wizard or created using the Orchestrator SDK.  

5. To add a new activity to the IP, select **Add**.  

6. To open and add the assembly file, select the ellipsis **(…)** button to the right of **Library**. Browse to the desired assembly file, select it, and select **Open**. The file name and path are displayed in the Library field.  

7. To select an activity from the assembly, select the **Class** dropdown arrow and select the appropriate activity name from the list. The name and description defined in the activity are shown in the **Display Name** and **Description** fields.  

8. If desired, modify the display name and description of the activity.  

9. The default activity icon is displayed for the activity. If a different icon is desired, select **Modify**, select another icon from the browser, and select **OK**.  

10. Select **OK** to save the activity definition. The activity name and description now appear in the Activities list.  

11. Continue adding activities to the list as needed. When you're finished adding activities, select **Next**. The Dependencies and Included Files page displays.  

12. On this page, you can define a list of extra files that you want packaged with your Integration Pack. These files could be extra assemblies required by your activities, scripts, documentation, or other files you want deployed to Runbook Servers and Runbook Designers along with your activities. Select **Add**, select the file(s) you need, and then select **OK** to add files to the list.  

13. When you're done adding files to the list, select **Next**. The Orchestrator Integration Pack File page displays.  

14. In the textbox provided, enter the path and filename of the Integration Pack to be created. If you enter a filename that already exists, it will be overwritten. Ensure that you've sufficient access to write to the path specified or the process will fail. If no path is specified, the OIP file will be created in the Documents folder (`C:\users\<your username>\Documents`). Select **Next** to start building the IP.  

    > [!IMPORTANT]
    > The characters in the filename must be valid for the language that's installed on your operating system.  

    > [!IMPORTANT]
    > Specify a name for the Integration Pack that isn't common to ensure that it doesn't match the name of another Integration Pack. Orchestrator cannot install two Integration Packs with the same name.  

15. When the IP has been successfully built, the final page of the wizard will display the path and filename of the new OIP file. Select Finish to exit the wizard. If there's an error, you can select **Back** and retry the build process.  

    For information on deploying your Integration Pack, see the article [Add an Integration Pack](../how-to-add-an-integration-pack.md).  

## Update an existing integration pack  

The Orchestrator Integration Pack Wizard allows you to import an existing Integration Pack so that you can make changes and repackage it as a new version. Ensure that you check the **Enable Upgrade** checkbox, otherwise a new IP will be created instead of replacing or upgrading the previous installed version.  

### Helpful IP Upgrade Tips  

#### Update underlying assemblies

When you create an Integration Pack, metadata about the IP is stored in the package so that it can be read by the wizard during subsequent upgrades. When you update certain items such as activities or the underlying assemblies for those activities, you need to rebuild the IP. However, if you modify the activity settings and select a new assembly file, it will reset the fields on the Activity Information page, requiring you to enter the information again.  

You can retain the IP config settings while modifying only the assembly. Save your new assembly to the same path and filename as the previous assembly (which is shown in the Library field of the Activity Information dialog).

## QIK Integration Pack Migration  

If you created an Integration Pack using the Opalis QIK Wizard, you'll need to convert it to be compatible with Orchestrator before it can be imported and used by Orchestrator.  

Prior to converting an IP, the following steps must be completed:  

- If the activities in your IP were created using the QIK CLI Wizard, you must follow the steps outlined in [QIK CLI Activity Migration][cli-migration] to make them compatible with Orchestrator. If you don't have a separate copy of the assembly containing the activities, you'll need to install the IP to an Opalis 6.3 server first, and then locate the assembly in the following directory: `C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions\Support\Quick Integration Kit 3`.

- If the activities in your IP were custom developed in C# using the Opalis API, you must follow the steps outlined in [Migrating QIK API Custom Activities][opalis-migration] to make them compatible with Orchestrator.  

    > [!NOTE]
    > Java-based activities using the Opalis API for Java are no longer supported by the Integration Toolkit or by Orchestrator.  

- If your IP contains dependent or other included files, those file must be available to repackage into the new IP. If you don't have a separate copy of these files, you'll need to install the IP to an Opalis 6.3 server first, and then locate the files in the following directory: `C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions\Support\Bin`.  

- If your IP contains a custom resource file used for activity and category icons, that file must be available for the new IP. If you don't have a separate copy of this file, you'll need to install the IP to an Opalis 6.3 server first, and then locate the file in the following directory: `C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions`.  

- If your IP used the standard icons provided by QIK for the category or activity icons and you wish to continue using those icons instead of using the new icons provided in Orchestrator, you'll need to obtain the `Opalis.QIK.Wizard.Images.dll` file, and use it as you would a custom resource file. If you don't have a separate copy of this file, you'll need to install the IP to an Opalis 6.3 server first, and then locate the file in the following directory: `C:\Program Files (x86)\Common Files\Opalis Software\Opalis Integration Server\Extensions`.  

> [!NOTE]
> For the easiest conversion process, you should place all of these files in the locations they were in when the IP was originally packaged before starting the IP Wizard. The IP Wizard references these files by their original paths. Selecting a new path is possible for all files, but selecting a new path for assemblies containing the activities will result in some of the details of the activity to be reset, requiring you to enter the information again. By using the original paths for the files, the existing information is simply reused without having to re-enter it.  

#### Convert an Opalis-compatible Integration Pack

To convert an Opalis-compatible Integration Pack, follow these steps:

1. Start the Integration Pack Wizard.

2. Select the **Import Integration Pack**.  

3. Select the existing OIP file and select **Open**.  

4. You'll see a warning message indicating the IP isn't compatible with Orchestrator. Select **OK**.  

5. Modify the product details as necessary to reflect any changes. The version number of the IP is automatically incremented and the “Upgrade” checkbox is checked. Select **Next**.  

6. On the Activities page, go through each activity and ensure that the information is completed correctly. If the assembly for the activity hasn't been migrated or isn't in the same location as it was when the IP was created, the **Class** field will be empty. To prevent having to retype any information, you should replace the assembly before starting the wizard.  

7. When you're done editing activities, select **Next**.  

8. Ensure the dependent files are still in the same location as shown, or remove them and add new dependent files. Select **Next**.  

9. Enter a path and filename for the new IP file. Don't use the same name as the previous IP so that you can ensure that you retain a copy of the previous IP. Select **Next** to build the IP.  

   You now have an IP that is compatible with Orchestrator and can be registered and deployed using Orchestrator Deployment Manager.  

[cli-migration]: command-line-activity-wizard.md#qik-cli-activity-migration
[opalis-migration]: /previous-versions/system-center/developer/hh855057(v=msdn.10)

## Integration Packs – Known Issues  

### Filename length limitation  

When including assemblies in your Integration Pack, they're automatically added to the registry by the installer. Due to the limitation in the registry key name length, the combined path and filename of an assembly can't exceed 234 characters. Given the default path where assemblies within an IP are placed, the maximum filename length of an included assembly file can't exceed 80 characters. If an assembly with a filename exceeding 80 characters is included in the installation, the installation will fail.  

## Orchestrator resources

In addition to this online reference provided for System Center Orchestrator, there are many resources that can provide additional information on building runbooks, using the Integration Toolkit, and best practices.  

- [System Center home](https://www.microsoft.com/cloud-platform/system-center)
- [System Center documentation](../index.yml)
- [Orchestrator team blog](https://blogs.technet.microsoft.com/orchestrator/)
- [Orchestrator community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=systemcenterorchestrator)|

## Related content

- [Integration Toolkit Documentation](orchestrator-integration-toolkit-overview.md).
- [Orchestrator SDK](/previous-versions/system-center/developer/hh855054(v=msdn.10)).
