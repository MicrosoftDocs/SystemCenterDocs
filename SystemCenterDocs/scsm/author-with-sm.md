---
title: Author with Service Manager
description: Provides an overview of using, authoring, and customizing management packs, which enable customizations in Service Manager.
manager: carmonm
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
ms.assetid: aee0c089-e64e-4d2b-8313-a30a0efc5659
---

# Author with System Center 2016 - Service Manager

Authoring in Service Manager refers to using, authoring, and customizing management packs, which enable customizations in Service Manager. The articles in this section provide an introduction to authoring in Service Manager, including an overview of the Service Manager Authoring Tool.

## Introduction to authoring with the Service Manager Authoring Tool

Service Manager automates help desk functions, such as ticketing and change request processes, to help organizations manage their help desks. Service Manager integrates with Active Directory Domain Services \(AD DS\), Operations Manager, and Configuration Manager to build a single, reconciled inventory of an organization's assets.  

Service Manager uses management pack files that contain object definitions for the various features of the product. You can customize the behavior of Service Manager and extend it by creating and modifying management packs. This authoring guide describes the use, authoring, and customization of management packs.  

The Service Manager 2016 Software Development Kit \(SDK\) contains information that you might need when you are authoring with Service Manager. The SDK includes reference information for the class libraries and documents that the schema uses to create XML\-based management packs. To download the documentation for the System Center Service Manager 2016 SDK, see [System Center Service Manager Software Development Kit \(SDK\) Documentation](https://msdn.microsoft.com/library/hh965050.aspx).  

### Overview of management packs

Management packs in Service Manager are XML\-based files that contain definitions for classes, workflows, views, forms, and reports. You can use management packs to do the following:  

-   Extend Service Manager with new objects  
-   Extend Service Manager with new behavior  
-   Store new custom objects that you created, such as forms or templates.  
-   Transport customizations to another Service Manager deployment or implement the customizations in a newer deployment  

You can use management packs to extend Service Manager with the definitions and the information necessary to implement all or part of a service management process.  

By default, the Service Manager installation folder contains several preimported management packs that enable core Service Manager features, such as incident management and change management.  

> [!IMPORTANT]  
>  Unsealed management packs are not automatically upgraded during an upgrade to System Center 2016 - Service Manager.  

### Overview of authoring methods for Service Manager

There are three methods that you can use to customize Service Manager. While all three methods result in changes to a management pack file, they differ in scope and in the complexity of the customization that they provide.  

The three methods for customizing and extending Service Manager are as follows:  

-   Using the Service Manager console  
-   Using the Service Manager Authoring Tool  
-   Directly modifying and authoring management pack files  

In general, we recommend that you use the Service Manager console or the Authoring Tool for simple customizations and that you work directly with the management pack files only for customizations that the Service Manager console and the Authoring Tool do not support.  

#### Service Manager console  

The **Administration** pane and the **Authoring** pane in the Service Manager console provide for limited ad hoc customization of Service Manager features. When you customize Service Manager features in the Service Manager console, the customizations are stored in new or existing unsealed management packs and in the Service Manager database. \(Unsealed management packs are management packs that you can modify. For more information about sealed and unsealed management packs, see [Management Packs: Key Concepts](mps-in-auth-tool.md)).  

The Service Manager console provides for the following customizations:  

-   In the **Administration** pane, you can customize settings for activities, change management, incident management, and notifications. For example, you can configure the list notification recipients when an incident changes status.  
-   In the **Authoring** pane, you can make simple customizations to objects, such as queues, lists, and views.  


#### Authoring Tool  
The Authoring Tool provides an environment in which you can open, view, customize, extend, and author Service Manager management packs. You can use the Authoring Tool to modify some class properties, customize forms in a graphical form designer, and modify and create Service Manager workflows.  

You can also use the Authoring Tool to create advanced customizations that require testing and verification before implementation. The Authoring Tool does not require advanced user skills or advanced knowledge of the internal architecture of Service Manager.  

#### Directly modifying and authoring management pack files  

For extensive or complex customizations and for customizations that require coding \(such as extending the data in the Service Manager database, customizing forms, or modifying the default behavior of a feature's workflow\), you have to edit the .xml file of the corresponding management pack directly. Working directly with management pack files requires in\-depth knowledge in several areas, such as the System Center Common Schema and the structure of management packs. Also, manual editing is prone to errors.  

### Overview of the Authoring Tool for Service Manager

The Authoring Tool is a tool in Service Manager that you can use to open an existing management pack so that you can view, customize, and extend it. Using the Authoring Tool, you can do the following:  

-   Extend and customize the Service Manager class model  
-   Customize forms  
-   Create and customize workflows  

You can also use the Authoring Tool to create new Service Manager management packs. By authoring management packs, you can customize the features of Service Manager.  

After you modify or create a management pack, you must save it and then import it into Service Manager.  

#### Requirements for the Authoring Tool

Before you set up the Authoring Tool in Service Manager, ensure that the server on which you plan to install the Authoring Tool meets all the following server and operating system requirements.  

##### Server requirements  

You can install the Authoring Tool on a server that hosts the Service Manager management server, or you can install it on a separate server.  

##### Operating system requirements  

-   Windows Vista \(any edition\) with the latest service pack  
-   Windows 7  
-   Windows Server 2008 with the latest service pack  
-   Windows Server 2008 R2  

##### Additional requirements  

-   [Microsoft .NET Framework 3.5](https://go.microsoft.com/fwlink/p/?LinkId=162791), which you can download from the Microsoft Download Center.  
-   Microsoft Visual Studio 2008 Shell, which must be in the same language as the display language of the operating system. You can install Visual Studio 2008 Shell from the **Prerequisites** page in the Service Manager Authoring Tool Setup Wizard.  

    > [!NOTE]  
    >  During Authoring Tool Setup, if an error appears stating that Microsoft Visual Studio Shell 2008 is not installed and you've verified that it is installed, then the Visual Studio 2008 Shell Isolated Mode Redistributable Package might not be installed completely. To install it, navigate to \<SystemDrive\>\\VS 2008 Shell Redist\\Isolated Mode\\ and run VS\_Shell\_isolated.enu.exe.  

#### Set up the Authoring Tool

The SCSM2016\_AuthoringTool\_RTM.exe program file contains the Service Manager Authoring Tool .msi installation package and support files. This includes the files that are required for customizing default Service Manager forms. Ensure that the user who will be running the Authoring Tool has access to the local folder that you used to extract the files from the SCSM2016\_AuthoringTool\_RTM.exe program file.  

If Windows Error Reporting is enabled on the computer that is running the Authoring Tool, errors are reported automatically.  

##### To install the Authoring Tool  

1.  Verify that the computer on which you plan to install the Authoring Tool meets the requirements.  
2.  Download the [SCSM2016\_AuthoringTool\_RTM.exe](https://www.microsoft.com/download/details.aspx?id=40896) program file from the Microsoft Download Center to the local computer on which you want to install the Authoring Tool. Double\-click **SCSM2016\_AuthoringTool\_RTM.exe**.  
3.  In the **WinZip Self\-Extractor - SCSM2016\_AuthoringTool\_RTM.exe** dialog box, type a path to which to extract the files, and then click **Unzip**.  
4.  Browse to the folder where you extracted the files, expand the **CDImage** folder, and locate **Setup.exe**. Double\-click **Setup.exe** to start Setup.  
5.  In the Service Manager Authoring Tool Setup Wizard, click **Install the Service Manager Authoring Tool**.  
6.  Continue through the **Product registration** and the **Installation location** pages.  
7.  On the **Prerequisites** page, if any prerequisite test fails, you must update the server to ensure that each prerequisite is met. If Microsoft Visual Studio 2008 Shell is not installed, click **Install Microsoft Visual Studio Shell 2008** to install the application.  
     Click **Check prerequisites again**, and fix any other problems until all prerequisite tests pass.  
8.  Continue through the **Use Microsoft Update to help keep your computer secure and up\-to\-date** pages.  
9. On the **Installation summary** page, click **Install** and wait for the installation to finish.  

##### To start the Authoring Tool  

1.  On your desktop, click **Start**.  
2.  Click **Programs**, click **Microsoft System Center**, and then click **Service Manager 2016 Authoring**.  
3.  Click **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  
4.  In the **Class Browser** pane, click **Refresh**. This populates the browser with all the classes that are defined in management packs from the \<Installation folder\>\/Library folder. When you opened the Authoring Tool for the first time, this pane was empty.  

#### Authoring Tool panes

In the Service Manager Authoring Tool, you can open a management pack, view and customize its objects, and author new objects.  

The Authoring Tool has several panes. You can resize, dock, undock, move, or close each pane according to your preferences. You can open any of the panes in the Authoring Tool from the **View** menu.  

The following sections describe the panes in the Authoring Tool.  

##### Class browser  

The **Class Browser** pane displays the classes and their properties from all the management packs that are in the Library folder and all the management packs that have been opened in the Authoring Tool. You can also drag a property from this pane to add a control to a form that you are authoring in the authoring pane.  

##### Form browser  

The **Form Browser** pane displays a list of forms from all the management packs that are in the Library folder or from a specific management pack. From this pane, you can locate and select a form to view or to customize in the authoring pane, without knowing the exact management pack of the form. From this pane, you can also view the details of a form in the **Details** pane.  

##### Management pack explorer  

In this navigation pane, you can view management packs and their objects. The objects are grouped by types. The **Management Pack Explorer** displays classes, forms, workflows, and references. You can also select a specific object, such as a form, to customize.  

##### Authoring  

The authoring pane displays the tabs in which you change or create management pack objects, such as forms and classes. For example, when you customize or author forms, this pane displays the user interface \(UI\) controls of a form so that you can add, move, or change these controls to customize the appearance and behavior of the form.  

The authoring pane also contains the **Start Page** tab, which displays the **Authoring Tool Overview** page.  

##### Details  

The **Details** pane displays details, such as properties, for a selected object. The information in this pane is updated every time you select an object in the **Management Pack Explorer**, authoring pane, **Class Browser** pane, or **Form Browser** pane. You can make changes directly in this pane to update property values.  

##### Form customization toolbox  

The **Form Customization Toolbox** pane displays basic UI controls that you can drag to the authoring pane when you customize forms.  

##### Activities toolbox  

The **Activities Toolbox** pane displays activities that you can use as building blocks when you author workflows.  

#### Upgrade management packs to work with the Authoring Tool

During an upgrade to Service Manager, all customized Service Manager management packs are unsealed. \(Unsealed management packs are management packs that you can modify. For more information about sealed and unsealed management packs, see [Management Packs: Key Concepts](mps-in-auth-tool.md)). Management packs are copied to the new Service Manager folders without any further upgrade\-related processing. Using these custom management packs that were authored in previous versions of System Center Service Manager is supported. However, there are some issues to be aware of, and you may have to make some updates to these management packs to ensure that they work properly and as intended after the upgrade to System Center 2016 - Service Manager.  

##### Forms  
The placement of a control in a form is determined by its top, bottom, left, and right margins in relation to either its parent control or to the form itself. In a customized form, this method can cause controls to be adjusted improperly when the margins of the parent control or of the form are modified.  

As a result of updated styles that were implemented in System Center 2012 - Service Manager, some custom forms that were authored in System Center Service Manager 2010 might have layout issues when they are imported into System Center 2012 or 2016 - Service Manager. Depending on the customization, some controls might be placed incorrectly, causing issues such as overlapping and clipping. Some of these issues affect only how the form looks, and other issues can prevent some intended functionality of the form.  

The following sections describe the issues that you might encounter when you import into System Center 2016 - Service Manager forms that were authored in System Center Service Manager 2010. These sections also describe how you can use the System Center 2016 - Service Manager Authoring Tool to rectify these issues to ensure that these forms look and function as intended.  

###### Clipping and overlapping controls  

Some controls on a form might appear clipped, with incomplete border lines and cut\-off text. Sometimes this issue appears in conjunction with another issue in which controls overlap each other. Also, some controls on a form might not be visible, causing some functionality of the form to be unavailable.  

To rectify these issues, you may have to use the Authoring Tool to adjust the control's properties as follows. You may have to try several remedies, and you may have to make several attempts before the control is placed correctly.  

-   Select the affected control, and check the value of its **Margin** properties: **Bottom**, **Left**, **Right**, and **Top**. For example, set the values of these properties to 0, or to a positive value, to ensure that there are no negative values that cause the control to be placed incorrectly.  
-   Check the values of the affected control's **Layout** group properties: **Horizontal Alignment** and **Vertical Alignment**. You may have to set the values of these properties to **Stretch** for better control alignment.  
-   Place the affected control in a grid inside a **Panel** control for better control alignment.  
-   Set the parent control's dimensions to **Auto** to allow its size to shrink or grow dynamically.  
-   Set the **Height** property of the container of the affected control to **Auto**. This allows the width and the height of controls to be automatically adjusted correctly to fit the container of the object.  

###### Shuffle controls  

Some controls on a form might be shuffled with each other, resulting in controls not being placed in their designated location on the form.  

To rectify this issue, use the Authoring Tool to do one of the following:  

-   Drag controls to their desired location on the form.  
-   Select the control that is shuffled. In the **Details** pane, in the **Margin** properties group, adjust properties such as **Bottom** or **Left** to place the control in the desired location.  
-   Select the control that contains the shuffled control. In the **Details** pane, modify its properties such as **Bottom** or **Left**, in the **Margin** properties group.  

##### Workflows  

Workflows that were developed in System Center Service Manager 2010 are supported in System Center 2016 - Service Manager.  

###### Virtual Machine management activities  

The Virtual Machine Management workflow activities in System Center 2016 - Service Manager support System Center Virtual Machine Manager 2008 R2. However, these activities do not support System Center 2016 - Virtual Machine Manager.  

If you are trying to automate IT processes that require the use of an activity that supports System Center 2016 - Virtual Machine Manager, using System Center 2016 - Orchestrator runbooks and VMM instead might be helpful.  

## Next steps

- Learn about customizing objects functionality in Service Manager with [Management packs in the Authoring Tool](mps-in-auth-tool.md).
- [Customize and author classes with Service Manager authoring](auth-classes.md).
