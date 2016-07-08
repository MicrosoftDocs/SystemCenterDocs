---
title: Changes to the System Center Common Schema
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cea233ab-0da0-42e7-993a-9d735997f90e
 

















---
# Changes to the System Center Common Schema
System Center 2012 - Service Manager includes an updated version of the System Center Management Pack Schema. This schema is now called the System Center Common Schema, and it includes a number of improvements and additions that are intended to enhance existing functionality and enable Service Manager features. This topic describes the changes to the System Center Common Schema.  
  
 For more information about Service Manager management packs and for more XML samples, see [Directly Authoring a Management Pack File to Manage Projectors](../../../sm/manage/author/Directly-Authoring-a-Management-Pack-File-to-Manage-Projectors.md).  
  
## Properties and Property Restrictions  
 The common schema extends classes through several new property types. These property types include the binary, enumerator, and autoincrement types.  
  
 In addition, you can define restrictions on certain property values. For example, you can define a regular expression restriction on a string property value. In the following example, the **BuildingName** property has a regular expression restriction that is defined so that only a value that contains the word "Building" followed by a space and a number is considered valid.  
  
```  
  
<ClassType ID="Lobby" Accessibility="Public" Base="System!System.Entity">  
   <Property ID="Id" Type="int" Key="true" />  
   <Property ID="BuildingName" Type="string" RegEx="Building [0-9]+" />  
</ClassType>  
  
```  
  
## Images  
 Images are not stored inside a management pack. Therefore, the **\<PresentationTypes\>** section of the management pack no longer contains the **\<Images\>**, **\<Image\>**, or **\<ImageData\>** tags. Instead, use an image resource.  
  
```  
<Resources>  
   <Image ID="TestLibrary.Resources.Image1" Accessibility="Public" FileName="image.png"/>  
</Resources>  
  
```  
  
## Enumerations  
 The common schema supports enumerations. Enumerations are a tree of values that you can use to restrict the value of a property or attribute.  
  
 Each enumeration has a required unique **ID** attribute and an optional **Parent** attribute.  
  
 In the following example, the **XBoxState** enumeration is defined with three possible values: Running, Stopped, and Error.  
  
```  
  
<EnumerationTypes>  
   <EnumerationValue ID="XBoxState" Accessibility="Public"/>  
   <EnumerationValue ID="XBoxState.Running" Parent="XBoxState" Accessibility="Public"/>  
  <EnumerationValue ID="XBoxState.Stopped" Parent="XBoxState" Accessibility="Public"/>  
   <EnumerationValue ID="XBoxState.Error" Parent="XBoxState" Accessibility="Public" />  
   <EnumerationValue ID="XBoxState.Error.RROD" Parent="XBoxState.Error" Accessibility="Public" />  
</EnumerationTypes>  
  
```  
  
 In the following example, the **Xbox** class defines an **enum** property of type **XBoxState**.  
  
```  
  
<ClassType ID="XBox" Accessibility="Public" Base="System!System.ConfigItem" Hosted="true">  
   <Property ID="Id" Type="int" Key="true" />  
   <Property ID="Name" Type="string" />  
   <Property ID=“State" Type="enum" EnumType=“XBoxState" />  
</ClassType>  
  
```  
  
## Relationships  
 The functionality of relationship definitions has been enhanced in the common schema. The **RelationshipType** type now has **Source** and **Target** subelements with **ID** properties that can be used as display names. In addition, you can define minimum and maximum cardinality for both the source and target \(for example, 1\-to\-1 or 0\-to\-many relationships\).  
  
 Cardinality is not enforced by the management pack validation process, but it is intended to help define user interfaces for the management pack. For example, cardinality can be checked to determine whether a field can be represented in a form by a text box or by a list.  
  
> [!IMPORTANT]  
>  Any **MaxCardinality** value that is defined as greater than 1 is processed as unlimited.  
  
 If you add a new relationship type from your own management pack, users must have sufficient privileges to update all properties of the source and target class instances of the relationship type in order to create an instance of the new relationship type.  
  
 In the following example, a hosting relationship \(called **HasXboxes**\) between the **Lobby** type and the **Xbox** type is defined. In this relationship definition, each **Lobby** type can have multiple **Xbox** types.  
  
```  
  
<RelationshipType ID="HasXBboxes" Accessibility="Public" Base="System!System.Hosting">  
   <Source ID="Source" Type="Lobby" />  
   <Target ID="Target" Type="Xbox" MinCardinality="0" MaxCardinality="9999" />  
</RelationshipType>  
  
```  
  
