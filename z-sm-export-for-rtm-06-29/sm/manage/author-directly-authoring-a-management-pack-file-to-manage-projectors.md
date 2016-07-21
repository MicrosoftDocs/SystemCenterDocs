---
title: Directly Authoring a Management Pack File to Manage Projectors
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6438afdd-c997-4b64-9961-2abc0cac9e9b
 

















---
# Directly Authoring a Management Pack File to Manage Projectors
Management packs are used to direct and extend the functionality of System Center 2012 - Service Manager. This topic uses projectors as an example for describing the various sections of a management pack and for defining the various objects that are needed for managing projectors in an organization.  
  
 This topic includes a complete management pack sample with the necessary extensions to manage projectors in an organization. Also, it describes how to import a management pack using a Windows&nbsp;PowerShell cmdlet.  
  
 This topic describes the following sections of a management pack:  
  
-   The Manifest  
  
-   TypeDefinitions to create class enumerations and relationships  
  
-   Forms  
  
 This topic also describes the following sections of a management pack that contain declarations and definitions for user interface \(UI\) and localization elements:  
  
-   Categories  
  
-   Presentation  
  
-   Class Extensions  
  
## The Manifest Section  
 The first section of a management pack contains the manifest. The manifest identifies the management pack and declares any references to other management packs.  
  
 The following example shows the **Manifest** section of a management pack that was designed to track projectors in an organization.  
  
```  
  
<Manifest>  
  <Identity>  
    <ID>ServiceManager.Projector_Authoring</ID>  
    <Version>7.0.3707.0</Version>  
  </Identity>  
  <Name>Projector Library</Name>  
  <References>  
    <Reference Alias="System">  
      <ID>System.Library</ID>  
      <Version>7.0.3707.0</Version>  
      <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
    </Reference>  
    <Reference Alias="SMConsole">  
      <ID>Microsoft.EnterpriseManagement.ServiceManager.UI.Console</ID>  
      <Version>7.0.3707.0</Version>  
      <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
    </Reference>  
    <Reference Alias="Authoring">  
      <ID>Microsoft.EnterpriseManagement.ServiceManager.UI.Authoring</ID>  
      <Version>7.0.3707.0</Version>  
      <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
    </Reference>  
    <Reference Alias="SMConfig">  
      <ID>ServiceManager.ConfigurationManagement.Library</ID>  
      <Version>7.0.3707.0</Version>  
      <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
    </Reference>  
  </References>  
</Manifest>  
```  
  
> [!IMPORTANT]  
>  In the **References** section, do not use nonalphanumeric values, such as a '.', in the Alias for a reference.  
  
## TypeDefinitions Section-Creating a Class  
 The next section of a management pack contains type definitions. The **TypeDefinitions** section of a management pack contains definitions for classes, enumerations, and relationships that are used by the management pack.  
  
 The following example shows a class that contains information about projectors:  
  
```  
  
<TypeDefinitions>  
    <EntityTypes>  
      <ClassTypes>  
        <ClassType ID="System.ConfigItem.Projector" Base="System!System.ConfigItem" Hosted="false" Accessibility="Public" Abstract="false">  
          <Property ID="SerialNumber" Type="int" Key="true" />  
          <Property ID="Make" Type="string" />  
          <Property ID="Model" Type="string"  />  
          <Property ID="Location" Type="string" />  
          <Property ID="Condition" Type="enum" EnumType="ProjectorCondition"  />  
        </ClassType>  
      </ClassTypes>  
      <RelationshipTypes>  
      </RelationshipTypes>  
      <EnumerationTypes>  
        <EnumerationValue ID="ProjectorCondition" Accessibility="Public"/>  
        <EnumerationValue ID="ProjectorCondition.Working" Parent="ProjectorCondition" Accessibility="Public"/>  
        <EnumerationValue ID="ProjectorCondition.BeingRepaired" Parent="ProjectorCondition" Accessibility="Public"/>  
        <EnumerationValue ID="ProjectorCondition.New" Parent="ProjectorCondition" Accessibility="Public"/>  
        <EnumerationValue ID="ProjectorCondition.Broken" Parent="ProjectorCondition" Accessibility="Public"/>  
        <EnumerationValue ID="ProjectorViewTasksEnumeration" Accessibility="Public"/>  
      </EnumerationTypes>  
    </EntityTypes>  
  </TypeDefinitions>  
  
```  
  
 The following is a section\-by\-section explanation of what the type definition contains.  
  
 **The ClassTypes Section**  
  
 The **ClassType** element defines the projector class:  
  
 `<ClassType ID="System.ConfigItem.Projector" Base="System!System.ConfigItem" Hosted="false" Accessibility="Public" Abstract="false">`  
  
 The **ID** attribute is the unique identifier of this class. It is set to:  
  
 `ID="System.ConfigItem.Projector"`  
  
 The **Base** attribute is the ID of the class from which this class derives. Because a projector is a kind of configuration item, this is set to:  
  
 `Base="System!System.ConfigItem"`  
  
 The notation of **System\!** indicates that this class, **System.ConfigItem**, is in the management pack that is referenced by the alias **System**.  
  
 The **Hosted** attribute defines whether this class is hosted by another class. In this case, an instance of this class can only exist when a host instance exists that contains it. For this example, projectors are not hosted by anything; therefore, the **Hosted** attribute is set to **false**:  
  
 `Hosted="false"`  
  
 Setting the **Hosted** attribute to **true** indicates that the class is hosted by another class. A hosting relationship must be declared in the **RelationshipTypes** section.  
  
 The **Accessibility** attribute defines whether other classes can derive from this class. In cases where you might want to allow others to create a more specific version of your class, set this attribute to **public**, for example:  
  
 `Accessibility="Public"`  
  
 Setting the **Accessibility** attribute to **Internal** prevents other classes from deriving from this class.  
  
 The **Abstract** attribute defines whether instances of this class can be created, or whether the class should just be used as a parent class to other classes to derive from. In this example, this attribute is set to **false**. Setting this attribute to **true** means that no instances of this class can be created directly and that this class can be used only as a parent class.  
  
 The next section of the class definition contains the class properties. The XML that defines the class properties for this example are defined in the following code example:  
  
