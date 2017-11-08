---
title: Work with management packs
description: Explains how to work with management packs in the Service Manager Authoring Tool.
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
ms.assetid: 8cbaa369-8881-46f6-9615-e9cbab638d5c
---

# Work with management packs in the Service Manager Authoring Tool

All customizations to objects and to functionality in Service Manager are implemented by using management packs. This section describes management packs and how to use and manage them to implement various types of customizations using different customization methods.  

## Key concepts about management packs

Before you work with management packs in Service Manager, you should be familiar with the following management pack concepts.  

### Sealed and unsealed management packs  
 There are two types of management packs:  

-   Sealed management packs: A sealed management pack \(.mp file\) cannot be modified.  

-   Unsealed management packs: An unsealed management pack \(.xml file\) can be modified.  

 Other than lists and forms, objects such as views that are defined in a sealed management pack cannot be customized. Customizing a list that is defined in a sealed management pack includes adding list items. Customizing a form that is defined in a sealed management pack includes adding fields.  

 You cannot unseal a management pack that is sealed. To modify objects that are stored in a management pack that you have already sealed, you can modify the original unsealed management pack file from which the sealed management pack was created. Alternatively, you can import the sealed management pack, and export it to a new unsealed management pack, that can be modified. After you import a sealed management pack, you cannot import the unsealed version of the same management pack until you delete the sealed version.  

### Model management pack  
 A model management pack is a management pack that contains definitions for basic objects, such as classes, combination classes, and relationship types.  

 Building model management packs makes it possible for other customizations-typically, customizations that are related to presentation, such as templates, views, and tasks-to be stored in separate management packs that depend on the model extensions. In addition, model management packs are easily transferred into the data warehouse for archiving and reporting purposes.  

### Dependencies, resources, and bundling management packs  
 A management pack can depend on another management pack that is sealed. For example, a custom template in one management pack can depend on a list that is defined in another management pack. The management pack that contains the base definitions \(such as the list\), on which other definitions depend, must be sealed. A management pack can also require resources, such as a form or an image, that are stored separately.  

 When you deploy a management pack that has resource requirements, you must bundle the required resources and the management pack into a single management pack file that can be imported into Service Manager.  

 In addition, if a management pack has dependencies on other management packs, those dependent management packs must be imported first. As an alternative, you can bundle the dependent management packs along with the required resources and the depending management pack.  

 For more information about how to bundle a management pack with its resources and dependent management packs, see the [How to Bundle Management Packs and Resource Files](bundle-mps.md).  

### Management pack customization  
 You might have to customize and extend the default, preimported management packs so that information technology \(IT\) professionals and other users in your organization can extend existing solutions and customize them to meet your business and customer needs. To customize features in Service Manager, you can add new objects or modify the objects that are related to that feature.  

 A customization to an object is a modification that applies to the base definition of the object. For customizations to be able to be applied to a base definition, the base definition must be stored in a sealed management pack. And because it is not possible to save customizations in the sealed management pack that contains the object's base definition, you always have to use or create another unsealed management pack to store customizations.  

 Typically, when you customize objects from a default, preimported management packs, you work with two management packs. The first management pack is the sealed management pack that contains the base definitions of objects, and the second management pack, which is initially unsealed, contains the customizations to the base object. In this case, the management pack with the customization depends on the management pack that contains the base definition of the object.  

 When you customize objects that are defined in an unsealed management pack, you can use the same management pack to store the customizations.  

 After you complete the customizations, you can deploy them by importing the management pack into Service Manager. During an import of a sealed management pack, Service Manager synchronizes the Service Manager database and the data warehouse database with the definitions from the management pack. During an import of an unsealed management pack, other than list definitions, Service Manager synchronizes only the Service Manager database with the definitions from the management pack. List definitions in an unsealed management pack are synchronized to both databases.  

## Guidelines and best practices for management packs

The following guidelines and best practices for working with management packs in Service Manager are described in this section.  

-   Group customizations into separate management packs.  

-   Seal model management packs.  

-   Create your own custom management packs when possible.  

-   Export custom management packs.  

-   Work across multiple management groups.  

### Group customizations into separate management packs  
 Group customizations into separate management packs as follows:  

-   Store model extensions and presentation extensions in separate management packs.  

     We recommend that you store the following objects in a model management pack:  

    -   New classes and class extensions, including properties and corresponding icons  

    -   New lists  

    -   Combination classes  

    -   Relationships  

    -   Child EnumerationValues that should not be modified  

    -   Forms for viewing and editing objects of the defined classes, and the respective assembly resources  

-   Group customizations by the solution that you are developing. For example, store incident-management-related customizations and settings separately from change-management-related customizations and settings.  

-   Group customizations based on usage considerations. For example, store customizations that you need to test and deploy as a unit in the same management pack.  

### Seal model management packs  
 You should seal management packs that contain base classes and other model objects, on which other definitions in other management packs depend on. Sealing a management pack prevents it from being modified. Also, it is important to seal a management pack so that its definitions are synchronized with the data warehouse database during import. This makes it possible for you to later add customizations (in another management pack), such as presentations that depend on the base objects from the sealed management pack.  

### Create your own custom management packs when possible  
 Some of the solution\-specific, preimported, unsealed management packs ("Configuration" management packs) contain customizable elements for the specific solution. In some cases you must store your customizations in those preimported management packs to ensure that the management pack adheres to the dependency rules. For example, templates that use list values that are defined in a "Configuration" management pack must be stored in that same management pack. This is because the list values that are used are defined in another unsealed management pack, and dependency on unsealed management packs is not supported.  

 However, whenever possible we recommend that you create new management packs to store your customizations. Creating your own management pack simplifies transportation of the management pack, and it can simplify an upgrade.  

 For example, when you extend a solution by adding objects, such as views, tasks, groups, queues, and form customizations-objects that have dependencies on other objects that are defined in sealed management packs-you should create a new management pack to store the custom objects.  

### Export custom management packs  
 Periodically, export your customized management packs from the Service Manager database, and store the backup file on a hard drive. This will ensure that custom management packs are synchronized with the management packs in the Service Manager database. It will also make it possible for you to restore the customizations to the Service Manager database, if necessary.  

### Work across multiple management groups  
 Ensure that you do not make different customizations to the same management pack in different management groups. To implement customizations across multiple management groups, you can import the same customized management pack in the other management groups.  

 For example, if you want to have the same enumerations in multiple management groups, make the change in one management group, and then copy the custom management pack to the rest of the management groups. That way, the version and identity of the management pack is identical in all the management groups.  

## Next steps

- [Work with management packs in the Service Manager console](work-mps-console.md).
- [Work with management packs in the Service Manager Authoring Tool](work-mps-auth-tool.md).
- [Work with management pack XML files](work-mps-xml.md).
