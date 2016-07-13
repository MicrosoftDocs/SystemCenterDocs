---
title: Guidelines for Creating Custom Activities
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50891279-b22e-4d84-baf7-1488f6e9585b
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
# Guidelines for Creating Custom Activities
[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] automates a variety of information technology \(IT\) processes. For the Incident Management process, for example, [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] includes various automated steps, such as automated notifications to users when incidents are created or resolved and automatic routing of incidents to various queues, based on categorization. This automation is implemented by using workflows that are defined for the various solutions, and it uses Windows Workflow Foundation \(WF\) capabilities to describe, execute, and track the automated operations.  
  
 Customers and partners can extend the included automation by defining new workflows and adding them into a process. Workflows can be set to occur on a fixed schedule or on a specified condition occurring in the database, for example, when an incident is created or when it changes to a specified state, such as **Active** or **Resolved**.  
  
 The [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] provides an easy\-to\-use method of creating new workflows. It provides a library of different workflow activities, such as creating an incident or updating an incident, and a drag\-and\-drop graphical designer that you can use to arrange these workflow activities into a workflow sequence. The [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] then compiles the new workflow into a set of definitions, code, and management pack content. When this information is imported into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], it integrates the new workflow into the specified solution.  
  
 Understanding what is going on behind the scenes of the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] can benefit more advanced users. First, customers and partners can use this information to extend the workflow activity library in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] with workflow activities that apply to their specific processes. Secondly, developers can use this information to build custom or advanced workflows that are compatible with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] by using their development tool of choice, such as the Microsoft Visual Studio development system.  
  
## Workflow Activities and the WorkflowActivityBase Class  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] workflows use WF activities. To work smoothly with the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], these activities derive from the base class **WorkflowActivityBase**, which belongs to the **Microsoft.EnterpriseManagement.Workflow.Common** namespace. The **WorkflowActivityBase** base class introduces properties and methods that are not available in the generic **Activity** base class for WF activities. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] how to define WF activities by using the generic **Activity** base class, see [Activity Class](http://go.microsoft.com/fwlink/p/?LinkID=193539).  
  
### Benefits of Using the WorkflowActivityBase Class  
 Users can import WF activities from the Visual Studio activity library, and they can work with those activities in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)]**Authoring** pane. However, those activities behave in the same way as they do in the Visual Studio Design environment. They do not have the customizations that are built into the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity library.  
  
> [!NOTE]  
>  Not all Visual Studio WF activities have been tested for compatibility with the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], and some Visual Studio WF activities might not run correctly in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
 The following table lists the differences in behavior between WF activities that are based on the **WorkflowActivityBase** base class and WF activities that are based on the generic **Activity** base class.  
  
|Scenario|[!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] WF activity \(**WorkflowActivityBase** base class\)|Visual Studio WF activity \(**Activity** base class\)|  
|--------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------|  
|User binds activity properties \(to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] object properties or to properties from other activities\).|Calls the **Bind property to** dialog box that is customized for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] users.|Calls the **Bind property to** dialog box that is intended for developers.|  
|User adds the activity to a **For\-Each Loop** activity.|Adds the properties **Propertytobind** \(the loop index\) and **CurrentItem**, which are required to take part in loop\-specific operations \(**CurrentItem** is an internal property\).|Behaves in the same way for each iteration of the loop, and does not interact with the property that indexes the loop.|  
  
> [!IMPORTANT]  
>  Because of the customizations that are required for the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] workflow designer, activities that are based on the **WorkFlowActivityBase** class do not function as expected in the Visual Studio workflow design environment.  
  
 Users can build custom WF activities in Visual Studio for use in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)]. However, to take advantage of the custom design\-time behavior of the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], custom activities must be based on the **WorkflowActivityBase** class instead of the **Activity** class.  
  