## Combination Classes  
 Combination classes represent an aggregation of multiple related types in the management pack, similar to views that are defined in a Microsoft SQL Server database that can return data from multiple tables. Combination classes store and retrieve all the aggregated data in one operation to the database, and they can make it easier to define user interfaces for a management pack.  
  
 In the following example, a projection is defined for an incident management view. This projection combines several different components that are related to an incident into one unit that can be used more easily for forms and for database operations.  
  
```  
  
<TypeProjections>  
   <TypeProjection ID="System.WorkItem.Incident.View.ProjectionType"  
      Accessibility="Public" Type="Incident!System.WorkItem.Incident">  
      <Component Alias="AffectedUser"  
Path="$Target/Path[Relationship='SMCore!System.WorkItemCreatedForUser']$"/>  
      <Component Alias="AssignedUser" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
   </TypeProjection>  
   <TypeProjection ID="System.WorkItem.Incident.View.DCMProjectionType" Accessibility="Public" Type="Incident!System.WorkItem.Incident.DCMIncident">  
      <Component Alias="AffectedUser" Path="$Target/Path[Relationship='SMCore!System.WorkItemCreatedForUser']$"/>  
      <Component Alias="AssignedUser" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
      <!--Baseline and Configuration Item Information-->  
      <Component Alias="AffectedComputer" Path="$Target/Path[Relationship='Incident!System.WorkItem.Incident.DCMIncident.Refers.NonComplianceComputer']$"/>  
   </TypeProjection>  
   <TypeProjection ID="System.WorkItem.ChangeRequestViewProjection" Accessibility="Public" Type="System.WorkItem.ChangeRequest">  
      <Component Alias="AssignedTo" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
   </TypeProjection>  
   <TypeProjection ID="System.WorkItem.ChangeRequestProjection" Accessibility="Public" Type="System.WorkItem.ChangeRequest">  
      <Component Alias="Activity" Path="$Target/Path[Relationship='SMActivity!System.WorkItemContainsActivity']$">  
         <Component Alias="ActivityAssignedTo" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
         <Component Alias="ActivityRelatedWorkItem" Path="$Target/Path[Relationship='SMCore!System.WorkItemRelatesToWorkItem']$">  
            <Component Alias="ActivityRelatedWorkItemAssignedTo" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
         </Component>  
         <Component Alias="ActivityRelatedConfigItem" Path="$Target/Path[Relationship='SMCore!System.WorkItemRelatesToConfigItem']$"/>  
         <Component Alias="ActivityAboutConfigItem" Path="$Target/Path[Relationship='System!System.WorkItemAboutConfigItem']$"/>  
         <Component Alias="ActivityFileAttachment" Path="$Target/Path[Relationship='System!System.WorkItemHasFileAttachment']$">  
            <Component Alias="ActivityFileAttachmentAddedBy" Path="$Target/Path[Relationship='System!System.FileAttachmentAddedByUser']$"/>  
         </Component>  
         <Component Alias="Reviewer" Path="$Target/Path[Relationship='SMActivity!System.ReviewActivityHasReviewer']$">  
            <Component Alias="User" Path="$Target/Path[Relationship='SMActivity!System.ReviewerIsUser']$"/>  
            <Component Alias="VotedBy" Path="$Target/Path[Relationship='SMActivity!System.ReviewerVotedByUser']$"/>  
         </Component>  
      </Component>  
      <Component Alias="CreatedBy" Path="$Target/Path[Relationship='SMCore!System.WorkItemCreatedByUser']$"/>  
      <Component Alias="AssignedTo" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
      <Component Alias="CreatedFor" Path="$Target/Path[Relationship='SMCore!System.WorkItemCreatedForUser']$"/>  
      <Component Alias="RelatedWorkItem" Path="$Target/Path[Relationship='SMCore!System.WorkItemRelatesToWorkItem']$">  
         <Component Alias="RelatedWorkItemAssignedTo" Path="$Target/Path[Relationship='SMCore!System.WorkItemAssignedToUser']$"/>  
      </Component>  
      <Component Alias="RelatedConfigItem" Path="$Target/Path[Relationship='SMCore!System.WorkItemRelatesToConfigItem']$"/>  
      <Component Alias="AboutConfigItem" Path="$Target/Path[Relationship='System!System.WorkItemAboutConfigItem']$"/>  
      <Component Alias="FileAttachment" Path="$Target/Path[Relationship='System!System.WorkItemHasFileAttachment']$">  
         <Component Alias="FileAttachmentAddedBy" Path="$Target/Path[Relationship='System!System.FileAttachmentAddedByUser']$"/>  
      </Component>  
   </TypeProjection>  
   <TypeProjection ID="System.FileAttachmentProjection" Accessibility="Public" Type="System!System.FileAttachment">  
      <Component Alias="FileAttachmentAddedBy" Path="$Target/Path[Relationship='System!System.FileAttachmentAddedByUser']$"/>  
   </TypeProjection>  
</TypeProjections>  
```  
  
