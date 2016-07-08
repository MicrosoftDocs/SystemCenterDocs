---
title: Classes: General Guidelines and Best Practices
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4a7ff61-5a6d-4b11-92f6-4a5131974fc8
 

















---
# Classes: General Guidelines and Best Practices
Use the following guidelines and best practices when you are customizing classes in the System Center 2016 - Service Manager Authoring Tool.  
  
## Naming Conventions for Type Definitions  
 The Service Manager schema model naming convention is based on the .NET namespaces naming convention.  
  
### Basic Naming Conventions  
 The basic naming convention is **CompanyName.TechnologyArea.ProductName.FunctionalityArea.Name**, where:  
  
-   **ProductName** is optional; use it if the definition is independent of any specific product.  
  
-   **FunctionalityArea** is optional; use it if the definition can apply to different areas.  
  
-   **Name** reflects the meaning of the class, not the inheritance hierarchy.  
  
 Examples: **Microsoft.AD.Printer**, **Microsoft.Windows.Computer**, **System.Knowledge.Article**, **System.WorkItem.Incident**, and **System.StarRating.Average**.  
  
### The System Namespace  
 The **System** namespace refers to definitions that are independent of Microsoft and Windows. This usually applies to the base definitions that either Windows applications or Unix applications depend on. These base definitions should be company independent.  
  
 Use the following guidelines for the System prefix:  
  
-   **System.Computer** represents any type of computer, and it is not vendor specific.  
  
-   Use the **System** prefix if you expect others to define schemas on top of that namespace.  
  
-   Note that **Microsoft.Windows.Computer** does not start with **System**, although most Windows applications \(regardless of the vendor that defines it\) rely on this definition.  
  
### Best Practices for Naming Classes  
 Use the following best practices when you are naming classes:  
  
-   Do not create two separate classes \(even if they are in two different management packs\) that would result in identical key values being stored for different objects of the two classes.  
  
-   When you are extending a class, always ensure that the class extension names are unique across management packs. If possible, use meaningful class extension names.  
  
-   When you are extending a class, do not define a property with an ID that is already in use in that class.  
  
-   Do not use periods in names of properties of a custom class.  
  
-   If you add a custom named calculation when you author a cube, preface the name of the named calculation with NC\_. This will reduce the possibility of using a name of a property that already exists.  
  
## Do Not Create Too Many Classes  
 Creating too many classes can result in needless complexity with minimal value. A good rule is to use the least number of classes to achieve the desired results. Other than abstract classes, if a class is not going to be the target of any workflow or be used to store data, it probably should not be created. Also, if two classes are similar, consider using a single class for both of them, possibly by using a property that can hold the values for any differences.  
  
## Do Not Use Properties That Update Too Frequently  
 Property values should change rarely after they are first populated. A possible cause for frequent property value changes is a custom connector or any other customization that programmatically updates the Service Manager database. These scenarios can potentially cause property values to update too frequently, such as every 10 to 15 minutes or less for a large number of objects.  
  
 Such frequent changes to property values might slightly impact the performance of the workflows, and they might have other performance impacts. This is because the system keeps track of those changes in history. Also, depending on the property being changed, these changes can add a significant amount of data to be processed and stored by the data warehouse.  
  
## Do Not Extend an Abstract Class  
 In System Center 2012 - Service Manager, you cannot extend an abstract class. If you need to extend an abstract class, you can do either of the following:  
  
-   Create a new class with the properties you want to add, and then create a relationship between the new class and the abstract class.  
  
-   Extend each of the relevant concrete classes that derive from the abstract class.  
  
## Improve Simple Search for Work Item Classes  
 When you define a custom class that is derived from the “**System.WorkItem**” class, we recommend that you store the **DisplayName** property of that class in the following format: **WorkItem.ID\<SPACE\>WorkItem.Title**.  
  
 This improves simple search. Simple search searches only the **DisplayName** property, and by explicitly including the **Title** property value and the **ID** property value in the **DisplayName** property value, the results of simple search are improved. This is because the user can search either by a word in the title or by ID.  
  
## See Also  
 [Classes: Customizing and Authoring](../Topic/Classes:%20Customizing%20and%20Authoring.md)