## Workflow Activities and Service Manager Automated Activities  
 WF activities can interact with a different type of activity, the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activities that are used by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] work items. *Work items* are one of the main types of objects that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] uses. Work items track units of work, such as **Incidents**, **Service Requests**, **Change Requests**, and other units of work. Most work items comprise one or more [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activities. For example, a **Change Request** typically includes at least two activities: a **Review** activity and a **Change Execution** activity. The work item typically executes these activities in order.  
  
 When a work item is created, the first [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity becomes active and remains active while [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] \(or the user\) carries out whatever work the activity represents. When that work finishes, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] marks the first activity as **Completed** and activates the next activity in the sequence. When the final activity in the sequence is marked as **Completed**, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] marks the entire work item as **Completed**.  
  
 Some [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activities can be executed manually, such as the **Review** activity of a **Change Request**. Other [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activities can be automated, such as an activity that sends an email to a user. The **Change Execution** activity of a **Change Request** can be automated. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] uses WF workflows to automate [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activities.  
  
## Example: The Set Activity Status to Completed Activity  
 This example of a WF workflow activity in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] uses the **Set Activity Status to Completed** WF activity. This WF activity typically represents the last step in a workflow that implements an automated [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity, and it sets the status of that activity to **Completed**. Setting this status triggers the system to move to the next activity in the work item, and this process repeats until the last activity in the work item is completed.  
  
 The **Set Activity Status to Completed** activity takes one input, **Activity ID**, which identifies the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity on which to act. The WF activity then connects to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, retrieves the specified [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity from the database, sets its status to **Completed**, and then saves it back to the database. Most of the code samples that are included in this example come from the SetActivityStatusToCompleted.cs file, an underlying file that describes the **Set Activity Status to Completed** activity.  
  
### Initializing the Example WF Activity  
 The first section of the SetActivityStatusToCompleted.cs file contains the declaration and initialization statements. This activity is based on the **WorkflowActivityBase** class, and it uses the validator class **SetActivityStatusToCompletedValidator** and the designer class **WorkflowActivityBaseDesigner**.  
  
 The **WorkflowActivityBaseDesigner** class contains the customizations that are described in the previous section, "Benefits of Using the WorkflowActivityBase Class." You can further extend and customize this class.  
  
 The first section of the activity definition for this example activity includes the following code:  
  
```  
namespace Microsoft.ServiceManager.WorkflowAuthoring.ActivityLibrary  
{  
    // ---------------------------------------------------------------------  
    /// <summary>  
    /// Activity to set an activity's status to complete  
    /// </summary>  
    // ---------------------------------------------------------------------  
    [ToolboxItem(typeof(ActivityToolboxItem))]  
    [ActivityValidator(typeof(Validators.SetActivityStatusToCompletedValidator))]  
    [Designer(typeof(WorkflowActivityBaseDesigner))]  
    public sealed partial class SetActivityStatusToCompleted : WorkflowActivityBase  
    {  
  
```  
  
### Input Properties for the Example WF Activity  
 The code declares one property, **ActivityId**, as a dependency property. This means that this property can be bound to parameters that are defined at the workflow level. In this case, the ID of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity is passed in to the workflow as a workflow parameter, and it flows into this activity as an input.  
  
```  
  // --------------------------------------------------------------------------------  
  /// <summary>  
  /// Dependency Property for ActivityId property  
  /// </summary>  
  // --------------------------------------------------------------------------------  
  public static DependencyProperty ActivityIdProperty =   
      DependencyProperty.Register("ActivityId", typeof(String), typeof(SetActivityStatusToCompleted));  
  
  // --------------------------------------------------------------------------------  
  /// <summary>  
  /// Activity ID  
  /// </summary>  
  // --------------------------------------------------------------------------------  
  [Browsable(true)]  
  [DesignerSerializationVisibility(DesignerSerializationVisibility.Visible)]  
  public string ActivityId  
  {  
      get  
      {  
          return (string)this.GetValue(ActivityIdProperty);  
      }  
      set  
      {  
          this.SetValue(ActivityIdProperty, value);  
      }  
}  
  
```  
  
### Execution Behavior in the Example WF Activity  
 The **Execute** method does the actual work of this WF activity. Within the scope of the **Execute** method, the WF activity does the following:  
  
-   Detects whether it is operating within a **For\-Each Loop** activity, and, if so, sets the appropriate WF activity properties.  
  
-   Connects to the specified [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and creates an **EnterpriseManagementGroup** object.  
  
-   Uses the **ActivityId** property to get the identified [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity from the database.  
  
-   Finds the class definition of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity, gets the **Status** property of the retrieved [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity, and sets the property to the **Completed** enumeration list value.  
  
-   Commits the changes to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity.  
  
-   Uses the **TrackData** method \(part of the WF infrastructure\) to log tracking information about the execution and status of the WF activity.  
  
```  
        // --------------------------------------------------------------------------------  
        /// <summary>  
        /// The execute method will have the implementation to set the activity status to complete.  
        /// </summary>  
        // --------------------------------------------------------------------------------  
        protected override ActivityExecutionStatus Execute(ActivityExecutionContext executionContext)  
        {  
            try  
            {  
                // Initialize the current item if the activity contained within the For-Each loop  
                base.Execute(executionContext);  
  
                // Validate Parameters  
                if (String.IsNullOrEmpty(ActivityId))  
                {  
                    throw new ArgumentNullException("ActivityId");  
                }  
  
                string SMServer = "localhost";                  
  
                Guid TaskGuid = new Guid(ActivityId);  
                EnterpriseManagementGroup _mg = new EnterpriseManagementGroup(SMServer);  
  
                EnterpriseManagementObject Activity = _mg.EntityObjects.GetObject  
                    <EnterpriseManagementObject>(TaskGuid, ObjectQueryOptions.Default);  
  
                ManagementPack SystemMP = _mg.ManagementPacks.GetManagementPack(  
                    SystemManagementPack.System);  
                ManagementPack ActivityMP = _mg.ManagementPacks.GetManagementPack(  
                    Resources.ActivityManagementMP, SystemMP.KeyToken, SystemMP.Version);  
  
                ManagementPackClass activityClass = _mg.EntityTypes.GetClass(  
                    Resources.WorkItemActivityClass, ActivityMP);  
  
                ManagementPackProperty status = activityClass.PropertyCollection["Status"];  
                ManagementPackEnumeration Completed =   
                    _mg.EntityTypes.GetEnumeration("ActivityStatusEnum.Completed", ActivityMP);  
  
                Activity[status].Value = Completed;  
                Activity.Commit();  
            }  
            catch (ArgumentNullException argNullException)  
            {  
                // Log to Tracking Service  
                TrackData(argNullException.ToString());  
  
                throw;  
            }  
            catch (EnterpriseManagementException mgmtException)  
            {  
                TrackData(mgmtException.ToString());  
                throw;  
            }  
  
            return ActivityExecutionStatus.Closed;  
        }  
    }  
}  
  
```  
  
### Validation Behavior in the Example WF Activity  
 The SetActivityStatusToCompletedValidator.cs file defines the validation behavior of the WF activity. This behavior defines how the designer indicates whether this WF activity is fully defined or if it still requires one or more inputs to be defined. The [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] indicates a validation error similarly to Visual Studio by using a red exclamation point \(**\!**\) icon on the workflow activity in the **Authoring** pane.  
  
```  
namespace Microsoft.ServiceManager.WorkflowAuthoring.ActivityLibrary.Validators  
{  
    // --------------------------------------------------------------------------------              
    /// <summary>  
    /// Validator for the SetActivityStatusToCompleted activity  
    /// </summary>  
    // --------------------------------------------------------------------------------              
    internal class SetActivityStatusToCompletedValidator : ActivityValidator  
    {  
        // --------------------------------------------------------------------------------          
        /// <summary>  
        /// Validator for the SetActivityStatusToCompleted activity  
        /// </summary>  
        // --------------------------------------------------------------------------------      
        public override ValidationErrorCollection Validate(ValidationManager manager, object obj)  
        {  
            // Performing default validation              
            ValidationErrorCollection errorColl = base.Validate(manager, obj);  
  
            SetActivityStatusToCompleted setActivityStatusToCompletedObj =   
                (SetActivityStatusToCompleted)obj;  
  
            // Check if validation is happening during compilation of activity and  
            // not during the hosting of an activity                  
            if (setActivityStatusToCompletedObj.Parent == null)  
            {  
                return errorColl;  
            }  
  
            string propertyName = Common.GetPropertyName(setActivityStatusToCompletedObj);  
  
            // Add validation error if ActivityId is null or empty                  
            if (setActivityStatusToCompletedObj.ActivityId == null   
                &&  
                setActivityStatusToCompletedObj.GetBinding(SetActivityStatusToCompleted.ActivityIdProperty) == null   
                &&  
                String.Compare(propertyName, "ActivityId", false, CultureInfo.InvariantCulture) != 0)  
            {  
                errorColl.Add(new ValidationError(  
                    Resources.SetActivityStatusToCompleted_ActivityId_DesignTimeValidation, 10, false));  
            }  
  
            return errorColl;  
        }  
    }  
}  
  
```  
  
### Using the Example WF Activity in a Workflow  
 The **Set Activity Status to Completed** activity is included in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] default **Activities Toolbox** pane. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] adding custom activities to the **Activities Toolbox** pane, see [How to Install a Custom Activity Assembly](../../../sm/manage/author/How-to-Install-a-Custom-Activity-Assembly.md) in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] online Help.  
  
 You can use the authoring pane of the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to author workflows in a manner that is similar to using the Visual Studio workflow design interface. However, the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] offers the following benefits:  
  
-   Users without development skills can build workflows; they do not have to work with code directly.  
  
-   When a user saves a workflow in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], the tool generates the corresponding Visual C\# and XOML code and compiles it into a .dll file. The tool also integrates the workflow with a management pack that can interact directly with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Visual C\# Code for the Workflow  
 The following sample shows the Visual C\# code that the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] generates for an example workflow that uses the **Set Activity Status to Completed** activity. This code declares a simple sequential workflow, **SetActivityStatusToCompleteWF**, that has one workflow parameter, the dependency property **ActivityId**. The value of **ActivityID** is determined by the management pack definitions that are shown later in this example. When the workflow runs, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] identifies the value and passes it into the workflow.  
  
```  
namespace WorkflowAuthoring  
{  
    using System;  
    using System.ComponentModel;  
    using System.ComponentModel.Design;  
    using System.Workflow.ComponentModel.Design;  
    using System.Workflow.ComponentModel;  
    using System.Workflow.ComponentModel.Serialization;  
    using System.Workflow.ComponentModel.Compiler;  
    using System.Drawing;  
    using System.Collections;  
    using System.Workflow.Activities;  
    using System.Workflow.Runtime;  
  
    public partial class SetActivityStatusToCompleteWF : System.Workflow.Activities.SequentialWorkflowActivity  
    {  
  
        public static DependencyProperty ActivityIdProperty = DependencyProperty.Register("ActivityId", typeof(string), typeof(SetActivityStatusToCompleteWF));  
  
        [System.ComponentModel.DesignerSerializationVisibilityAttribute(DesignerSerializationVisibility.Visible)]  
        [System.ComponentModel.BrowsableAttribute(true)]  
        [System.ComponentModel.CategoryAttribute("Misc")]  
        public string ActivityId  
        {  
            get  
            {  
                return ((string)(this.GetValue(ActivityIdProperty)));  
            }  
            set  
            {  
                this.SetValue(ActivityIdProperty, value);  
            }  
        }  
    }  
}  
  
```  
  
## XOML Code for the Workflow  
 WF uses the XOML format for some of the workflow definitions. In the case of the example workflow, the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] creates the file SetActivityStatusToCompleteWF.xoml with the following content:  
  