```  
  
<Property ID="SerialNumber" Type="int" Key="true" />  
<Property ID="Make" Type="string" />  
<Property ID="Model" Type="string"  />  
<Property ID="Location" Type="string" />  
<Property ID="Condition" Type="enum" EnumType="ProjectorCondition"  />  
  
```  
  
 Each **Property** element has the following attributes:  
  
-   The **ID** attribute, which designates the unique identifier of the property.  
  
-   The **Type** attribute, which indicates the data type of the property.  
  
-   The **Key** attribute. Setting this attribute to **true** indicates that this property is to be used to uniquely identify this class.  
  
 **Creating Enumeration Types**  
  
 Enumerations of the **enum** data type are special data types. Enumerations are used to constrain the data that is allowed for a property to a specific set of values. Enumerations can be hierarchical; one enumeration can be based on another enumeration.  
  
 Enumerations are defined in the **EnumertionTypes** section of a solution pack. An enumeration definition contains the root enumeration, followed by the actual enumeration values.  
  
 Each **EnumerationValue** accepts a few attributes:  
  
 In this example, an enumeration is defined for keeping track of the condition of the projectors. The following defines this enumeration:  
  
-   **ID** is the identifier for the enumeration or enumeration value.  
  
-   **Accessibility** specifies whether this enumerator can contain other enumerators.  
  
-   **ParentName** is an attribute that specifies the **ID** of the parent of the enumerator value.  
  
```  
  
<EnumerationTypes>  
   <EnumerationValue ID="ProjectorCondition" Accessibility="Public"/>  
   <EnumerationValue ID="ProjectorCondition.Working" Parent="ProjectorCondition" Accessibility="Public"/>  
   <EnumerationValue ID="ProjectorCondition.BeingRepaired" Parent="ProjectorCondition" Accessibility="Public"/>  
   <EnumerationValue ID="ProjectorCondition.New" Parent="ProjectorCondition" Accessibility="Public"/>  
   <EnumerationValue ID="ProjectorCondition.Broken" Parent="ProjectorCondition" Accessibility="Public"/>  
   <EnumerationValue ID="ProjectorViewTasksEnumeration" Accessibility="Public"/>  
</EnumerationTypes>  
  
```  
  
## Creating a Form  
 Service Manager forms are based on Windows Presentation Framework \(WPF\) forms. Service Manager extends WPF with simple attributes that are added to the XML definition and allow Service Manager to bind data from the management pack to the form.  
  
 Service Manager forms can be created by using several different tools, including Microsoft Visual Studio or Microsoft Expression Blend. Because the forms are XML\-based, they can also be defined by using any XML editor.  
  
 The following example shows a form definition that was created by using Microsoft Expression Blend. This form contains four controls, three text boxes and one combo box, that are bound to the **Projector** class properties that were defined previously:  
  
```  
  
<UserControl xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:local="clr-namespace:SMFormsDemo" x:Class="SMFormsDemo.TestControl" x:Name="Control" Width="574" Height="390" Opacity="1" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" Background="{DynamicResource {x:Static SystemColors.WindowBrushKey}}">  
   <UserControl.Resources>  
      <ObjectDataProvider ObjectType="{x:Type local:helper}" MethodName="GetStatusValues" x:Key="getStatusValues"/>  
   </UserControl.Resources>  
   <Grid x:Name="LayoutRoot">  
      <Label Margin="70,20,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Serial Number:"/>  
      <TextBox Margin="180,20,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=SerialNumber, Mode=TwoWay}"/>  
      <Label Margin="70,60,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Make:"/>  
      <TextBox Margin="180,60,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Make, Mode=TwoWay}"/>  
      <Label Margin="70,100,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Model:"/>  
      <TextBox Margin="180,100,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Model, Mode=TwoWay}"/>  
      <Label Margin="70,140,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Location:"/>  
      <TextBox Margin="180,140,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Location, Mode=TwoWay}"/>  
      <Label Margin="70,180,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Condition:"/>  
      <ComboBox Margin="180,180,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" ItemsSource="{Binding Source={StaticResource getStatusValues}, Mode=OneWay }" IsSynchronizedWithCurrentItem="True">  
         <ComboBox.SelectedItem>  
            <Binding Path="Condition" Mode="TwoWay" UpdateSourceTrigger="PropertyChanged"/>  
         </ComboBox.SelectedItem>  
         <ComboBox.ItemTemplate>  
            <DataTemplate>  
               <StackPanel>  
                  <TextBlock Text="{Binding Path=DisplayName}"/>  
               </StackPanel>  
            </DataTemplate>  
         </ComboBox.ItemTemplate>  
      </ComboBox>  
   </Grid>  
</UserControl>  
  
```  
  
 To enable binding of controls on the form to class properties that are defined in a management pack, a number of items must be specified.  
  
 **Binding Text Controls**  
  
 To bind text boxes to class properties in a management pack, add a **Binding Path** tag to the text box control's **Text** property, for example:  
  
