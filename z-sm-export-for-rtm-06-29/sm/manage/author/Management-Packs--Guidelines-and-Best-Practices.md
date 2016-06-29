---
title: Management Packs: Guidelines and Best Practices
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dee02a8-d162-4acf-8131-a30fc4bb9c0d
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Management Packs: Guidelines and Best Practices
The following guidelines and best practices for working with management packs in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] are described in this topic:  
  
-   Group customizations into separate management packs.  
  
-   Seal model management packs.  
  
-   Create your own custom management packs when possible.  
  
-   Export custom management packs.  
  
-   Work across multiple management groups.  
  
## Group Customizations into Separate Management Packs  
 Group customizations into separate management packs as follows:  
  
-   Store model extensions and presentation extensions in separate management packs.  
  
     We recommend that you store the following objects in a model management pack:  
  
    -   New classes and class extensions, including properties and corresponding icons  
  
    -   New lists  
  
    -   Combination classes  
  
    -   Relationships  
  
    -   Child EnumerationValues that should not be modified  
  
    -   Forms for viewing and editing objects of the defined classes, and the respective assembly resources  
  
-   Group customizations by the solution that you are developing. For example, store incident\-management\-related customizations and settings separately from change\-management\-related customizations and settings.  
  
-   Group customizations based on usage considerations. For example, store customizations that you need to test and deploy as a unit in the same management pack.  
  
## Seal Model Management Packs  
 You should seal management packs that contain base classes and other model objects, on which other definitions in other management packs depend on. Sealing a management pack prevents it from being modified. Also, it is important to seal a management pack so that its definitions are synchronized with the data warehouse database during import. This makes it possible for you to later add customizations \(in another management pack\), such as presentations that depend on the base objects from the sealed management pack.  
  
## Create Your Own Custom Management Packs When Possible  
 Some of the solution\-specific, preimported, unsealed management packs \(“Configuration” management packs\) contain customizable elements for the specific solution. In some cases you must store your customizations in those preimported management packs to ensure that the management pack adheres to the dependency rules. For example, templates that use list values that are defined in a “Configuration” management pack must be stored in that same management pack. This is because the list values that are used are defined in another unsealed management pack, and dependency on unsealed management packs is not supported.  
  
 However, whenever possible we recommend that you create new management packs to store your customizations. Creating your own management pack simplifies transportation of the management pack, and it can simplify an upgrade.  
  
 For example, when you extend a solution by adding objects, such as views, tasks, groups, queues, and form customizations—objects that have dependencies on other objects that are defined in sealed management packs—you should create a new management pack to store the custom objects.  
  
## Export Custom Management Packs  
 Periodically, export your customized management packs from the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, and store the backup file on a hard drive. This will ensure that custom management packs are synchronized with the management packs in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database. It will also make it possible for you to restore the customizations to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, if necessary.  
  
## Work Across Multiple Management Groups  
 Ensure that you do not make different customizations to the same management pack in different management groups. To implement customizations across multiple management groups, you can import the same customized management pack in the other management groups.  
  
 For example, if you want to have the same enumerations in multiple management groups, make the change in one management group, and then copy the custom management pack to the rest of the management groups. That way, the version and identity of the management pack is identical in all the management groups.  
  
## See Also  
 [Management Packs: Working with Management Packs](../Topic/Management%20Packs:%20Working%20with%20Management%20Packs.md)