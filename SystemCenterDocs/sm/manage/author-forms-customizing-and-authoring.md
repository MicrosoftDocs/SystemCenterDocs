---
title: Overview of customizing and authoring forms
description: Learn about how you can customize and author forms with the Service Manager Authoring Tool.
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
ms.assetid: dd99e994-e34d-469e-aea0-5c3547eeab66
---

# Overview of customizing and authoring forms with the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

A form is a window that makes it possible for users to interact with objects from the database. Users can use a form to view and edit the properties of objects. Each form is tied to a specific class, and it displays information only for instances of the targeted class. A form contains fields. Typically, each field is bound to a specific property of the form's targeted class. The incident form, for example, is tied to the incident object. Therefore, the incident form displays information about incident objects in the database.  

 A Service Manager form consists of the Windows Presentation Foundation \(WPF\) form implementation in a Microsoft .NET&nbsp;Framework assembly and a form definition in a Service Manager management pack. The form definition specifies the class that the form represents, along with the other properties of the form.  

## Key concepts about forms

Before customizing forms, you should be familiar with the following form concepts.  

### How forms are used  
 When the management pack that contains the form definitions is imported into Service Manager, the form definitions are stored in the database. Later, when the user initiates a Service Manager console task that requires the display of an object, Service Manager must find a form to display the requested object. Service Manager accesses the database and searches for a form that has been defined for that object. If no form is defined for the object, Service Manager searches for a form that is defined for the object's parent object. Service Manager continues to search the entire object's inheritance hierarchy until it finds a defined form.  