```  
{Binding Path=SerialNumber, Mode=TwoWay}  
```  
  
 This tag binds the text box control to the **SerialNumber** property of the **Projector** class that was defined in the management pack, and it specifies that this should be a two\-way binding. The value of the property is retrieved from the database and displayed in the text box when the form is loaded, and the property value is stored back to the database if it is changed by the user.  
  
 **Binding Combo Boxes**  
  
 To allow the form to retrieve enumeration data from the underlying management pack and bind it to a control on the form, a helper class must be defined in the **code\-behind** in the form. This helper class should contain a method that returns an enumeration that is defined in the management pack. To return an enumeration use the **GetEnumerations** method of the current management pack. This instance is accessed with the **ConsoleContextHelper** class from the Service Manager software development kit \(SDK\). In the following example, a helper class defines a **GetStatusValues** method that retrieves the values for the **ProjectorCondition** enumeration that was defined in the management pack:  
  
```  
  
public class helper  
{  
   public static ICollection<IDataItem> GetStatusValues()  
   {  
      return ConsoleContextHelper.Instance.GetEnumerations("ProjectorCondition",true);  
   }  
}  
  
```  
  
 To access this method, a few things must be defined in the form definition in the management pack.  
  
 First, a namespace that points to the namespace for the **code behind** for the form is added to the form definition. In this example, the namespace is **SMFormsDemo**:  
  
```  
xmlns:local="clr-namespace:SMFormsDemo"  
```  
  
 Next, an **ObjectDataProvider** must be defined to provide the values for the combo box that displays the projector status. This **ObjectDataProvider** is defined as a resource:  
  
```  
  
<UserControl.Resources>  
   <ObjectDataProvider   
      ObjectType="{x:Type local:helper}"    
      MethodName="GetStatusValues"   
      x:Key="getStatusValues" />  
</UserControl.Resources>  
  
```  
  
 This data provider specifies the object and method name that retrieves the enumeration values from the management pack.  
  
 Finally, to bind the combo box to the enumeration values that are defined in the management pack, an **ItemsSource** attribute is added to the combo box definition. This attribute specifies where to retrieve the enumeration values, for example:  
  
```  
ItemsSource="{Binding Source={StaticResource getStatusValues}, Mode=OneWay }"  
```  
  
 Next, **SelectedItem** and **ItemTemplate** elements are added to the Extensible Application Markup Language \(XAML\) definition of the combo box control. The following example shows the combo box definition with the binding XAML included:  
  
```  
  
<ComboBox Margin="180,180,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" ItemsSource="{Binding Source={StaticResource getStatusValues}, Mode=OneWay }" IsSynchronizedWithCurrentItem="True">  
   <ComboBox.SelectedItem>  
      <Binding Path="Condition" Mode="TwoWay" UpdateSourceTrigger="PropertyChanged"/>  
   </ComboBox.SelectedItem>  
   <ComboBox.ItemTemplate>  
      <DataTemplate>  
         <StackPanel>  
            <TextBlock Text="{Binding Path=DisplayName}"/>  
         </StackPanel>  
      </DataTemplate>  
   </ComboBox.ItemTemplate>  
</ComboBox>  
  
```  
  
## The Category Section  
 The **Category** section of a management pack groups management pack elements together for easier navigation.  
  
 The first two **\<Category\>** elements in the example are used to control the display of the **New** and **Edit** tasks in the **Projectors** view.  
  
```  
<Category ID="ProjectorViewHasTasks.View" Target="AllProjectorsView" Value="ProjectorViewTasksEnumeration" />  
<Category ID="ProjectorViewHasTasks.CreateTask" Target="CreateProjector" Value="ProjectorViewTasksEnumeration" />  
```  
  
 The second two **Category** elements in the example management pack are used to make the projector condition enumeration appear in the **Lists** view in the **Authoring** pane in the Service Manager console. This enables the user to customize the values:  
  
```  
<Category ID="Project.ProjectorConditionEnumVisibleCategory" Target="ProjectorCondition" Value="System!VisibleToUser"/>  
```  
  
 Adding this category in the following example makes the **Edit** task appear in the **Lists** view for the **EnumerationValue** that is pointed at in the **Target** attribute:  
  