## Console Tasks  
 Console tasks are extended in the common schema. Previously, console tasks were simple pointers to an application directory and executable file name. Console tasks are now implemented as handler code in a Microsoft .NET Framework assembly. The handler code references the assembly that houses the code, the handler name, and a list of named values that can be passed as arguments to the handler.  
  
 In the following example, the **Some.Handler.Name** handler is defined in the **MyLibrary.Resources.Assembly** assembly. A list of handler parameters and their values is also defined.  
  
```  
<ConsoleTask ID="MyLibrary.ConsoleTasks.T1"  
    Accessibility="Public"  
     Target="System!System.Entity"  
     Enabled="true"  
     RequireOutput="true">  
   <Assembly>MyLibrary.Resources.Assembly1</Assembly>  
   <Handler>Some.Handler.Name</Handler>  
   <Parameters>  
      <Argument Name="Application">cmd.exe</Argument>  
      <Argument Name="WorkingDirectory">%TEMP%</Argument>  
      <Argument>test1</Argument>  
      <Argument>test2</Argument>  
   </Parameters>  
</ConsoleTask>  
```  
  
## Resources  
 Binary data is not stored directly in a management pack. Instead, metadata about the binary resource is stored in the management pack, and the actual binary data is stored externally in a resource file. The metadata includes a unique identifier, the file name, the creation data, the modified date, and accessibility information.  
  
 Binary data can include generic resources, images, assemblies, report definitions, and forms. The following example shows a generic XML resource, an assembly resource, and a report resource.  
  
```  
  
<Resources>  
   <Resource ID="TestLibrary.Resources.Test1" Accessibility="Public" FileName="res1.xml"/>  
   <Resource ID="TestLibrary.Resources.Test2" Accessibility="Public" FileName="res2.xml"/>  
   <Assembly ID="TestLibrary.Resources.Assembly1" Accessibility="Public" QualifiedName="Baz, Version=1.0.0.0" FileName="baz.dll"/>  
   <Assembly ID="TestLibrary.Resources.Assembly2" Accessibility="Public" QualifiedName="Yoyo, Version=1.0.0.0" FileName="yoyo.dll">  
      <Dependency ID="TestLibrary.Resources.Assembly1"/>  
   </Assembly>  
   <ReportResource ID="TestLibrary.Resources.Report1" Accessibility="Public" MIMEType="text/xml" FileName="res1.xml"/>  
   <Image ID="TestLibrary.Resources.Image1" Accessibility="Public" FileName="image.png"/>  
</Resources>  
  
```  
  
## Forms  
 Forms are defined in a management pack. You can use forms to view and modify a single instance of a type or combination class.  
  
 Forms are based on the Windows Presentation Framework \(WPF\), and they are defined in assemblies. The assembly and class that contain the form implementations for a management pack are included in the resources section of the management pack. As with any binary resource in a management pack that uses the new common schema, the management pack itself does not contain the binary data for the form. Only the resource manifest is specified in the management pack.  
  
 You can specify your own configuration information for the form in the management pack. In the following example, the Configuration section contains a **ShowXboxes** property. This configuration information is not evaluated by the management pack verification process; it is only interpreted by the form implementation.  
  
```  
  
    <Forms>  
   <Form ID="LobbyForm" Target="Projection" Assembly="FormAssembly“ TypeName="MyFormClass">  
   <Configuration>  
      <ShowXboxes>yes</ShowXboxes>  
   </Configuration>  
   </Form>  
</Forms>  
  
```  
  
## See Also  
 [Directly Authoring a Management Pack File to Manage Projectors](../../../sm/manage/author/Directly-Authoring-a-Management-Pack-File-to-Manage-Projectors.md)   
 [Forms: General Guidelines and Best Practices](../Topic/Forms:%20General%20Guidelines%20and%20Best%20Practices.md)
