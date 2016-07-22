---
title: Management Packs: Key Concepts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e6888f7-a895-4ae2-8148-eca3833f57e4
 

















---
# Management Packs: Key Concepts
Before you work with management packs in System Center 2012 - Service Manager, you should be familiar with the following management pack concepts.  
  
## Sealed and Unsealed Management Packs  
 There are two types of management packs:  
  
-   Sealed management packs: A sealed management pack \(.mp file\) cannot be modified.  
  
-   Unsealed management packs: An unsealed management pack \(.xml file\) can be modified.  
  
 Other than lists and forms, objects such as views that are defined in a sealed management pack cannot be customized. Customizing a list that is defined in a sealed management pack includes adding list items. Customizing a form that is defined in a sealed management pack includes adding fields.  
  
 You cannot unseal a management pack that is sealed. To modify objects that are stored in a management pack that you have already sealed, you can modify the original unsealed management pack file from which the sealed management pack was created. Alternatively, you can import the sealed management pack, and export it to a new unsealed management pack, that can be modified. After you import a sealed management pack, you cannot import the unsealed version of the same management pack until you delete the sealed version.  
  
## Model Management Pack  
 A model management pack is a management pack that contains definitions for basic objects, such as classes, combination classes, and relationship types.  
  
 Building model management packs makes it possible for other customizations-typically, customizations that are related to presentation, such as templates, views, and tasks-to be stored in separate management packs that depend on the model extensions. In addition, model management packs are easily transferred into the data warehouse for archiving and reporting purposes.  
  
## Dependencies, Resources, and Bundling of Management Packs  
 A management pack can depend on another management pack that is sealed. For example, a custom template in one management pack can depend on a list that is defined in another management pack. The management pack that contains the base definitions \(such as the list\), on which other definitions depend, must be sealed. A management pack can also require resources, such as a form or an image, that are stored separately.  
  
 When you deploy a management pack that has resource requirements, you must bundle the required resources and the management pack into a single management pack file that can be imported into Service Manager.  
  
 In addition, if a management pack has dependencies on other management packs, those dependent management packs must be imported first. As an alternative, you can bundle the dependent management packs along with the required resources and the depending management pack.  
  
 For more information about how to bundle a management pack with its resources and dependent management packs, see the [How to Bundle Management Packs and Resource Files](../../../sm/manage/author/How-to-Bundle-Management-Packs-and-Resource-Files.md).  
  
## Management Pack Customization  
 You might have to customize and extend the default, preimported management packs so that information technology \(IT\) professionals and other users in your organization can extend existing solutions and customize them to meet your business and customer needs. To customize features in Service Manager, you can add new objects or modify the objects that are related to that feature.  
  
 A customization to an object is a modification that applies to the base definition of the object. For customizations to be able to be applied to a base definition, the base definition must be stored in a sealed management pack. And because it is not possible to save customizations in the sealed management pack that contains the object's base definition, you always have to use or create another unsealed management pack to store customizations.  
  
 Typically, when you customize objects from a default, preimported management packs, you work with two management packs. The first management pack is the sealed management pack that contains the base definitions of objects, and the second management pack, which is initially unsealed, contains the customizations to the base object. In this case, the management pack with the customization depends on the management pack that contains the base definition of the object.  
  
 When you customize objects that are defined in an unsealed management pack, you can use the same management pack to store the customizations.  
  
 After you complete the customizations, you can deploy them by importing the management pack into Service Manager. During an import of a sealed management pack, Service Manager synchronizes the Service Manager database and the data warehouse database with the definitions from the management pack. During an import of an unsealed management pack, other than list definitions, Service Manager synchronizes only the Service Manager database with the definitions from the management pack. List definitions in an unsealed management pack are synchronized to both databases.  
  
## See Also  
 [Management Packs: Working with Management Packs](../Topic/Management%20Packs:%20Working%20with%20Management%20Packs.md)