```  
<SequentialWorkflowActivity x:Class="WorkflowAuthoring.SetActivityStatusToCompleteWF" x:Name="SetActivityStatusToCompleteWF" xmlns:ns0="clr-namespace:Microsoft.ServiceManager.WorkflowAuthoring.ActivityLibrary;Assembly=Microsoft.ServiceManager.WorkflowAuthoring.ActivityLibrary, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/workflow">  
<ns0:SetActivityStatusToCompleted ActivityId="{ActivityBind SetActivityStatusToCompleteWF,Path=ActivityId}" x:Name="setActivityStatusToCompleted1" PropertyToBind="{x:Null}" />  
</SequentialWorkflowActivity>  
```  
  
 SetActivityStatusToCompleteWF.xoml declares that the workflow**,  SetActivityStatusToCompleteWF**, runs one workflow activity, **Set Activity Status To Completed**. That activity has one input parameter, *ActivityId*, which gets its value from the **ActivityId** property of the workflow.  
  
## Declaring the Workflow and Its Trigger Condition in a Management Pack  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] cannot use an isolated workflow .dll file; the workflow must be integrated with a management pack. The management pack defines when the workflow should run and what input values to use. At the same time that it generates the workflow code and compiles the workflow .dll file, the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] adds the workflow\-related information to a management pack.  
  
 The example workflow, **SetActivityStatusToCompleteWF**, is associated with an example management pack, named Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml. This management pack extends the **Change Management** process with a new automated [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity. When the new activity becomes active during a change management operation, it triggers the **SetActivityStatusToCompleteWF** workflow.  
  
 The management pack defines the trigger of the workflow \(when the new [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity changes state\), and it defines the value to use for the **ActivityId** property \(the unique identifier of the new [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity\). When the workflow runs, it changes the status of the new [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity to **Completed**. Note that in a normal workflow, this would be the last step following some other task that is performed by other WF activities in the workflow.  
  
 The **Monitoring** section of the management pack contains the **Rule** definition for the workflow. In turn, the **Rule** definition has two parts, the **DataSource** element and the **WriteAction** element.  
  
 In the case of the example workflow, the **DataSource** element contains a **Subscription** element, which specifies that the workflow should run when an instance of the **AddComputerToGroup** class \(a custom [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] class\) changes state to **Active**.  
  
```  
<Monitoring>  
    <Rules>  
      <Rule ID="SetActivityToCompleteRule" Enabled="true"   
     Target="SystemCenterLibrary!Microsoft.SystemCenter.SubscriptionWorkflowTarget"   
     ConfirmDelivery="false" Remotable="true" Priority="Normal" DiscardLevel="100">  
        <Category>Notification</Category>  
        <DataSources>  
          <DataSource ID="DS"   
TypeID="Subscriptions!Microsoft.SystemCenter.CmdbInstanceSubscription.DataSourceModule">  
    <Subscription>  
<InstanceSubscription Type="$MPElement[Name='AddComputerToGroup']$">  
    <UpdateInstance>  
<Criteria>  
   <Expression>  
       <SimpleExpression>  
           <ValueExpression>  
   <Property State="Post">  
$Context/Property[Type='Activity!System.WorkItem.Activity']/Status$  
</Property>  
   </ValueExpression>  
   <Operator>Equal</Operator>  
   <ValueExpression>  
       <Value>  
$MPElement[Name='Activity!ActivityStatusEnum.Active']$  
       </Value>  
   </ValueExpression>  
</SimpleExpression>  
    </Expression>  
</Criteria>  
    </UpdateInstance>  
</InstanceSubscription>  
<StartWatermark>1</StartWatermark>  
<PollingIntervalInSeconds>60</PollingIntervalInSeconds>  
<BatchSize>100</BatchSize>  
   </Subscription>  
</DataSource>  
     </DataSources>  
```  
  
 The **WriteAction** element \(specifically, **Microsoft.EnterpriseManagement.SystemCenter.Subscription.WindowsWorkflowTaskWriteAction**\) defines what to do when the trigger condition is met. Within this element, a **Subscription** element identifies the workflow assembly file to run \(SetActivityStatusToCompleteWF.dll\) and the class in the assembly that represents the workflow, **WorkflowTypeName**.  
  
 The **Subscription** element also includes a **WorkflowParameter** element, which defines the **ActivityId** property and, using the syntax **$Data\/BaseManagedEntityId$**, binds it to the unique identifier of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] activity that is recorded in the **DataSource** element.  
  
 The **WriteAction** element also stores optional configuration details for the workflow, such as how many retries to perform if the workflow fails, how frequently to retry, and the maximum time in seconds that a workflow should run before it is shut off.  
  
```  
    <WriteActions>  
    <WriteAction ID="WA"   
TypeID="Subscriptions!Microsoft.EnterpriseManagement.SystemCenter.Subscription.WindowsWorkflowTaskWriteAction">  
    <Subscription>  
        <WindowsWorkflowConfiguration>  
     <AssemblyName>SetActivityStatusToCompleteWF</AssemblyName>  
     <WorkflowTypeName>  
WorkflowAuthoring.SetActivityStatusToCompleteWF  
     </WorkflowTypeName>  
     <WorkflowParameters>  
 <WorkflowParameter Name="ActivityId"   
      Type="string">$Data/BaseManagedEntityId$  
 </WorkflowParameter>  
     </WorkflowParameters>  
     <RetryExceptions></RetryExceptions>  
     <RetryDelaySeconds>60</RetryDelaySeconds>  
     <MaximumRunningTimeSeconds>300</MaximumRunningTimeSeconds>  
</WindowsWorkflowConfiguration>  
    </Subscription>  
</WriteAction>  
     </WriteActions>  
   </Rule>  
 </Rules>  
</Monitoring>  
```  
  
### Importing the Management Pack  
 For the workflow to run on a particular [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, all of the files that are related to the workflow must reside on that server. These files include the following:  
  
-   The WF activity assembly files. If you are using only the [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] WF activities, by default, the appropriate files are installed. If you are using custom activities, see [How to Install a Custom Activity Assembly](../../../sm/manage/author/How-to-Install-a-Custom-Activity-Assembly.md) in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] online Help.  
  
-   The workflow assembly file, in this case, SetActivityStatusToCompleteWF.dll. You must manually copy this file to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
-   The management pack file, in this case, Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml. You must manually copy this file to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
 When all of the files are in place, import the management pack into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. You can do this by using the mpimport.exe command\-line tool or the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] console. After you have imported the management pack, the workflow is ready to run whenever the condition that is defined as its trigger is met.  
  
## See Also  
 [Workflow Activity Reference](../../../sm/manage/author/Workflow-Activity-Reference.md)