### Generic forms  
 If Service Manager cannot find any form for the object or for any of its parent objects, Service Manager dynamically builds a default *generic form* for that object. The generic form is a system\-generated form that is sufficient for simple form use. The generic form represents a quick and easy way to create a form for objects without any form definitions.  

 By default, the generic form displays all the properties of the form in a simple layout that you cannot change. The generic form displays the properties of all the parent objects in the inheritance hierarchy of the form, and you cannot change that behavior. Customizations to the generic form are limited. For example, you can specify the properties that you want the generic form to display; however, the generic form cannot be used as a basis for customization. If you later define a custom form for that object, your custom form overwrites the object's generic form.  

 For information about hiding properties in a generic form and other ways that you can customize a generic form, see the blog post [Overview of the Forms Infrastructure and the Generic Form](http://go.microsoft.com/fwlink/p/?LinkID=208536).  

### Combination classes in forms  
 Sometimes, you need a form to display information that is derived from more than one class. To do this, you create a *combination class* and then bind a field on the form to the combination class. For more information about combination classes, see [Changes to the System Center Common Schema](author-working-with-management-pack-xml-files.md).  

### Functional aspects of a form  
 A form has the following functional aspects:  

1.  Initialization  

2.  Size and location  

3.  Refresh  

4.  Submit changes  

 These aspects are described in the following sections.  

#### Initialization  
 During initialization, a form's Extensible Application Markup Language \(XAML\) is parsed and all controls on the form are instantiated and loaded. The form's **Loaded** event indicates when the form and all contained elements have been loaded. Data\-loading operations are asynchronous. Therefore, the target instance may not be available when the **Loaded** event is raised. Instead, the **DataContextChanged** event must be used for notification when the target instance is set for the form. The **PropertyChanged** event for the **DataContext** property can be used in place of the **DataContextChanged** event.  

 We recommend that you use the **Loaded** event for control\-related custom initialization and then use the **DataContextChanged** or **PropertyChanged** events on the **DataContext** property for target instance\-related custom initialization.  

#### Size and location  
 When a form is displayed in a pop\-up window, its initial size is determined based on the form's **Width**, **Height**, **MinWidth**, and **MinHeight** properties. If these properties are not set for the form, the form's initial size is calculated based on its content.  

 We recommend that you set these properties as follows:  

-   Set the **Width** and **Height** properties of the form to explicitly specify the ideal size. Consider setting these properties to the **Auto** value. This sets the width and height of the form based on the size of the content.  

-   Set the **MinWidth** and **MinHeight** properties of the form to specify the smallest window acceptable for the form. If a user resizes the window to a smaller size than specified, scrollbars appear for scrolling to the hidden form content.  

 When the form is hosted inside the Service Manager forms host, the last\-used size and location is preserved for subsequent display of that form by the same user within the same run session.  

#### Refresh  
 The target instance of a form can change as a result of executing a **Refresh** command on the form. The handler for this command fetches new data from the database. When the data arrives, the form's **DataContext** property value is set to the new target instance and the **DataContextChanged** event is raised.  

 To differentiate between the **DataContextChanged** event that was raised when the form was first loaded and the event that was raised to handle a **Refresh** command, check the **OldValue** property of the event arguments that are passed in with the event. This property is null if the form has just been initialized.  

#### Submit changes  
 The form host pop\-up window in Service Manager provides buttons for submitting changes that are made in the form and for closing the pop\-up window.  

 When a user clicks the **Apply** button for a form, the form's target instance is submitted for storage. This operation is synchronous; therefore, the user cannot edit the form until the submission operation is complete. If failure occurs during the form submission, an error message appears. The form remains open for further changes. We recommend that users apply their changes frequently to avoid collisions if another instance of the form is being edited at the same time.  

 If the user clicks the **OK** button, the behavior is similar to **Apply**, except that, if the form submission operation is successful, the form and its host window are closed.  

 If the user clicks the **Cancel** button, a dialog box appears that asks the user to confirm the operation. The user can click **Yes** and lose changes, or click **No** and return to the form.   

## General guidelines and best practices for forms

You can extend features of Service Manager by adding or modifying forms. This topic describes some best practice recommendations for creating and using Service Manager forms, using various tools and scripting form definitions directly.  

 This topic is primarily targeted at partners and customers who are experienced in building their own custom forms by using Windows Presentation Foundation \(WPF\) and Microsoft Visual&nbsp;Studio Team System or Microsoft Expression Blend.  

 The general guidelines for authoring a new form are as follows.  

-   Use standard controls.  

-   Follow general form design guidelines.  

-   Avoid code\-behind.  

-   Include exception handling.  

-   Consider forms customization and upgrades.  

-   Name all customizable controls.  

-   Bind the form to data sources.  

-   Use Service Manager forms infrastructure validation rules, value convertors, and error templates.  

-   Use forms infrastructure commands and events.  

 For information about these guidelines, see the following sections.  

### Use standard controls  
 Controls that are used on a form can be:  

-   **Standard controls**. This includes .NET library controls, such as combo box and list box.  

-   **Custom controls**. This includes additional controls that are created by the form author or by a third party.  

> [!TIP]  
>  When you use standard controls wherever possible and avoid creating custom controls, you promote consistency with regard to the user experience of forms. If you must create a custom control, separate the visual appearance and behavior and the logical behavior by using control templates to define the appearance of the control. Preferably, there should be a separate control template for each Windows Theme.  

### Follow general form design guidelines  
 When you design a form, use public design guidelines to ensure that the form is user friendly and that it adheres to common user\-interaction paradigms.  

 For more information about general Windows design, see [Windows User Experience Interaction Guidelines](http://go.microsoft.com/fwlink/p/?LinkID=134101).  

 In addition:  

-   Divide information across multiple tabs to make the form simpler and easier to read. Include the most commonly used information on the first tab and information of lesser importance on subsequent tabs.  

-   Use layout panels to lay out controls on the form. This ensures that the form behaves correctly when it is resized and localized.  

-   Avoid setting individual control visual properties, and use styles instead. This makes it possible for you to change the appearance of all controls across a series of forms by modifying the style, and it promotes a consistent appearance across related forms.  

### Avoid code-behind  
 *Code\-behind* is a term that describes the code that is joined with markup\-defined objects when an XAML page is markup compiled. Limit the use of code\-behind in a form as much as possible. It is preferable that you embed the code for a form in the control itself, because later it is easier to change that code. Instead, use the declarative capabilities that are supported by the Service Manager forms infrastructure to define value conversions and validation rules in the form.  

 As a general guideline, you should limit the use of code\-behind to situations in which it is not possible to provide the required functionality by using the declarative capabilities of XAML, with classes defined in the WPF and the forms infrastructure library. Even then, consider moving the functionality that is implemented in code\-behind into a helper library, and then reference it from the XAML.  

### Include exception handling  
 Ensure that the code in the form contains exception handling so that the form can be loaded both during the design phase in the Authoring Tool and in the Service Manager console at run time.  

### Consider forms customization and upgrades  
 When you are designing a new form, you should consider future customizations and upgrades to that form. To ensure that it is possible to customize and to upgrade a form while preserving customizations, follow the guidelines and tips that are provided previously in this section, along with the following guidelines:  

-   Consider future customizations and upgrades early while you are designing the form. Forms are likely to evolve in future versions, and it is important to consider how users will be able to upgrade to new versions of your form while preserving their customizations to the original form. For example, you might provide an updated form after users have already invested heavily in customizing your original form. Users expect their customizations to survive the version upgrade.  

-   Provide a unique name for each control on the form to make it possible for customizations to be applied to controls. Form customizations are stored as a set of actions that are targeted at a specific control or a set of controls. The target control is referenced by name, which is why it is important to preserve control names across versions of the form. If a control does not have a name, the Form Customization Editor generates a name, but the generated name is not preserved across different versions of the form.  

-   Ensure that control names remain immutable across different versions of the form. This ensures that customizations for a given control in a previous version can be applied to the same control in a new version of the form.  

-   If possible, avoid moving controls to a different location on the same tab when you upgrade a form. A common user customization is moving controls on the form to a different location. If you change the location of a control in a new version of the form, there is a risk that the new control location could overlap with a control that the user has relocated.  

-   If possible, avoid moving controls between tabs when you are designing an update to an existing form. Controls are identified both by name and by the tab on which they are located. Moving a control from one tab to another in a new version of the form can break customizations that the user makes to that control, because the customizations will fail to identify the target control.  

-   When the update to a form includes new controls, consider adding the new controls to a new tab. That is the safest way to avoid interfering with any user customizations to the existing tabs and controls.  

-   Be aware of how controls are bound. Read\-only controls should use only one\-way bindings.  

### Name all customizable controls  
 Ensure that the control names describe what data the control is bound to, or describe what the control does.  

### Bind the form to data sources  
 The main purpose of a form is to visualize a single object from the Service Manager database. This object is called a **target instance**, which is always specified by the **DataContext** property of a form \(which is inherited from the **FrameworkElement** class\).  

> [!IMPORTANT]  
>  Do not modify the form's **DataContext** property. The forms hosting environment uses this property to identify the form target instance.  

 In the Service Manager data model, a target instance is represented as a **BindableDataItem** object. This class aggregates the underlying software development kit \(SDK\) object, and it exposes its properties through an indexer, which takes a property name as a parameter.  

 The **BindableDataItem** class also implements **ICustomTypeDescriptor**, which makes it possible to use the **BindableDataItem** class as a data source for WPF binding. The following is an example of binding a target instance property to the **Text** property of a **TextBox** control:  

```  

<TextBox Name="textBoxDescription" Text="{Binding Path=Summary}"/>  

```  

 It is not necessary to specify the **Source** of the binding because the target instances are set as the **DataContext** of the form, which serves as the default **Source** for all controls on the form.  

 Controls on the form can be bound to data sources other than the target instance, and the forms infrastructure library contains a number of controls that perform the binding implicitly. For example, the instance picker control is bound to the data source, which provides the collection of instances to choose. It is also possible to define additional data sources declaratively using the **ObjectDataProvider** and **XmlDataProvider** classes.  

 The forms infrastructure considers the target instance as the only read\/write data source on the form. Therefore, the implementation of the **Submit** command will only store the changes that are made to the target instance. Other data sources for the form are treated as read only.  

### Use Service Manager forms infrastructure validation Rules, value convertors, and error templates  
 We recommend that you use forms infrastructure validation rules in forms to designate data input that is not valid. The WPF binding infrastructure supports validation for control properties that are bound to a data source with either one\-way or two\-way bindings. The binding object has a **ValidationRules** collection that can contain any number of **ValidationRule** objects. Whenever data is pushed from the control to the data source, the **ValidationRule** objects are called to validate the value.  

 The forms infrastructure library contains a number of validation rules that handle the most common cases. The forms infrastructure takes advantage of the validation rules to determine whether the form contents can be submitted for storing. For example, a form's **Submit** button can be disabled if there is a control that has a validation error on the form.  

 We recommend that you use the custom error template that is provided with the forms infrastructure library. If a control has a validation error, it appears by default with a red border around it. The WPF makes it possible to define a custom error indicator through the **Validation.ErrorTemplate** property, which can be set on any control. The Service Manager forms infrastructure library contains a custom error template, which displays an error icon instead of the WPF red border. In addition, when a mouse points to the error icon, a tooltip pops up with an error message. The error message should indicate the reason why the data in the control failed validation.  

 The following example shows how to reference the error template in XAML:  

```  

<TextBox Text="{Binding SomeProperty}"  
         scwpf:Validation.ValueRequired="True"   
         Validation.ErrorTemplate="{DynamicResource {ComponentResourceKey {x:Type scwpf:Validation}, InvalidDataErrorTemplate}}"/>  

```  

 If built\-in validation rules do not provide the required validation logic, we recommend that you build custom validation rules to represent that logic. This will make it possible for standard and custom validation logic to coexist within the common validation handling mechanism.  

 If the validation rules mechanism is not adequate for a particular scenario, you should instead handle **FormEvents.PreviewSubmitEvent** and run the validation from there.  

 The following code example provides an example of the pattern that you can use to run custom validation:  

```  

void MyForm_Loaded(object sender, RoutedEventArgs e)  
{  
    // hook to handle form events  
    this.AddHandler(  
        FormEvents.PreviewSubmitEvent,  
        new EventHandler<PreviewFormCommandEventArgs>(this.OnPreviewSubmit));  
}  
private void OnPreviewSubmit(object sender, PreviewFormCommandEventArgs e)  
{  
    string errorMessage;  
    bool result = this.DoVerify(out errorMessage);  
    if (!result)  
    {  
        // cancel Submit operation  
        e.Cancel = true;  
        // display error message  
        MessageBox.Show(errorMessage);  
    }  
}  
internal bool DoVerify(out string errorMessage)  
{  
    // Do custom verification and return true to indicate that  
    // validation check has passed; otherwise return false and  
    // populate errorMessage argument  
}  

```  

### Use form infrastructure commands and events  
 The form infrastructure exposes a number of commands that can be run on a form. These commands include:  

-   **FormsCommand.Submit**, which saves the target instance of the form.  

-   **FormsCommand.SubmitAndClose**, which saves the target instance of the form and closes the form.  

-   **FormsCommand.Refresh**, which repeats the query for the target instance of the form.  

-   **FormCommands.Cancel**, which discards all changes and closes the form.  

 Each of these commands is bracketed by events, which are raised before and after the command runs.  

 Before the command, the following events are raised:  

-   The **FormEvents.PreviewSubmit** event is raised before the **FormCommand.Submit** command, and the **FormEvents.Submitted** event is raised after the **FormCommand.Submit** command.  

-   The **FormEvents.PreviewRefresh** event is raised before the **FormCommands.Refresh** command, and the **FormCommand.Refreshed** command is raised after the **FormCommand.Submit** command.  

-   The **FormEvents.PreviewCancel** event is raised before the **FormCommands.Cancel** command, and the **FormCommand.Canceled** event is raised after the **FormCommand.Cancel** command.  

 The preview events pass along a **PreviewFormCommandEventArgs** object. This object contains a mutable **Cancel** property that will prevent the corresponding command from running when the property is set to **true**.  

 The post\-command events pass a **FormCommandExecutedEventArgs** object. This object contains a **Result** property that indicates whether the running of the command succeeded, was canceled, or caused an error. In case of an error, the **Error** property of the **FormCommandExecutedEventArgs** object references the exception that provides information about the error.  

 It is possible to enable, disable, and run form commands both programmatically and declaratively.  

 To enable form commands programmatically, establish a **CommandBinding** between the form and the related command.  

 In the following example, a command binding is established between the form and a **Refresh** command, and two handlers are defined for this command. The first handler returns whether or not the **Refresh** command can run, and the second handler actually contains the implementation of the **Refresh** command:  

```  

    public class MyForm : UserControl  
    {  
        public MyForm()  
        {  
            // do standard initialization  
            // establish CommandBinding for Refresh command  
            this.CommandBindings.Add(  
                new CommandBinding(FormCommands.Refresh, this.ExecuteRefresh, this.CanExecuteRefresh));  
        }  
        private void CanExecuteRefresh(  
              object sender,  
              CanExecuteRoutedEventArgs e)  
        {  
            // put your logic that determines whether Refresh   
// can be executed here  
            bool canExecute = true;  
            BindableDataItem dataItem = this.DataContext as BindableDataItem;  
            if (dataItem)  
            {  
                canExecute = dataItem["Status"] != "New";  
            }  
            e.CanExecute = canExecute;  
        }  
        private void ExecuteRefresh(  
            object sender,  
            ExecutedRoutedEventArgs e)  
        {  
            // here is placeholder for the code that has do be   
// executed upon running Refresh command  
        }  
    }  

```  

 You can also define handlers for form commands declaratively. You can do this by employing a **Rule** object that uses a **RoutedCommandTrigger**. The following code example shows how to define handlers declaratively:  

```  

    <scwpf:BusinessLogic.Rules>  
        <scwpf:RuleCollection>  
            <scwpf:Rule>  
                <scwpf:Rule.Triggers>  
                    <scwpf:RoutedCommandTrigger   
RoutedCommand="{x:Static scwpf:FormCommands.Refresh}"/>  
                </scwpf:Rule.Triggers>  
                <scwpf:Rule.Conditions>  
                    <scwpf:PropertyMatchCondition   
                        Binding="{Binding Status}"   
                        Value="New"   
                        Operation="NotEquals" />  
                </scwpf:Rule.Conditions>  
                <!-- Use RuleAction objects to define the logic that executed   
                upon running Refresh command; this can be left empty -->  
            </scwpf:Rule>  
        </scwpf:RuleCollection>  
    </scwpf:BusinessLogic.Rules>  

```  