```  
<Category ID="Projector.ProjectorConditionCategory" Target="ProjectorCondition" Value="Authoring!Microsoft.EnterpriseManagement.ServiceManager.UI.Authoring.EnumerationViewTasks"/>  
```  
  
## The Presentation Section  
 The **Presentation** section of a management pack declares and defines user\-interface\-related elements. These include forms declarations, categories, and console tasks.  
  
 **The Forms Section**  
  
 The **Forms** section declares forms that are used by your management pack. The following example specifies where to find the form that is defined to display and edit instances of the **Projector** class. This binds the form to the **Projector** class that is defined in the management pack:  
  
```  
  
<Forms>  
   <Form TypeName="SMFormsDemo.TestControl"  
      ID="TestForm"  
      Target="System.ConfigItem.Projector"  
      Assembly="ProjectorFormsAssembly"  
      Accessibility="Public">  
   <Category>Form</Category>  
   </Form>  
</Forms>  
  
```  
  
 The following attributes are used in the preceding example:  
  
-   The **TypeName** attribute contains the namespace and class name of the form.  
  
-   The **ID** attribute contains the unique identifier of this form instance.  
  
-   The **Target** attribute contains the name of the class that this form is bound to.  
  
-   The **Assembly** attribute points to the external resource that contains the form.  
  
-   The **Accessibility** attribute defines whether this form can be customized.  
  
 **Defining a View**  
  
 The **Views** section of a management pack contains definitions of user interface \(UI\) views. These views can be used to filter and display objects in a management pack.  
  
```  
<View Target="System.ConfigItem.Projector"   
Enabled="true"  
TypeID="SMConsole!GridViewType"  
ID="AllProjectorsView"  
Accessibility="Public">  
<Category>NotUsed</Category>  
<Data>  
<Adapters>  
      <Adapter AdapterName="dataportal:EnterpriseManagementObjectAdaptor">  
                <AdapterAssembly>Microsoft.EnterpriseManagement.UI.SdkDataAccess</AdapterAssembly>  
   <AdapterType>  
Microsoft.EnterpriseManagement.UI.SdkDataAccess.DataAdapters.EnterpriseManagementObjectAdapter  
   </AdapterType>  
      </Adapter>  
            <Adapter AdapterName="viewframework://adapters/ListDefault">  
              <AdapterAssembly>Microsoft.EnterpriseManagement.UI.ViewFramework</AdapterAssembly>  
              <AdapterType>Microsoft.EnterpriseManagement.UI.ViewFramework.ListSupportAdapter</AdapterType>  
            </Adapter>  
</Adapters>  
<ItemsSource>  
  <AdvancedListSupportClass DataTypeName="" AdapterName="viewframework://adapters/AdvancedList" FullUpdateAdapter="dataportal:EnterpriseManagementObjectAdapter" FullUpdateFrequency='1' DataSource="mom:ManagementGroup" IsRecurring="true" RecurrenceFrequency="5000"  treaming='true' xmlns="clr-namespace:Microsoft.EnterpriseManagement.UI.ViewFramework;assembly=Microsoft.EnterpriseManagement.UI.ViewFramework" xmlns:av="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:s="clr-namespace:System;assembly=mscorlib" >  
    <AdvancedListSupportClass.Parameters>  
                <QueryParameter Parameter="TargetClass" Value="System.ConfigItem.Projector"/>  
    </AdvancedListSupportClass.Parameters>  
    </AdvancedListSupportClass>  
    </ItemsSource>  
    <Criteria />  
</Data>  
<Presentation>  
<Columns>  
            <mux:ColumnCollection xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:mux="http://schemas.microsoft.com/SystemCenter/Common/UI/Views/GridView" xmlns:s="clr-namespace:System;assembly=mscorlib">  
              <mux:Column Name="SerialNumber" DisplayMemberBinding="{Binding Path=SerialNumber}" Width="100" DisplayName="SerialNumber" Property="SerialNumber" DataType="s:Int32" />  
              <mux:Column Name="Location" DisplayMemberBinding="{Binding Path=Location}" Width="100" DisplayName="Location" Property="Location" DataType="s:String" />  
              <mux:Column Name="Condition" DisplayMemberBinding="{Binding Path=Condition.DisplayName}" Width="100" DisplayName="Condition" Property="Condition.DisplayName" DataType="s:String" />  
              <mux:Column Name="DisplayName" DisplayMemberBinding="{Binding Path=DisplayName}" Width="100" DisplayName="Display Name" Property="DisplayName" DataType="s:String" />  
              <mux:Column Name="OwnerUser" DisplayMemberBinding="{Binding Path=OwnerUser.DisplayName}" Width="100" DisplayName="SupportOwner" Property="OwnerUser.DisplayName" DataType="s:String" />  
            </mux:ColumnCollection>      
</Columns>  
</Presentation>  
</View>  
  
```  
  
 The View Target attribute points to the class that the view will be used to display.  
  
 In the preceding example, the Service Manager Console management pack is referenced. This management pack contains a definition of a view type being used. In this instance, the **SMConsole\!GridViewType** view type is defined.  
  
 The **AdvancedListSupportClass** defines a number of parameters, the most important of which is the **TargetClass** parameter. Set this parameter to the **ID** of the **ClassType** that will appear in this view. To display the columns that are properties of the **ClassType**, use the **Column** element and bind it to the **PropertyID** attribute.  
  
 The **IsRecurring** attribute of the **ListSupportClass** element determines whether the view auto\-refreshes. The **RecurrenceFrequency** attribute defines the refresh interval in milliseconds. In this example, the refresh interval is set to 1 second, but that is not recommended for production installations.  
  
 **Defining Folders**  
  
 Defining a folder determines the location in the navigation tree in which the view is displayed. In this example, a configuration item is defined so that it is only suitable to place the view under the existing folder for configuration items in the **Configuration Items** workspace:  
  
