---
title: Sample Activity - Setting an Activity's Status to Completed
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e31bc91-020f-47e7-bd2b-d40ddc2fb7ca
---

# Sample Activity - Setting an Activity's Status to Completed

>Applies To: System Center 2016 - Service Manager

The following is a sample activity in Service Manager that sets an activity's status to complete.  

```  
using System;  
using System.Linq;  
using System.Drawing;  
using System.Collections;  
using System.ComponentModel;  
using System.Workflow.Runtime;  
using System.Collections.Generic;  
using System.Workflow.Activities;  
using System.ComponentModel.Design;  
using Microsoft.EnterpriseManagement;  
using System.Workflow.ComponentModel;  
using System.Workflow.Activities.Rules;  
using System.Workflow.ComponentModel.Design;  
using Microsoft.EnterpriseManagement.Common;  
using System.Workflow.ComponentModel.Compiler;  
using System.Workflow.ComponentModel.Serialization;  
using Microsoft.EnterpriseManagement.Configuration;  
using Microsoft.EnterpriseManagement.Configuration.IO;  
using Microsoft.EnterpriseManagement.Workflow.Common;  

namespace Microsoft.ServiceManager.WorkflowAuthoring.ActivityLibrary  
{  
    // --------------------------------------------------------------------------------  
    /// <summary>  
    /// Activity to set an activity's status to complete  
    /// </summary>  
    // --------------------------------------------------------------------------------  
    [ToolboxItem(typeof(ActivityToolboxItem))]  
    [ActivityValidator(typeof(Validators.SetActivityStatusToCompletedValidator))]  
    [Designer(typeof(WorkflowActivityBaseDesigner))]  
    public sealed partial class SetActivityStatusToCompleted : WorkflowActivityBase  
    {  
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
