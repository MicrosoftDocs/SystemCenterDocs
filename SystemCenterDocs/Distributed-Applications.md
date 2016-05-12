---
title: Distributed Applications
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9deed7cf-5546-485f-9276-a1e4ad9dd928
---
# Distributed Applications
A *Distributed Application* in [!INCLUDE[om12short](Token/om12short_md.md)] is an application that is comprised of multiple objects. These objects may be defined by different management packs and may be managed on the same agent or on different agents. The purpose of the distributed application is to provide an overall health for an application that is comprised of different objects.

Distributed applications do not provide any additional monitoring for the objects in an application. Instead, they include objects that are already being monitored. The value of the distributed application is to provide a relationship between the health of objects that are part of a single application.

You can create distributed applications using the **Distributed Applications Designer** in the Operations console.

## Distributed Application Designer
The *Distributed Application Designer* provides you with the ability to create a distributed application in a graphical environment with minimal knowledge of the underlying management pack elements that are created. There are some limitations to the tool though as follows:

-   The component groups can only have explicit members, which means that you cannot populate them dynamically. For example, you may have a distributed application with a set of web sites. You install an additional web server with a site that should be included. You would have to edit the distributed application and manually add the new site.

-   You cannot create multiple levels of health rollup. The health of the application will be the worst health of any of the component groups regardless of the relationships that have been created for them.

You can create a distributed application without these limitations by using the [Visual Management Pack Designer](Authoring-Tools.md#VMPD).

## Contents of Distributed Applications

### Objects
A distributed application must include one or more objects in order to be useful. Any object discovered by different management packs installed in the management group can be used in a distributed application. This might come from a management pack installed from the catalog or one that you have created on your own. These can be objects created by different monitoring wizards as discussed in [Management Pack Templates](Management-Pack-Templates.md).

### Component Groups
A component group can contain any number of objects, and any object added to the distributed application must be contained in a component group. When you create the component group, you specify one or more classes that the group can contain. Only objects that are instances of these classes may be added to the particular group. If you specify **All Objects** then any objects in the management group can be included in the component group.

If you want to limit the objects that can be included in the component group, then you should select the **Object\(s\) if the following type\(s\)** and then select one or more classes from the class tree. The tree will contain all of the classes in the management group which are provided by all the management packs currently installed.

The dialog box arranges classes in a tree according to their base classes. You can read more about base classes at [Base Classes](Understanding-Classes-and-Objects.md#BaseClasses). If you select a class, then each of its base classes will also be selected. This allows you to select a single class such as **Computer Role** that is often used as a base class and automatically select all of its base classes.

### Relationships
*Relationships* can be drawn between component groups to represent some relation between different kinds of objects. Health is not rolled up between the component groups, but the relationship is indicated by lines between the groups.

## <a name="Templates"></a>Distributed Application Templates
Templates allow you to start a new distributed application with a predefined set of component groups. You need to add objects to these component groups and can modify the component groups and add additional component groups as you require. You can save time in creating a distributed application by selecting a template that most closely resembles your requirements. If you want to create an empty distributed application and manually add all your own component groups, then select the **Blank** template.

The following table lists the available templates:

|Template|Description|Container Groups|Contained Classes|
|------------|---------------|--------------------|---------------------|
|.NET 3\-Tier Application|Brings together objects and monitoring data from synthetic transactions with data from Application Performance Monitoring|-   \[Application name\] Client Perspective<br />-   \[Application name\] Presentation Tier<br />-   \[Application name\] Business Tier<br />-   \[Application name\] Data Tier|-   Perspective<br />-   ASP.NET application<br />-   .NET application component<br />-   Database|
|Line of Business Web Application|Component groups common to a web application|-   Web Sites<br />-   Databases|-   Web Site<br />-   Database|
|Messaging|Component groups common to messaging services|-   Messaging Clients<br />-   Storage<br />-   Messaging Components<br />-   Directory Services<br />-   Network Services<br />-   Physical Network|-   Perspective<br />-   <br />-   Logical Hardware Component<br />-   Computer Role<br />-   Computer Role<br />-   Network Device|
|Blank|Empty distributed application with no component groups|None|None|

## Viewing Distributed Applications
Each distributed application will be listed in the **Distributed Application** state view in the **Monitoring** pane of the Operations console. The state of the distributed application will be the worst state of any of the objects that it contains. You can launch any of the other kinds of the view by right\-clicking on the distributed application and selecting the view that you want. Each view will include data for all of the objects contained in the distributed application.

## Creating and Modifying Distributed Applications

#### To create a distributed application

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace.

3.  Right\-click **Distributed Applications** and select **Create a new distributed application**.

4.  In the **Name** box, type a name for the distributed application. This name will appear in the **Monitoring** workspace of the Operations console.

5.  In the **Template** box, select  the template for the starting point of the distributed application. See [Distributed Application Templates](Distributed-Applications.md#Templates) for information on the available templates.

6.  Select the management pack that you created in step 1.

7.  Click **OK**.

#### To edit an existing distributed application

1.  In the Operations console, select the **Authoring** workspace.

2.  Select **Distributed Applications**.

3.  In the **Distributed Applications** pane, right\-click the distributed application you want to edit and select **Edit**.

#### To create a component group

1.  With the distributed application open, click **Add Component**.

    > [!NOTE]
    > The first time that you create a component group since opening the Operations console, it may take several seconds to open the **Create a New Component Group** dialog box since the list of classes must be cached. The amount of time that this takes will depend on the number of classes in your management group.

2.  In the **Name your component group** text box, provide a name for the component group. This is the name that will appear in the diagram view and the Health Explorer for the distributed application.

3.  If the component group should be able to contain any type of object, then select **All Objects**. If you want to specify one or more types that the component group should be able to contain, then select **Objects of the following type**.

4.  Select one or more classes to allow objects of that type to be included in the management group.

5.  Click **OK** when you have selected the classes.

    > [!NOTE]
    > You may receive a message saying that the allowed limit was reached while making a new object type button visible. This means that no more object selection panes can be added to left side of the Distributed Application Designer. Either select **Leave the new object type not visible** to not create a new object selection panel for the current component group or select **Replace the selected visible Object Type button with a new one** and select one of the object types in the list to close. You can reopen the selection pane by selecting it in the **Organize Object Types** pane.

#### To add an object to the distributed application

1.  Ensure that a component group is created that allows the type of object that you want to add.

2.  If a selection pane is not open for the type of object you want to add, click **Organize Object Types** and then select the type of object you want to add.

3.  Select the type of object you want to add in the Object Picker. This should display a list of all objects of the selected type.

4.  Click and drag one or more of the objects into a component group. Note that you will only be able to add the objects to a component group that will accept objects of that type.

## See Also
[Understanding Classes and Objects](Understanding-Classes-and-Objects.md)


