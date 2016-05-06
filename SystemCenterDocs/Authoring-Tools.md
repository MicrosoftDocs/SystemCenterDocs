---
title: Authoring Tools
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: adb418d7-95ab-4e33-8ced-34a934016aa3
---
# Authoring Tools
There are multiple tools available for creating new monitoring in [!INCLUDE[om12long]./Token/om12long_md.md)]. The choice you make will depend on your requirements and experience with [!INCLUDE[om12short]./Token/om12short_md.md)]. Each of the available tools is described below.

## <a name="OperationsConsole"></a>Operations Console
The **Authoring** workspace of the Operations console contains templates and wizards that let you create monitoring scenarios that require minimal knowledge of authoring concepts.

Specific characteristics of the Operations console include the following:

-   Creates or changes a management pack file in an existing management group. Changes are committed and deployed to agents immediately.

-   Creates predefined monitoring scenarios by using templates and wizards. Cannot create custom monitoring scenarios.

-   Cannot create custom classes or discoveries except for specific cases that the template provides.

The primary advantage of the Operations console is the ability to create new monitoring scenarios with minimal complexity. The Operations console provides the following approaches for creating monitoring scenarios.

### Management Pack Templates
Management Pack templates let you create complete monitoring scenarios with minimal input. A single template can create different monitors, rules, and even new target classes without requiring you to know any of the details. If a template is available for the monitoring scenario that you want to create, this method is typically your easiest and most effective solution.

### Distributed Application Designer
The Distributed Application Designer lets you create a single application that is comprised of multiple objects. It does not let you create new monitoring for these objects. The health of each object included in the distributed application is based on the monitors already running against that object. The health of the distributed application is based on the health of the individual objects that are included in it.

### Authoring Wizards
Wizards let you create new monitors, rules, and tasks. You have to know the details of what data the workflow uses and what action are performed with that data. Wizards are available for a variety of different data sources and monitoring scenarios. You cannot create a new target with the monitoring wizards. You can use a suitable wizard that is available in an existing management pack, or you can create a wizard by using a template or by editing the management pack in the Authoring console.

Use of the Operations console is documented in this guide.

## <a name="MPAuthor"></a>MP Author
MP Author is a free management pack authoring tool available from Silect Software. It allows an IT Pro to use a wizard driven interface to create management packs for System Center 2012 – Operations Manager without significant knowledge of the underlying management pack structure or any knowledge of XML. MP Author is intended to be the primary authoring tool for the IT Pro creating management packs for the latest version of Operations Manager.

MP Author is limited to the scenarios that it provides. You cannot create elements such as modules and monitor types required to support custom scenarios. Management packs created with the tool can be loaded into Visual Studio Authoring Extensions to provide this functionality.

Specific characteristics of MP Author include the following:

-   Creates or changes a management pack on disk without requiring access to the management group.

-   Creates management pack elements including custom classes, relationships, and discoveries that cannot be created in the Operations console.

-   Hides some of the complexity of management packs by providing an intuitive interface for creating common discovery and monitoring scenarios.

-   Provides user interface for creating product knowledge.

-   Integrates with [Silect MP Studio](http://silect.com/products/mp-studio) for further control over the management pack lifecycle

MP Author and its documentation can be downloaded at [www.mpauthor.com](http://www.mpauthor.com).

## <a name="AuthoringConsole"></a>System Center Operations Manager 2007 R2 Authoring Console
The [!INCLUDE[om2007r2long]./Token/om2007r2long_md.md)] Authoring console can be used to create management packs for both [!INCLUDE[om2007r2long]./Token/om2007r2long_md.md)] and [!INCLUDE[om12long]./Token/om12long_md.md)]. It is intended for management pack authors with significant knowledge of the structure of management pack elements and lets them create and modify all elements in a management pack. It is not limited to a specific set of scenarios, although it does require deeper technical knowledge than the Operations console.

The Authoring console provides many of the same wizards as the Operations console, except that the Authoring console wizards can provide access to additional options. The Authoring console provides custom dialog boxes similar to the Operations console to help you configure management pack elements where they are available. For those elements where no dialog box is available, you must edit the XML code of the management pack directly. To help edit, the Authoring console starts an external editor. You use the editor to edit the XML code of the specific element and, when it is closed, the editor returns the completed element back to the management pack. You can specify the editor that the Authoring console starts.

Specific characteristics of the Operations console include the following:

-   Creates or changes a management pack on disk without requiring access to the management group. Optionally, loads management packs from a management group and installs them after modification.

-   Provides custom ID for each management pack element.

-   Creates all management pack elements including custom classes, relationships, and discoveries that cannot be created in the Operations console.

-   Creates predefined monitoring scenarios by using wizards. Creates custom monitoring scenarios with the assistance of the user interface.

Use of the [!INCLUDE[om2007r2long]./Token/om2007r2long_md.md)] Authoring Console is documented in the [System Center Operations Manager 2007 R2 Authoring Guide](http://go.microsoft.com/fwlink/?LinkID=188119).

## <a name="XMLEditor"></a>Visual Studio Authoring Extensions
Because management packs are .xml files, any XML editor can create and modify them. While this is more complex than using the other authoring options, editing the XML gives you complete control over all elements in a management pack.

An XML editor is required for the following scenarios that cannot be performed in the consoles:

-   Management pack elements cannot be copied by using the other consoles. For example, you might want to create a management pack element by copying a similar element in the same management pack, or you might want to copy an element from another management pack into the current one. This functionality can only be performed with an XML editor.

-   The consoles do not let an existing management pack element be modified if it affects the configuration of another element. For example, a rule might use a custom module that requires values for one or more parameters. You might want to modify this module and add an additional parameter to it. Because the rule would not provide a value for this required parameter after the module was modified, the changed module cannot be saved. To make this change in the Authoring console, you must delete the rule and create it again after changing the module. By using an XML editor, you can change the module and rule at the same time.

-   The ID of a management pack element cannot be changed with the Authoring console after it has been created. You must perform this task with an XML editor. The ID of the element cannot only be changed, but you must search for the old ID and replace it with the new ID across the management pack because the element’s ID might be used multiple times in the XML code.

The Visual Studio Authoring Extensions allow you to work with the XML of a management pack in [!INCLUDE[om12long]./Token/om12long_md.md)] directly using Microsoft Visual Studio. It provides the following advantages over using a standard XML editor:

-   Provides XML templates and IntelliSense for different management pack elements so that you don’t have to have detailed knowledge of the schema.

-   Allows you to create XML fragments containing different management pack elements. The fragments can be copied within the management pack, to another management pack, and combined to build the final management pack.

-   Allows multiple authors to work on a single management pack project at the same time.

Documentation for the Visual Studio Extensions is available at [Visual Studio Authoring Extensions for System Center 2012 \- Operations Manager](http://go.microsoft.com/fwlink/?LinkID=232334).

## See Also
[System Center Operations Manager 2007 R2 Authoring Resource Kit](http://go.microsoft.com/fwlink/?LinkID=192098)



