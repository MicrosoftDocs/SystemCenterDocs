---
title: About Modeling OLAP Cubes in Management Packs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f6da179-5a54-46fb-adc4-3fcaa7bd9864
 

















---
# About Modeling OLAP Cubes in Management Packs
The ability to define customized management pack elements was used to model the online analytical processing \(OLAP\) cube management pack elements that are included in System Center 2012 - Service Manager. These management pack elements make it possible for the user to declaratively define and customize an OLAP cube at a higher level of abstraction. Based on the definition, the deployment of these management pack elements create the correct relationships, components, and fundamental building blocks of the OLAP cube at a greater level of detail, without any further user guidance. The following are the two main management pack elements that are included in OLAP cubes:  
  
-   SystemCenterCube  
  
-   CubeExtension  
  
## SystemCenterCube  
 The SystemCenterCube element defines the OLAP cube to a varying degree of detail, depending on your specific needs. This element contains the following subelements:  
  
-   MeasureGroup  
  
-   Substitution  
  
-   CustomMDX  
  
-   NamedCalculation  
  
-   Measure  
  
-   KPI  
  
-   Action \(however, only drill\-through actions are supported currently\)  
  
-   ManyToManyRelationship  
  
### MeasureGroup  
 Each OLAP cube contains a collection of facts that exist in the data mart, where each member in the collection corresponds to a measure group. Each measure group must have its own unique name within the OLAP cube. However, a single fact may correspond to multiple measure groups in an OLAP cube. For example, the abstract relationship *WorkItemAssignedToUser* may be defined three times in an OLAP cube, with the unique measure group names of *ChangeRequestAssignedToUser*, *IncidentAssignedToUser*, and *ProblemAssignedToUser*. As described in the in the [Substitution](../../../sm/manage/operate/About-Modeling-OLAP-Cubes-in-Management-Packs.md#BKMK_Substitutions) section, you can customize the fact so that only change requests, incidents, and problems are included in the respective measure group for the OLAP cube.  
  
 The following example shows the management pack element for the IncidentAssignedToUser measure group:  
  
```  
<MeasureGroup DateDimAlias="IncidentAssignedToUserDateDim" MeasureGroupName-"IncidentAssignedTouser" Fact="DWBase!WorkItemAssignedToUserFact"/>  
```  
  
 When the OLAP cube is deployed, the dimension, outriggers, and foreign key relationships are automatically calculated and the data source view will be updated with these new elements. The following table describes measure group attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|DateDimAlias|No|String|The name of the date dimension that will filter on this measure group. If no alias is defined, the date dim role playing name will automatically be "\(MeasureGroupName\)\_DateDim"|  
|MeasureGroupName|Yes|String|The name of the measure group in the cube. This name must be unique within the cube.|  
|Fact|Yes|Relationship or CustomFact|The target of the measure group, which must be a fact in the data warehouse.|  
  
##  <a name="BKMK_Substitutions"></a> Substitution  
 Because relationship facts in the data warehouse may target abstract relationships and dimensions, you need to substitute in concrete dimensions so that the measure group will contain only instances that you want to browse.  
  
 This is illustrated in the following example.  
  
```  
<Substitution MeasureGroupName="IncidentAssignedTouser" RelationshipEndpoint="Source" Relationship="Workitem!System.WorkItemAssignedToUser" TargetDimension="DWBase!WorkItemDim" ReplacementDimension="IncidentDW!IncidentDim"/>  
```  
  
 In this example, the *IncidentAssignedToUser* measure group points at the *WorkitemAssignedToUser* relationship. This relationship, however, will not only contain incidents, but it will also contain change requests and problems that have also been assigned to any users. To ensure that this measure group only contains incidents, Service Manager substitutes *WorkItemDim* with *IncidentDim*. This means that the table that is created in the data source view for the measure group automatically performs an inner join on WorkItemDim with IncidentDim and returns only those instances where a join is valid based on the EntityDimKey or BaseManagedEntityId.  
  
 Remember that you must define the relationship endpoint where you want to perform the substitution. This element is required because it is possible that the source and endpoint dimensions are identical and a methodology is needed to uniquely identify which dimension to substitute. An example of such a relationship is *WorkItemRelates to WorkItem*.  
  
 The substitution element is also used to define alias dimensions for the cube. In other words, you can define an alias name for a dimension, but it is not required to actually substitute a dimension. In effect, the substitution in this case is not on the dimension but on the cube dimension or alias dimension name, as shown in the following example:  
  
```  
<Substitution MeasureGroupName="IncidentAssignedToUser" RelationshipEndpoint="Target" Relationship="Workitem!System.WorkItemAssignedToUser" AliasTargetDimensionAs="AssignedToUserDim" TargetDimension="DWBase!UserDim"/>  
```  
  
 In this example, the alias cube dimension name is *AssignedToUserDim*. This is the name of the dimension that will be used to actually filter on this cube. By allowing users to define alias names, names can be specifically tailored to enable the desired, many\-to\-many relationships in the cube. This makes more advanced filtering and analytical capabilities possible.  
  
 Finally, substitutions are valid not only for relationship facts but for custom facts as well. In this scenario, the relationship endpoint would be set to *None*. The following table describes substitution attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|MeasureGroupName|Yes|String|The measure group name on which to perform the substitution|  
|RelationshipEndPoint|Yes|\(Target, Source, None\)|The endpoint of the relationship to perform the substitution. By default, the value is None for custom facts.|  
|Relationship|No|ManagementPackRelationship|The relationship to use for the substitution.|  
|AliasTargetDimensionAs|No|String|The alias name of the original targeted dimension|  
|AliasReplacementDimensionsAs|No|String|The alias name for the substituted dimension|  
|DimensionAlias|No|ManagementPackDimension|The dimension alias from a custom fact if one exists|  
  
## Custom MDX  
 You can use custom Multi\-Dimensional Expression \(MDX\) scripts to modify and tailor the OLAP cube to the exact specifications that meet your needs. Because Service Manager are model based, it is impossible to determine all your possible semantic needs when taking into account the wide spectrum of requirements and exact specifications for the domain\-specific business needs of a particular user. Custom MDX makes it possible for you to define MDX scripts that will be applied to the OLAP cube to enable specific scenarios that users need to measure and instrument.  
  
## Named Calculation  
 You can use named calculations to define new attributes on a dimension that a custom measure can later target. This makes it possible for you to extend the dimensional schema and customize the schema to fit your exact needs. The following example is from the SystemCenterWorkItemsCube:  
  
```  
<NamedCalculation ID="IncidentsPastTargetResolutionTime" Target="IncidentDW!IncidentDim" ColumnType="Int">  
<Calculation>(case when ( (([Status] = 'IncidentStatusEnum.Resolved' OR [Status] = 'IncidentStatusEnum.Closed') AND ResolvedDate > TargetResolutionTime) OR (([Status] != 'IncidentStatusEnum.Resolved' AND [Status] != 'IncidentStatusEnum.Closed') AND GETUTCDATE() > TargetResolutionTime)) then 1 else 0 end )</Calculation>  
</NamedCalculation>  
```  
  
 In this example, the Incident dimension contains data, such as the status of the incident and the target resolution time. However, there is no native measure that calculates the number of incidents that exceeded the target resolution time, although this type of data is very useful for a systems administrator. You can create this scenario using a named calculation and aggregate the data so that a custom measure can target the new attribute and then present the information to an end user.  
  
 Remember that Service Manager supports only NamedCalculation targeting dimensions. NamedCalculation cannot target facts. The following table describes named calculation attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|ID|Yes|String|Name of the named calculation.|  
|Target|Yes|ManagementPackDimension|The target dimension for the measure|  
|ColumnType|Yes|\(Int, Double\)|The Structured Query Language \(SQL\) type of the column|  
|Type|No|\(Count, Sum\)|The type of the measure|  
  
 The subelement \<Calculation\> contains, as its value, the definition of the named calculation. The value is stored as an MDX expression.  
  
## Measure  
 You can use custom measures to aggregate and display data based on numeric attributes from dimensions. Service Manager does not support custom measures based on facts. Continuing with the example of he Named Calculation above, Service Manager defines a custom measure on IncidentsPastTargetResolutionTime as the following:  
  
```  
<Measure ID="IncidentsPastTargetResolutionTimeCount" Target="IncidentDW!IncidentDim" Type="Sum" Property="IncidentsPastTargetResolutionTime"/>  
```  
  
 Reviewing this XML code, the target of the measure is the IncidentDimension and the specific property is *IncidentsPastTargetResolutionTime*. This is the custom property that was defined previously. Custom measures can target either native or calculated properties in the dimension.  
  
 Finally, the measure type is defined to be a sum. Possible values for a measure type include Sum and Count. Because of performance considerations, Service Manager Distinct Count measure types are not allowed. The following table describes measure attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|ID|Yes|String|Name of the measure|  
|Target|Yes|ManagementPackDimension|The target dimension for the measure|  
|Property|Yes|String|The targeted dimension property|  
|Type|No|\(Count, Sum\)|The type of the measure|  
  
## ManyToManyRelationship  
 The ManyToManyRelationship makes it possible for you, the cube designer, to add custom, many\-to\-many dimensions to an OLAP cube, for enabling advanced analytic scenarios. Defining many\-to\-many relationships is beyond the scope of this document. However, you can investigate this concept and its benefits. For more information about the ManyToManyRelationship, see [The Many\-to\-Many Revolution 2.0](http://go.microsoft.com/fwlink/p/?LinkId=246670).  
  
 During cube deployment, Service Manager automatically adds many\-to\-many dimensions to the cube for all "one\-hop" relationships, without any interaction from you. However, Service Manager does not add many\-to\-many dimensions for cascading \(multi\-hop\) relationships because of the exponential increase of possible relationships that could be added. Adding all these relationships can significantly degrade performance when the OLAP cube is browsed. This is because the aggregations of many\-to\-many relationships are generally not calculated during processing and because the joins will be evaluated while the OLAP cube is browsed. If you want a specific, cascading, many\-to\-many relationship, you can define the relationship using a management pack element and it will be added to the OLAP cube. Conversely, you can overwrite an automatically generated, many\-to\-many relationship to use a different intermediate measure group in instances in which multiple intermediate groups exist. In this case, Service Manager automatically uses the first group that is encountered. The following is an example of a many\-to\-many management pack relationship element:  
  
```  
<ManyToManyRelationship CubeDimension="ServiceDim" TargetMeasureGroup="AlertAboutConfigItem" IntermediateMeasureGroup="ServiceContainsConfigItem" />  
```  
  
 The following table describes many to many relationship attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|CubeDimension|Yes|String|Name of the many\-to\-many cube dimension|  
|TargetMeasureGroup|Yes|String|The target measure group to create the many\-to\-many relationship|  
|IntermediateMeasureGroup|Yes|String|The intermediate measure group to create the many\-to\-many relationship|  
  
## KPI  
 Organizations and businesses can use key performance indicators \(KPIs\) to quickly estimate the health of an enterprise by measuring its progress toward a predefined goal. Each KPI has a target value and an actual value. The target value is a quantitative goal that is critical to the success of the organization. Large amounts of data are filtered to one discrete value that can be used to monitor performance and progress towards goals and benchmarks. Some examples of KPIs are a college having a goal that 90% of their students graduate within four years or a basketball team with a goal of causing the opposing team to shoot less than 50&nbsp;percent for a game. You can use a scorecard to show a group of KPIs, providing in one instantaneous snapshot the overall health of a business. The following is an example KPI:  
  
```  
<KPI ID="IncidentResolutiuonKpi" >  
<Caption> The ratio of incidents resolved </Caption>  
<Value>IIF(([Measures].[IncidentDimCount])> 0,([Measures].[IncidentsResolvedCount]/[Measures].[IncidentDimCount]),null)</Value>   
<Goal>1.0</Goal>   
<GreenThreshold> 0.75</GreenThreshold>  
<YellowThreshold>0.5 </YellowThreshold>  
<Direction>Up</Direction>  
<StatusGraphic>Thermometer</StatusGraphic>   
</KPI>  
```  
  
 The following table describes KPI attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|ID|Yes|String|Name of the KPI|  
|Caption|Yes|String|Description of the KPI|  
|Value|Yes|String|MDX script defining the numeric value of the KPI|  
|Goal|Yes|String|&#x2715The target value of the KPI|  
|Green Threshold|Yes|String \(between 0.1 and 1\)|&#x2715Any number that is above or below this threshold, depending on the direction, is marked as green in the status symbol.|  
|&#x2715Yellow Threshold|Yes|String \(between 0.1 and 1\)|Any number that is above or below the threshold, depending on the direction, but does not meet the green threshold is marked as yellow in the status symbol. A number that does not meet the yellow threshold is marked as red in the status symbol.|  
|&#x2715Direction|Yes|&#x2715\(Up, Down\)|&#x2715If the direction is up, any numbers above the green or yellow threshold are marked with the corresponding symbol. Similarly for down, numbers below the green or yellow thresholds are marked with the corresponding symbol.|  
|&#x2715Status Graphic|Yes|&#x2715\(Shapes, TrafficLight, RoadSigns, Gauge, ReversedGauge, Thermometer, Cylinder, Faces, VarianceArrow\)|&#x2715The symbol that will represent the KPI.|  
  
## Action  
 Actions are events that you can trigger on an OLAP cube when you are accessing data in the cube. Only drill\-through actions are supported by Service Manager. The following is an example of an action:  
  
```  
<Action ID="DrillThroughOnWICreatedByUser" MeasureGroupName="CreatedByUser" ActionType="DrillThrough">   
<DrillThroughColumns CubeDimension="WorkItemCreatedByUser_UserDim">   
<Property PropertyName="FirstName" />   
<Property PropertyName="LastName" />   
<Property PropertyName="Company" />   
<Property PropertyName="Department" />   
<Property PropertyName="Office" />   
</DrillThroughColumns>   
</Action>  
```  
  
 The following table describes actions attributes.  
  
|Attribute|Required|Values|Definition|  
|---------------|--------------|------------|----------------|  
|ID|Yes|String|Name of the drill\-through action|  
|MeasureGroupName|Yes|String|Targeted measure group of the action|  
|ActionType|Yes|\(DrillThrough\)|Type of action. Only drill\-through actions are supported by Service Manager.|  
|CubeDimension|Yes|String|&#x2715The cube dimension that is the target of the action, which must be a slicer on the Measure Group|  
|PropertyName|Yes|String|Attribute of the dimension that is displayed when the drill\-through action is executed|  
  
## CubeExtension  
 The primary purpose of the CubeExtension element is to make it possible for you to modify the OLAP cube after the cube has deployed onto SSAS, without having to uninstall and reinstall the cube. In situations in which the OLAP cube has been fully processed with years of data, recreating the cube is time consuming because all partitions have to be fully reprocessed.  
  
 The CubeExtension element can define the following elements:  
  
-   NamedCalculation  
  
-   ManyToManyRelationship  
  
-   KPI  
  
-   Measure  
  
-   Action  
  
-   CustomMdx  
  
 Each customization that is defined in a CubeExtension element can also be defined in a SystemCenterCube object. The only customization that is not allowed is the addition of facts or measure groups and substitutions to the cube.  
  
## See Also  
 [Understanding OLAP Cubes](../../../sm/manage/operate/Understanding-OLAP-Cubes.md)