```  
<Folders>  
  <Folder ID="Folder.Projectors" Accessibility="Public" ParentFolder="SMConfig!ServiceManager.Console.ConfigurationManagement.ConfigItem.Root" />  
</Folders>  
<FolderItems>  
   <FolderItem   
      ElementID="AllProjectorsView"   
      Folder="Folder.Projectors" />  
   </FolderItems>  
```  
  
 In the preceding example, the **ElementID** attribute contains a reference to the view that was created. The **Folder** attribute points to a **Folders.Projectors** folder, which in turn has its root as defined in the **Configuration Management** workspace of the Service Manager console. This root folder is defined in the Configuration Management management pack.  
  
 The **ImageReference** element maps the view that was previously created to an icon that is defined in the **Configuration Management** namespace:  
  
```  
<ImageReferences>  
  <ImageReference ElementID="Folder.Projectors" ImageID="SMConfig!ConfigItemImage16x16" />  
  <ImageReference ElementID="AllProjectorsView" ImageID="SMConfig!ConfigItemImage16x16" />  
</ImageReferences>  
```  
  
 **Localization Using the LanguagePacks Section**  
  
 The **LanaguagePacks** section of a management pack defines string resources and mappings for management pack elements.  
  
 In the example, the **EnumerationValueProjectorCondition.Working** must appear as **Working**. To do this, display names for each of the following must be defined:  
  
-   View: All projectors  
  
-   Enumerations: working, broken, in repair, new  
  
```  
  <LanguagePacks>  
    <LanguagePack ID="ENU" IsDefault="true">  
      <DisplayStrings>  
        <DisplayString ElementID="AllProjectorsView">  
          <Name>All Projectors</Name>  
          <Description>This displays all projectors</Description>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.Working">  
          <Name>Working</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.Broken">  
          <Name>Broken</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.BeingRepaired">  
          <Name>In Repair</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.New">  
          <Name>New</Name>  
        </DisplayString>  
      </DisplayStrings>  
    </LanguagePack>  
</LanguagePacks>  
  
```  
  
 You can create additional **LanguagePack** elements, as necessary, for each additional language you require. The correct display string appears to the user based on the user's locale.  
  
 **Resources**  
  
 The **Resources** section of a management pack contains references to binary resources, which are contained in assemblies that are separate from the management pack. In the following example, a resource is defined that points to the assembly that contains the form that is used by the **Projector** class:  
  
```  
<Assembly ID="ProjectorFormsAssembly"    
         Accessibility="Public"   
         QualifiedName="SMFormsDemo, Version=1.0.0.0" FileName="SMFormsDemo.dll" CreationDate="1900-10-12T13:13:13" ModifiedDate="2008-12-12T12:12:12" />  
```  
  
## Class Extensions  
 A class extension is a class that adds properties to an existing class. In most cases, this existing class is in a sealed management pack. In cases where the existing class is not in a sealed management pack, the class extension must be contained in the same management pack as the class that is being extended.  
  
 A class extension inherits the properties of any parent classes, for example:  
  
-   Class A has a property called Property1  
  
-   Class B derives from, or extends, Class A and therefore has a property called Property1. This property is inherited from Class A, the parent, or base class\)  
  
-   The definition of Class B adds a property called Property2.  
  
-   Any class extension that derives from Class B will inherit Property1 and Property2.  
  
 The following example shows a class extension definition:  
  
```  
  
<TypeDefinitions>  
     <EntityTypes>  
       <ClassTypes>  
         <ClassType ID="IncidentManagmentPack.Extension" Accessibility="Public" Base="Incident!System.WorkItem.Incident" Hosted="false" IsExtensionType="true">  
          <Property ID="TimeOnIncident" Type="int" Key="false" />  
        </ClassType>  
      </ClassTypes>  
    </EntityTypes>  
  </TypeDefinitions>  
  
```  
  
 This class extension extends the **System.WorkItem.Incident** class and adds a new property called **TimeOnIncident**.  
  
 The definition for a class extension is similar to that of a class definition. Two attributes of the **ClassType** element are used to define a class definition: the **Base** attribute and the **IsExtensionType** attribute.  
  
 The **Base** attribute specifies the **ID** of the parent class from which the class extension derives. In this instance, the attribute value is set to **Incident\!System.WorkItem.Incident**. This value contains the **Alias** of the full management pack name, which contains the class being extended, an exclamation point, and then the name of the base class. For more information, see the following example.  
  
 The **IsExtensionType** attribute defines whether this class is an extension of the base class. Because **TimeOnIncident** is an extension to the **Incident** class, this property is set to **true**:  
  
