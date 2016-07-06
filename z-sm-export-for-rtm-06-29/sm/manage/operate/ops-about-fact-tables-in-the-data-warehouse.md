---
title: About Fact Tables in the Data Warehouse
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3151e63-94b6-48a9-a5ca-42551b7275d5
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
# About Fact Tables in the Data Warehouse
This topic describes how to define relationship facts in the data warehouse in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. A relationship fact in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse is similar to a relationship in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. You can use a relationship fact to help answer queries, such as the following:  
  
-   Which work items are currently assigned to the user John Smith so that you can determine their status?  
  
-   What is the list of all the computers in the domain that currently have Windows 7 installed so that you can update them to Windows 7 Service Pack 1 \(SP1\)?  
  
-   What are all the review activities that list Samantha Smith as a reviewer so that they can be reassigned because she is on vacation?  
  
 In each of these scenarios, there is a source instance and a target instance that are joined together by a relationship. Without a relationship fact, it is difficult to determine the associations between the instances. Consider the relationship in the Microsoft.Windows.ComputerHostsOperatingSystem in the Microsoft.Windows.Library management pack in the following example:  
  
```  
<RelationshipType ID="Microsoft.Windows.ComputerHostsOperatingSystem" Accessibility="Public" Base="System!System.Hosting">     
<Source ID="Computer" Type="Microsoft.Windows.Computer" />      
<Target ID="OperatingSystem" Type="Microsoft.Windows.OperatingSystem" MaxCardinality="1" />    
</RelationshipType>  
```  
  
 In a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] relationship, the source and target are always modeled by a management pack class. In this relationship, the class Microsoft.Windows.Computer is the source and the class Microsoft.Windows.OperatingSystem is the target. The following information defines the corresponding RelationshipFact based on the Microsoft.Windows.ComputerHostsOperatingSystem relationship:  
  
```  
<RelationshipFact ID="ComputerHostsOperatingSystemFact" Accessibility="Public" Domain="Domain.ConfigurationManagement" TimeGrain="Daily" SourceType="Windows!Microsoft.Windows.Computer" SourceDimension="ComputerDim">     
<Relationships RelationshipType="Windows!Microsoft.Windows.ComputerHostsOperatingSystem" TargetDimension="OperatingSystemDim" />     
</RelationshipFact>  
```  
  
 Notice how the relationship fact defines a source dimension and a target dimension. You might notice that the source and target dimensions target the source and target classes from the original relationship that the relationship fact is modeled on. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] dimensions, see [About Dimensions in the Data Warehouse](../../../sm/manage/operate/About-Dimensions-in-the-Data-Warehouse.md).  
  
 You can use relationship facts by associating two dimensions together, which makes it possible for reports to use the association to display important information from each dimension in relation to the other. For example, you can use the WorkItemAssignedToUser relationship to display information about incidents or change requests for a specific user in the report. This makes it possible for you to navigate in the data to find information that is specific to your needs. This is just one example of how relationship facts are useful in creating specialized views of data in reports.  
  
 The attributes and subelement tags that are required for modeling a relationship fact in a user\-defined management pack are described in the following table for the \<RelationshipFact\> tag.  
  
|Attribute|Description|  
|---------------|-----------------|  
|ID|A unique identifier for the relationship fact element. This is also the table name of the relationship fact in the data warehouse and data mart.|  
|Accessibility|This element should always be set to Public because the deployment process creates system\-derived management packs that refer to this outrigger during the generation of the automated transforms.|  
|Domain|The scope of the relationship fact. Possible values include the following: Instance Management Activity Management,    Incident Management Change Management, and Problem Management.<br /><br /> The value for this attribute must be an enumeration that is a child of the parent Domain enumeration, which is defined in the Microsoft.SystemCenter.Datawarehouse.Base management pack.|  
|TimeGrain|The detail level of the relationship fact. The value must be one of the following: Hourly, Daily, Weekly, or Monthly.|  
|SourceType|The management pack class for the source of the relationship.|  
|SourceDimension|The dimension that targets the source class. This is an optional field. If no SourceDimension is specified, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] automatically finds the dimension that directly targets the source class itself or the closest parent class of the source class in the class hierarchy.|  
  
 In a multiple\-relationship fact, the source dimension always remains the same. However, the target dimension can change, depending on the specific relationship. Every relationship type attribute in a multiple relationship fact must be unique. The following is an example of the relationship fact in the WorkItemAssignedToAndCreatedByUser management pack:  
  
```  
<RelationshipFact ID="WorkItemAssignedToAndCreatedUserFact" Accessibility="Public" Domain="Domain.InstanceManagement" TimeGrain="Daily" SourceType="WorkItem!System.WorkItem" SourceDimension="WorkItemDim">  
<Relationships RelationshipType="WorkItem!System.WorkItemAssignedToUser" TargetDimension="UserDim" />   
<Relationships RelationshipType="WorkItem!System.WorkItemCreatedByUser" TargetDimension="UserDim" />   
</RelationshipFact>  
```  
  
 In this example, you can see that although the target dimension is identical for both relationships, the relationships themselves are unique. Therefore, the relationship fact is valid. For more examples of outriggers, dimensions, and relationship facts, you can examine any of the data warehouse management packs that are included in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. A good example is the base data warehouse management pack named Microsoft.SystemCenter.Datawarehouse.Base.  
  
## See Also  
 [Customizing the Data Warehouse](../../../sm/manage/operate/Customizing-the-Data-Warehouse.md)