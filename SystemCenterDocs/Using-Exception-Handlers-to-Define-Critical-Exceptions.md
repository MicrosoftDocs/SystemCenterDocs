---
title: Using Exception Handlers to Define Critical Exceptions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67a9a184-f90c-4745-a3ec-a66c9d006c58
---
# Using Exception Handlers to Define Critical Exceptions
Exception handlers are application functions that “catch” exceptions that the applications throw to report errors and perform some error handling. By default, .NET Application Performance Monitoring defines critical exceptions as exceptions handled by specific exception handlers provided by the .NET framework. These handlers catch top\-level ASP.NET exceptions, and web service exceptions that the monitored application failed to catch and handle internally. By adding exception handlers, you are adding to what application monitoring’s definition of what a critical exception is. In effect, any exceptions handled by these functions will be considered critical exceptions. The advantage to doing this is that you maintain the benefit of streamlined reporting of critical exceptions only, but you have the additional benefit of reporting functions that are of interest to you. It is common to add any customer error handlers defined for web applications to the list of critical exception handlers so that you can be alerted when a user is sent to your error handler page in the web application.

> [!WARNING]
> Exception handlers are set on the process level. If you enable an exception handler for an application that is running in the process and then disable it for a different application running in that process, there will be a configuration conflict and application monitoring will be disabled. To resolve this, you must make the exception handling the same for all applications in the same process.

## Default Exception Handlers
The default list of exception handlers includes:

-   System.Web.HttpApplication.RecordError

-   System.Web.UI.Page.HandleError

-   System.Web.Services.Protocols.WebServiceHandler.WriteException

-   System.AppDomain.OnUnhandledExceptionEvent

-   System.Windows.Forms.Application.ThreadContext.OnThreadException

-   System.AppDomain.OnUnhandledExceptionEvent

-   System.Runtime.Remoting.Messaging.ReturnMessage..ctor

-   System.Windows.Forms.DataGridView.OnDataError

For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.Office.Server.Data.SqlSession.LogException

-   Microsoft.Office.Excel.Server.CalculationServer.Proxy.ExcelServerProxy.ProcessSoapException

-   Microsoft.Office.Excel.Server.CalculationServer.Proxy.ExcelServerProxy.ProcessWebException

-   Microsoft.SharePoint.Portal.WebControls.BusinessDataWebPart.ConstructErrorMessage

-   Microsoft.SharePoint.Diagnostics.ULS.SendEventTag

-   Microsoft.SharePoint.ApplicationRuntime.SPRequestModule.IsWebPartOnExceptionStack

-   Microsoft.SharePoint.Utilities.SqlSession.LogException

-   Microsoft.Office.Web.Environment.Sharepoint.Diagnostics.ULS.SendExceptionTag

-   Microsoft.SharePoint.Diagnostics.ULS.SendExceptionTag

-   Microsoft.Office.Server.Diagnostics.ULS.SendExceptionTag

-   System.Workflow.Runtime.WorkflowExecutor.IsIrrecoverableException

-   System.ServiceModel.DiagnosticUtility.IsFatal

-   System.Web.Mvc.ControllerActionInvoker.InvokeExceptionFilters

## Add an Exception Handler

#### To add an exception handler

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group you want to modify, and then select **Properties**.

3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Critical Exceptions** to open the **Exception handlers list** page. This is where you can add exception handlers.

5.  To add an exception handler, click **Add** and type the method you want to add to the exception handlers list. If you want this exception handler to affect monitoring, make sure the **Enable monitoring** checkbox is selected. Click **OK**.

    > [!IMPORTANT]
    > Adding handlers that are defined in the .NET Framework as part of mscorlib as Critical Exceptions will not produce any effect.

    > [!NOTE]
    > The method name is case sensitive and should be specified in the following format: Namespace.ClassName.MethodName

## Edit an Exception Handler

#### To edit an exception handler

1.  Open the .NET Application Performance Monitoring template. In the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group you want to modify and select **Properties**.

3.  On the Server\-Side Defaults tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Critical Exceptions**. This opens the **Exception handlers list** page where you can edit exception handlers.

5.  To edit an exception handler, click **Edit**, select the exception handler you want to change, and then modify it. Click **OK**.

    > [!NOTE]
    > The method name is case sensitive. Additionally, the method name should be specified in the following format: Namespace.ClassName.MethodName

## Remove an Exception Handler

#### To remove an exception handler

1.  Open the .NET Application Performance Monitoring template. In the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group you want to modify and select **Properties**.

3.  On the Server\-Side Defaults tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Critical Exceptions**. This opens the **Exception handlers list** page where you can remove exception handlers.

5.  To remove an exception handler, select the exception handler you want to remove, click **Remove**, and then click **OK**.