```  
IsExtensionType="true"  
```  
  
 The other option is **false**, which indicates that it is not an extension of another class but a new class that inherits from the base. The default value is **false**; therefore, this attribute does not have to be used if the class is not an extension.  
  
 **Full Example**  
  
 The following code example shows the full management pack containing the class extension.  
  
```  
<ManagementPack xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsl="http://www.w3.org/1999/XSL/Transform" ContentReadable="true" SchemaVersion="1.1">  
&nbsp;&nbsp; <Manifest>  
&nbsp;&nbsp;&nbsp;&nbsp; <Identity>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ID>ServiceManager.Extension</ID>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Version>1.0.0.0</Version>  
&nbsp;&nbsp;&nbsp;&nbsp; </Identity>  
&nbsp;&nbsp;&nbsp; <Name>ServiceManagerExtension</Name>  
&nbsp;&nbsp;&nbsp;&nbsp; <References>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Reference Alias="System">  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ID>System.Library</ID>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Version>1.0.2780.0</Version>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </Reference>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Reference Alias="Incident">  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ID>System.WorkItem.Incident.Library</ID>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Version>1.0.2780.0</Version>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </Reference>  
&nbsp;&nbsp;&nbsp; </References>  
&nbsp; </Manifest>  
&nbsp;&nbsp; <TypeDefinitions>  
&nbsp;&nbsp;&nbsp;&nbsp; <EntityTypes>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ClassTypes>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <ClassType ID="IncidentManagmentPack.Extension" Accessibility="Public" Base="Incident!System.WorkItem.Incident" Hosted="false" Extension="true">  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Property ID="TimeOnIncident" Type="int" Key="false" />  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </ClassType>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </ClassTypes>  
&nbsp;&nbsp;&nbsp; </EntityTypes>  
&nbsp; </TypeDefinitions>  
</ManagementPack>  
  
```  
  
## Importing a Management Pack by Using a Windows&nbsp;PowerShell Cmdlet  
 You can use the Windows&nbsp;PowerShell [Import\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225396) cmdlet to import a Service Manager management pack, for example:  
  
```  
Import-SCSMManagementPack MyServiceManager.ManagementPack.xml  
```  
  
 This document does not describe how to import and use management packs in the Service Manager console. For information about using management packs in the Service Manager console, see [Using Management Packs in System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=233228).  
  
## Example: Full Management Pack  
 The following code examples represent the full sample management pack that is used for examples in this topic, in addition to the form definition and the C\# code\-behind for the form.  
  
 **Management Pack**  
  
