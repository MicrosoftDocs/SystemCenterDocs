---
title: Default Entry Points for .NET Application Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2186d3b4-528b-485c-abec-8ee4e9dfb8c6
---
# Default Entry Points for .NET Application Monitoring
Application Performance Monitoring in [!INCLUDE[om12short](Token/om12short_md.md)] is preconfigured with many well\-known entry points \(see below\), but also lets you extend the default list by defining your own entry points. In addition to adding functions as entry points, you may also define entire Namespaces to act as entry points, so that the system begins timing execution the first time that it encounters the namespace during execution. Additionally, the application monitoring agent collects the values of variables for each entry point at the time the event occurs.

## Entry points Monitored by Default

### For ASP.NET pages

-   System.Web.UI.Page.ProcessRequest

-   \(System.Web.IHttpHandler\).ProcessRequest

### For ASP.NET 2.0 asynchronous pages

-   [!INCLUDE[sc2012sp1note](Token/sc2012sp1note_md.md)] System.Web.UI.Page.AsyncPageBeginProcessRequest

-   System.Web.Services.Protocols.LogicalMethodInfo.Invoke

-

### For COM\+ server\-side

-   System.EnterpriseServices.ServicedComponent.RemoteDispatchHelper

### For .NET Remoting server\-side

-   System.Runtime.Remoting.Messaging.ServerObjectTerminatorSink.AsyncProcessMessage

-   System.Runtime.Remoting.Messaging.ServerObjectTerminatorSink.SyncProcessMessage

### For WCF Server Side

-   System.ServiceModel.Dispatcher.SyncMethodInvoker.Invoke

### For WWF

-   System.Workflow.Runtime.WorkflowExecutor.RunScheduler

### For AJAX.NET

-   System.Web.Script.Services.RestHandler.ExecuteWebServiceCall

### For Windows Services
For [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)] these entry points are included:

-   System.ServiceProcess.ServiceBase.ServiceCommandCallback

-   System.ServiceProcess.ServiceBase.ServiceQueuedMainCallback

-   System.ServiceProcess.ServiceBase.Stop

-   System.ServiceProcess.ServiceBase.DeferredPowerEvent

-   System.ServiceProcess.ServiceBase.DeferredSessionChange

### For MVC
For [!INCLUDE[sc2012sp1_short](Token/sc2012sp1_short_md.md)] these entry points are included:

-   System.Web.Mvc.ControllerBase.Execute

-   \(System.Web.Mvc.IController\).Execute

-   System.Web.Mvc.AsyncController.BeginExecute

-   \(System.Web.Mvc.IAsyncController\).BeginExecute

-   System.Web.Mvc.ViewResultBase.ExecuteResult


