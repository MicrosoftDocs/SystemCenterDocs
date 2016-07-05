---
title: About Outriggers in the Data Warehouse
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30637bf9-375e-460f-8005-06defefc79cc
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
# About Outriggers in the Data Warehouse
An outrigger in the data warehouse in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] is essentially a list that can logically group together a set of values. The following tables show two examples that display a logical grouping of values that denote Priority and Windows Operating Systems.  
  
|Priority|  
|--------------|  
|Low|  
|Medium|  
|High|  
  
|Windows Operating Systems|  
|-------------------------------|  
|Windows XP|  
|Windows Vista|  
|Windows 7|  
  
 An outrigger is useful in two ways:  
  
-   You can use discrete values from an outrigger as a drop\-down menu for a report parameter when you create and view reports in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
-   You can use outrigger values to group data in reports for advanced analysis.  
  
 Outriggers in the data warehouse can target one or more class properties and consolidate them into a single set of discrete values. These properties can only be a data type String or ManagementPackEnumeration. When they are based on an enumeration, outriggers also preserve the hierarchy. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] does not support an outrigger that is defined on a data type other than String or ManagementPackEnumeration.  
  
 Although the benefit of defining an outrigger on an enumeration is evident, an advantage of defining an outrigger on a string column is that the data warehouse infrastructure combines the distinct values of a property from the instance space into a small list. You can then use the list in an easy\-to\-use drop\-down list in a report. A good example of a string\-based outrigger is the `Manufacturer` property on the **Computer** class, which is modeled as a string in the Service Manager database. By defining an outrigger on that property, Service Manager provides the ability to select a value from the drop\-down list, instead of searching among manufacturers that you procured your computers from.  
  
 To view an example of how an outrigger is used in a report in the parameter header, open the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]; navigate to **Reporting, Activity Management**; and then run the **Activity Distribution** report. Next, review the **Status** list to see the values of the outrigger. You can see how the outrigger was modeled in the management pack in the following example. Note the class **System.WorkItem.Activity**, which is defined in the System.Workitem.Activity.Library management pack:  
  
```  
<ClassType ID="System.WorkItem.Activity" Accessibility="Public" Base="WorkItem!System.WorkItem" Hosted="false" Abstract="true">   
< Property ID="SequenceId" Type="int" />     
<Property ID="Notes" Type="richtext" MaxLength="4000" />     
<Property ID="Status" Type="enum" EnumType="ActivityStatusEnum" />     
<Property ID="Priority" Type="enum" EnumType="ActivityPriorityEnum" />     
<Property ID="Area" Type="enum" EnumType="ActivityAreaEnum" />    
<Property ID="Stage" Type="enum" EnumType="ActivityStageEnum" />                      
</ClassType>  
```  
  
 Next, you might want to define an outrigger based on the enumeration property `Status`. The following example shows how you can define an outrigger in a management pack of your choice:  
  
```  
<Outrigger ID="ActivityStatus" Accessibility="Public">   
<Attribute ID="Status" PropertyPath="$Context/Property[Type='CoreActivity!System.WorkItem.Activity']/Status$" />     
</Outrigger>  
```  
  
 As described previously, you—the management pack author—can define an outrigger on one or more class properties. Each class property is modeled by a corresponding attribute in the outrigger. The following is an example of enumeration\-based outrigger visualization. In this example, Activity Status is based on ActivityStatusEnum:  
  
```  
<EnumerationTypes>   
<EnumerationValue ID="ActivityStatusEnum" Accessibility="Public" />   
<EnumerationValue ID="ActivityStatusEnum.Ready" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="5.0" />   
<EnumerationValue ID="ActivityStatusEnum.Active" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="10.0" />    
<EnumerationValue ID="ActivityStatusEnum.OnHold" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="15.0" />   
<EnumerationValue ID="ActivityStatusEnum.Completed" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="20.0" />   
<EnumerationValue ID="ActivityStatusEnum.Failed" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="25.0" />   
<EnumerationValue ID="ActivityStatusEnum.Cancelled" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="30.0" />   
<EnumerationValue ID="ActivityStatusEnum.Rerun" Parent="ActivityStatusEnum" Accessibility="Public" Ordinal="35.0" />     
...   
</EnumerationTypes>  
```  
  
 Each of the values is included in the outrigger’s set of discrete values. The following table lists the column ID and ActivityStatusValue from the ActivityStatus outrigger, which contains all the enumeration values from ActivityStatusEnum.  
  
|ID|ActivityStatusValue|  
|--------|-------------------------|  
|ActivityStatusEnum.Completed|Completed|  
|ActivityStatusEnum|Activity Status|  
|ActivityStatusEnum.Active|In Progress|  
|ActivityStatusEnum.OnHold|On Hold|  
|ActivityStatusEnum.Rerun|Rerun|  
|ActivityStatusEnum.Failed|Failed|  
|ActivityStatusEnum.Ready|Pending|  
|ActivityStatusEnum.Cancelled|Cancelled|  
  
 In the previous table, the ID column from the outrigger contains all the EnumerationValue IDs from the ActivityStatus enumeration type. The ActivityStatusValue is the actual user\-friendly display name that appears in the report drop\-down menus.  
  
 The following example provides further detail about how to construct and model an outrigger. Again, the outrigger ActivityStatus is used as an example:  
  
```  
<Outrigger ID="ActivityStatus" Accessibility="Public">  
<Attribute ID="Status" PropertyPath="$Context/Property[Type='CoreActivity!System.WorkItem.Activity']/Status$" />     
</Outrigger>  
```  
  
 The following table describes the attributes for the \<Outrigger\> tag.  
  
|Attribute|Description|  
|---------------|-----------------|  
|ID|A unique identifier for the outrigger element. This is also the table name of the outrigger in the data warehouse and datamart.|  
|Accessibility|This element should always be set to Public.|  
  
 Each \<Outrigger\> parent tag contains one or more \<Attribute\> subelement tags. The following table describes the attributes for this tag.  
  
|Attribute|Description|  
|---------------|-----------------|  
|ID|A unique identifier for each outrigger attribute|  
|PropertyPath|PropertyPath syntax, which must uniquely identify the class and attribute that the outrigger attribute is targeting.|  
  
## See Also  
 [Customizing the Data Warehouse](../../../sm/manage/operate/Customizing-the-Data-Warehouse.md)