```  
<ManagementPack ContentReadable="true" SchemaVersion="1.1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
  <Manifest>  
    <Identity>  
      <ID>ServiceManager.Projector</ID>  
      <Version>7.0.3707.0</Version>  
    </Identity>  
    <Name>Projector Library</Name>  
    <References>  
      <Reference Alias="SMConsole">  
        <ID>Microsoft.EnterpriseManagement.ServiceManager.UI.Console</ID>  
        <Version>7.0.3707.0</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
      <Reference Alias="Authoring">  
        <ID>Microsoft.EnterpriseManagement.ServiceManager.UI.Authoring</ID>  
        <Version>7.0.3707.0</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
      <Reference Alias="System">  
        <ID>System.Library</ID>  
        <Version>7.0.3707.0</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
      <Reference Alias="SMConfig">  
        <ID>ServiceManager.ConfigurationManagement.Library</ID>  
        <Version>7.0.3707.0</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
    </References>  
  </Manifest>  
  <TypeDefinitions>  
    <EntityTypes>  
      <ClassTypes>  
        <ClassType ID="System.ConfigItem.Projector" Accessibility="Public" Abstract="false" Base="System!System.ConfigItem" Hosted="false" Singleton="false" Extension="false">  
          <Property ID="SerialNumber" Type="int" Key="true" />  
          <Property ID="Make" Type="string" />  
          <Property ID="Model" Type="string" />  
          <Property ID="Location" Type="string" />  
          <Property ID="Condition" Type="enum" EnumType="ProjectorCondition" />  
        </ClassType>  
      </ClassTypes>  
      <EnumerationTypes>  
        <EnumerationValue ID="ProjectorCondition" Accessibility="Public" />  
        <EnumerationValue ID="ProjectorCondition.Working" Accessibility="Public" Parent="ProjectorCondition" />  
        <EnumerationValue ID="ProjectorCondition.BeingRepaired" Accessibility="Public" Parent="ProjectorCondition" />  
        <EnumerationValue ID="ProjectorCondition.New" Accessibility="Public" Parent="ProjectorCondition" />  
        <EnumerationValue ID="ProjectorCondition.Broken" Accessibility="Public" Parent="ProjectorCondition" />  
        <EnumerationValue ID="ProjectorViewTasksEnumeration" Accessibility="Public" />  
      </EnumerationTypes>  
    </EntityTypes>  
  </TypeDefinitions>  
  <Categories>  
    <Category ID="AllProjectorsView.Category" Target="AllProjectorsView" Value="SMConsole!Microsoft.EnterpriseManagement.ServiceManager.UI.Console.ViewTasks" />  
    <Category ID="ProjectorViewHasTasks.CreateTask" Target="AllProjectorsView" Value="Authoring!Microsoft.EnterpriseManagement.ServiceManager.UI.Authoring.CreateTypeCategory" />  
    <Category ID="Projector.ProjectorConditionCategory" Target="ProjectorCondition" Value="Authoring!Microsoft.EnterpriseManagement.ServiceManager.UI.Authoring.EnumerationViewTasks" />  
    <Category ID="Project.ProjectorConditionEnumVisibleCategory" Target="ProjectorCondition" Value="System!VisibleToUser" />  
  </Categories>  
  <Presentation>  
    <Forms>  
      <Form ID="TestForm" Accessibility="Public" Target="System.ConfigItem.Projector" Assembly="ProjectorFormsAssembly" TypeName="New_CI_lab.TestControl">  
        <Category>Form</Category>  
      </Form>  
    </Forms>  
    <Views>  
      <View ID="AllProjectorsView" Accessibility="Public" Enabled="true" Target="System.ConfigItem.Projector" TypeID="SMConsole!GridViewType" Visible="true">  
    <Category>NotUsed</Category>  
    <Data>  
    <Adapters>  
    <Adapter AdapterName="dataportal:EnterpriseManagementObjectAdapter">  
    <AdapterAssembly>Microsoft.EnterpriseManagement.UI.SdkDataAccess</AdapterAssembly>  
    <AdapterType>Microsoft.EnterpriseManagement.UI.SdkDataAccess.DataAdapters.EnterpriseManagementObjectAdapter</AdapterType>  
    </Adapter>  
    <Adapter AdapterName="viewframework://adapters/AdvancedList">  
    <AdapterAssembly>Microsoft.EnterpriseManagement.UI.ViewFramework</AdapterAssembly>  
    <AdapterType>Microsoft.EnterpriseManagement.UI.ViewFramework.AdvancedListSupportAdapter</AdapterType>  
    </Adapter>  
    <Adapter AdapterName="omsdk://Adapters/Criteria">  
    <AdapterAssembly>Microsoft.EnterpriseManagement.UI.SdkDataAccess</AdapterAssembly>  
    <AdapterType>Microsoft.EnterpriseManagement.UI.SdkDataAccess.DataAdapters.SdkCriteriaAdapter</AdapterType>  
    </Adapter>  
    </Adapters>  
    <ItemsSource>  
    <AdvancedListSupportClass DataTypeName="" AdapterName="viewframework://adapters/AdvancedList" FullUpdateAdapter="dataportal:EnterpriseManagementObjectAdapter" FullUpdateFrequency='1' DataSource="mom:ManagementGroup"   
  IsRecurring="true" RecurrenceFrequency="5000"  Streaming='true' xmlns="clr-namespace:Microsoft.EnterpriseManagement.UI.ViewFramework;assembly=Microsoft.EnterpriseManagement.UI.ViewFramework" xmlns:av="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:s="clr-namespace:System;assembly=mscorlib" >  
    <AdvancedListSupportClass.Parameters>  
                <QueryParameter Parameter="TargetClass" Value="System.ConfigItem.Projector"/>  
    </AdvancedListSupportClass.Parameters>  
    </AdvancedListSupportClass>  
    </ItemsSource>  
    <Criteria />  
    </Data>  
    <Presentation>  
    <Columns>  
<mux:ColumnCollection xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:mux="http://schemas.microsoft.com/SystemCenter/Common/UI/Views/GridView" xmlns:s="clr-namespace:System;assembly=mscorlib">  
              <mux:Column Name="SerialNumber" DisplayMemberBinding="{Binding Path=SerialNumber}" Width="100" DisplayName="SerialNumber" Property="SerialNumber" DataType="s:Int32" />  
              <mux:Column Name="Location" DisplayMemberBinding="{Binding Path=Location}" Width="100" DisplayName="Location" Property="Location" DataType="s:String" />  
              <mux:Column Name="Condition" DisplayMemberBinding="{Binding Path=Condition.DisplayName}" Width="100" DisplayName="Condition" Property="Condition.DisplayName" DataType="s:String" />  
              <mux:Column Name="DisplayName" DisplayMemberBinding="{Binding Path=DisplayName}" Width="100" DisplayName="Display Name" Property="DisplayName" DataType="s:String" />  
              <mux:Column Name="OwnerUser" DisplayMemberBinding="{Binding Path=OwnerUser.DisplayName}" Width="100" DisplayName="SupportOwner" Property="OwnerUser.DisplayName" DataType="s:String" />  
            </mux:ColumnCollection>      
    </Columns>  
    </Presentation>  
    </View>  
    </Views>  
    <Folders>  
      <Folder ID="Folder.Projectors" Accessibility="Public" ParentFolder="SMConfig!ServiceManager.Console.ConfigurationManagement.ConfigItem.Root" />  
    </Folders>  
    <FolderItems>  
      <FolderItem ElementID="AllProjectorsView" ID="FolderItem.AllProjectors" Folder="Folder.Projectors" />  
    </FolderItems>  
    <ImageReferences>  
      <ImageReference ElementID="Folder.Projectors" ImageID="SMConfig!ConfigItemImage16x16" />  
      <ImageReference ElementID="AllProjectorsView" ImageID="SMConfig!ConfigItemImage16x16" />  
    </ImageReferences>  
  </Presentation>  
  <LanguagePacks>  
    <LanguagePack ID="ENU" IsDefault="true">  
      <DisplayStrings>  
    <DisplayString ElementID="System.ConfigItem.Projector">  
    <Name>Projector</Name>  
    </DisplayString>  
        <DisplayString ElementID="Folder.Projectors">  
          <Name>Projectors</Name>  
          <Description>This is the Projector Folder</Description>  
        </DisplayString>  
        <DisplayString ElementID="AllProjectorsView">  
          <Name>All Projectors</Name>  
          <Description>This displays all projectors</Description>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.Working">  
          <Name>Working</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.Broken">  
          <Name>Broken</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.BeingRepaired">  
          <Name>In Repair</Name>  
        </DisplayString>  
        <DisplayString ElementID="ProjectorCondition.New">  
          <Name>New</Name>  
        </DisplayString>  
      </DisplayStrings>  
    </LanguagePack>  
  </LanguagePacks>  
  <Resources>  
    <Assembly ID="ProjectorFormsAssembly" Accessibility="Public" FileName="New_CI_lab.dll" QualifiedName="New_CI_lab, Version=0.0.0.0" />  
  </Resources>  
</ManagementPack>  
```  
  
 **Form Definition**  
  
