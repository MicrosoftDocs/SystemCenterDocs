---
title: Forms: General Guidelines and Best Practices
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85107d34-7b5f-4775-9730-b947cd2438f8
 

















---
# Forms: General Guidelines and Best Practices
You can extend features of System Center 2012 - Service Manager by adding or modifying forms. This topic describes some best practice recommendations for creating and using Service Manager forms, using various tools and scripting form definitions directly.  
  
 This topic is primarily targeted at partners and customers who are experienced in building their own custom forms by using Windows Presentation Foundation \(WPF\) and Microsoft Visual Studio Team System or Microsoft Expression Blend.  
  
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
  
### Use Standard Controls  
 Controls that are used on a form can be:  
  
-   **Standard controls**. This includes .NET library controls, such as combo box and list box.  
  
-   **Custom controls**. This includes additional controls that are created by the form author or by a third party.  
  
> [!TIP]  
>  When you use standard controls wherever possible and avoid creating custom controls, you promote consistency with regard to the user experience of forms. If you must create a custom control, separate the visual appearance and behavior and the logical behavior by using control templates to define the appearance of the control. Preferably, there should be a separate control template for each Windows Theme.  
  
### Follow General Form Design Guidelines  
 When you design a form, use public design guidelines to ensure that the form is user friendly and that it adheres to common user\-interaction paradigms.  
  
 For more information about general Windows design, see [Windows User Experience Interaction Guidelines](http://go.microsoft.com/fwlink/p/?LinkID=134101).  
  
 In addition:  
  
-   Divide information across multiple tabs to make the form simpler and easier to read. Include the most commonly used information on the first tab and information of lesser importance on subsequent tabs.  
  
-   Use layout panels to lay out controls on the form. This ensures that the form behaves correctly when it is resized and localized.  
  
-   Avoid setting individual control visual properties, and use styles instead. This makes it possible for you to change the appearance of all controls across a series of forms by modifying the style, and it promotes a consistent appearance across related forms.  
  
### Avoid Code\-Behind  
 *Code\-behind* is a term that describes the code that is joined with markup\-defined objects when an XAML page is markup compiled. Limit the use of code\-behind in a form as much as possible. It is preferable that you embed the code for a form in the control itself, because later it is easier to change that code. Instead, use the declarative capabilities that are supported by the Service Manager forms infrastructure to define value conversions and validation rules in the form.  
  
 As a general guideline, you should limit the use of code\-behind to situations in which it is not possible to provide the required functionality by using the declarative capabilities of XAML, with classes defined in the WPF and the forms infrastructure library. Even then, consider moving the functionality that is implemented in code\-behind into a helper library, and then reference it from the XAML.  
  
### Include Exception Handling  
 Ensure that the code in the form contains exception handling so that the form can be loaded both during the design phase in the Authoring Tool and in the Service Manager console at run time.  
  
### Consider Forms Customization and Upgrades  
 When you are designing a new form, you should consider future customizations and upgrades to that form. To ensure that it is possible to customize and to upgrade a form while preserving customizations, follow the guidelines and tips that are provided previously in this section, along with the following guidelines:  
  
-   Consider future customizations and upgrades early while you are designing the form. Forms are likely to evolve in future versions, and it is important to consider how users will be able to upgrade to new versions of your form while preserving their customizations to the original form. For example, you might provide an updated form after users have already invested heavily in customizing your original form. Users expect their customizations to survive the version upgrade.  
  
-   Provide a unique name for each control on the form to make it possible for customizations to be applied to controls. Form customizations are stored as a set of actions that are targeted at a specific control or a set of controls. The target control is referenced by name, which is why it is important to preserve control names across versions of the form. If a control does not have a name, the Form Customization Editor generates a name, but the generated name is not preserved across different versions of the form.  
  
-   Ensure that control names remain immutable across different versions of the form. This ensures that customizations for a given control in a previous version can be applied to the same control in a new version of the form.  
  
-   If possible, avoid moving controls to a different location on the same tab when you upgrade a form. A common user customization is moving controls on the form to a different location. If you change the location of a control in a new version of the form, there is a risk that the new control location could overlap with a control that the user has relocated.  
  
-   If possible, avoid moving controls between tabs when you are designing an update to an existing form. Controls are identified both by name and by the tab on which they are located. Moving a control from one tab to another in a new version of the form can break customizations that the user makes to that control, because the customizations will fail to identify the target control.  
  
-   When the update to a form includes new controls, consider adding the new controls to a new tab. That is the safest way to avoid interfering with any user customizations to the existing tabs and controls.  
  
-   Be aware of how controls are bound. Read\-only controls should use only one\-way bindings.  
  
### Name all Customizable Controls  
 Ensure that the control names describe what data the control is bound to, or describe what the control does.  
  
### Bind the Form to Data Sources  
 The main purpose of a form is to visualize a single object from the Service Manager database. This object is called a **target instance**, which is always specified by the **DataContext** property of a form \(which is inherited from the **FrameworkElement** class\).  
  
> [!IMPORTANT]  
>  Do not modify the form’s **DataContext** property. The forms hosting environment uses this property to identify the form target instance.  
  
 In the Service Manager data model, a target instance is represented as a **BindableDataItem** object. This class aggregates the underlying software development kit \(SDK\) object, and it exposes its properties through an indexer, which takes a property name as a parameter.  
  
 The **BindableDataItem** class also implements **ICustomTypeDescriptor**, which makes it possible to use the **BindableDataItem** class as a data source for WPF binding. The following is an example of binding a target instance property to the **Text** property of a **TextBox** control:  
  
```  
  
<TextBox Name="textBoxDescription" Text="{Binding Path=Summary}"/>  
  
```  
  
 It is not necessary to specify the **Source** of the binding because the target instances are set as the **DataContext** of the form, which serves as the default **Source** for all controls on the form.  
  
 Controls on the form can be bound to data sources other than the target instance, and the forms infrastructure library contains a number of controls that perform the binding implicitly. For example, the instance picker control is bound to the data source, which provides the collection of instances to choose. It is also possible to define additional data sources declaratively using the **ObjectDataProvider** and **XmlDataProvider** classes.  
  
 The forms infrastructure considers the target instance as the only read\/write data source on the form. Therefore, the implementation of the **Submit** command will only store the changes that are made to the target instance. Other data sources for the form are treated as read only.  
  
### Use Service Manager Forms Infrastructure Validation Rules, Value Convertors, and Error Templates  
 We recommend that you use forms infrastructure validation rules in forms to designate data input that is not valid. The WPF binding infrastructure supports validation for control properties that are bound to a data source with either one\-way or two\-way bindings. The binding object has a **ValidationRules** collection that can contain any number of **ValidationRule** objects. Whenever data is pushed from the control to the data source, the **ValidationRule** objects are called to validate the value.  
  
 The forms infrastructure library contains a number of validation rules that handle the most common cases. The forms infrastructure takes advantage of the validation rules to determine whether the form contents can be submitted for storing. For example, a form’s **Submit** button can be disabled if there is a control that has a validation error on the form.  
  
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
  
### Use Form Infrastructure Commands and Events  
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
  
## See Also  
 [Windows Presentation Foundation \(WPF\) Web Site \(WindowsClient.NET\)](http://go.microsoft.com/fwlink/p/?LinkID=134100)   
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)