```  
  
<UserControl  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:local="clr-namespace:SMFormsDemo"  
    x:Class="SMFormsDemo.TestControl"  
    x:Name="Control"  
    Width="574" Height="390" Opacity="1" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" Background="{DynamicResource {x:Static SystemColors.WindowBrushKey}}">  
  <UserControl.Resources>  
    <ObjectDataProvider ObjectType="{x:Type local:helper}"  MethodName="GetStatusValues" x:Key="getStatusValues" />  
  </UserControl.Resources>  
  <Grid x:Name="LayoutRoot">  
    <Label Margin="70,20,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Serial Number:"/>  
    <TextBox Margin="180,20,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=SerialNumber, Mode=TwoWay}"/>  
    <Label Margin="70,60,0,0" HorizontalAlignment="Left"  VerticalAlignment="Top" Width="160" Height="25" Content="Make:"/>  
    <TextBox Margin="180,60,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Make, Mode=TwoWay}" />  
    <Label Margin="70,100,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Model:"/>  
    <TextBox Margin="180,100,0,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Model, Mode=TwoWay}"/>  
    <Label Margin="70,140,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Location:"/>  
    <TextBox Margin="180,140,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" d:IsStaticText="True" Text="{Binding Path=Location, Mode=TwoWay}" />  
    <Label Margin="70,180,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" Content="Condition:"/>  
    <ComboBox Margin="180,180,80,0" HorizontalAlignment="Left" VerticalAlignment="Top" Width="160" Height="25" ItemsSource="{Binding Source={StaticResource getStatusValues}, Mode=OneWay }" IsSynchronizedWithCurrentItem="True">  
      <ComboBox.SelectedItem>  
        <Binding Path="Condition" Mode="TwoWay" UpdateSourceTrigger="PropertyChanged"/>  
      </ComboBox.SelectedItem>  
      <ComboBox.ItemTemplate>  
        <DataTemplate>  
          <StackPanel>  
            <TextBlock Text="{Binding Path=DisplayName}"/>  
          </StackPanel>  
        </DataTemplate>  
      </ComboBox.ItemTemplate>  
    </ComboBox>  
  </Grid>  
</UserControl>  
  
```  
  
 **Form Code\-Behind**  
  
```  
  
using System;  
using System.Collections.Generic;  
using System.Collections.ObjectModel;  
using System.Threading;  
using System.Windows.Controls;  
using Microsoft.EnterpriseManagement.ServiceManager.Application.Common;  
using Microsoft.EnterpriseManagement.UI.DataModel;  
namespace SMFormsDemo  
{  
   /// <summary>  
   /// Interaction logic for ProjectorForm.xaml  
   /// </summary>  
   public partial class TestControl : UserControl  
   {  
        public TestControl()  
      {  
         InitializeComponent();  
      }        
   }  
   public class helper  
   {  
  
      public static ICollection<IDataItem> GetStatusValues()  
      {  
            return ConsoleContextHelper.Instance.GetEnumerations("ProjectorCondition",true);  
      }  
   }  
}  
  
```  
  
## See Also  
 [Changes to the System Center Common Schema](../../../sm/manage/author/Changes-to-the-System-Center-Common-Schema.md)   
 [Forms: General Guidelines and Best Practices](../Topic/Forms:%20General%20Guidelines%20and%20Best%20Practices.md)
