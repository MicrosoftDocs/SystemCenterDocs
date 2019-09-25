---
ms.assetid: 5d49e7f3-0e22-4ab4-90c4-ef1c67a28aae
title: Using Exception Handlers to Define Critical Exceptions
description: This article provides an overview of using exception handlers to define critical exceptions
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 07/29/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Using Exception Handlers to Define Critical Exceptions

Exception handlers are application functions that "catch" exceptions that the applications throw to report errors and perform some error handling. By default, .NET Application Performance Monitoring defines critical exceptions as exceptions handled by specific exception handlers provided by the .NET framework. These handlers catch top-level ASP.NET exceptions, and web service exceptions that the monitored application failed to catch and handle internally. By adding exception handlers, you are adding to what application monitoring's definition of what a critical exception is. In effect, any exceptions handled by these functions will be considered critical exceptions. The advantage to doing this is that you maintain the benefit of streamlined reporting of critical exceptions only, but you have the additional benefit of reporting functions that are of interest to you. It is common to add any customer error handlers defined for web applications to the list of critical exception handlers so that you can be alerted when a user is sent to your error handler page in the web application.

> [!Warning]
> Exception handlers are set on the process level. If you enable an exception handler for an application that is running in the process and then disable it for a different application running in that process, there will be a configuration conflict and application monitoring will be disabled. To resolve this, you must make the exception handling the same for all applications in the same process.

## Default Exception Handlers

The default list of exception handlers includes:

- Web.HttpApplication.RecordError
- Web.UI.Page.HandleError
- Web.Services.Protocols.WebServiceHandler.WriteException
- AppDomain.OnUnhandledExceptionEvent
- Windows.Forms.Application.ThreadContext.OnThreadException
- AppDomain.OnUnhandledExceptionEvent
- Runtime.Remoting.Messaging.ReturnMessage..ctor
- Windows.Forms.DataGridView.OnDataError

For System Center 2012 SP1 these resources are included:

- Office.Server.Data.SqlSession.LogException
- Office.Excel.Server.CalculationServer.Proxy.ExcelServerProxy.ProcessSoapException
- Office.Excel.Server.CalculationServer.Proxy.ExcelServerProxy.ProcessWebException
- SharePoint.Portal.WebControls.BusinessDataWebPart.ConstructErrorMessage
- SharePoint.Diagnostics.ULS.SendEventTag
- SharePoint.ApplicationRuntime.SPRequestModule.IsWebPartOnExceptionStack
- SharePoint.Utilities.SqlSession.LogException
- Office.Web.Environment.Sharepoint.Diagnostics.ULS.SendExceptionTag
- SharePoint.Diagnostics.ULS.SendExceptionTag
- Office.Server.Diagnostics.ULS.SendExceptionTag
- Workflow.Runtime.WorkflowExecutor.IsIrrecoverableException
- ServiceModel.DiagnosticUtility.IsFatal
- Web.Mvc.ControllerActionInvoker.InvokeExceptionFilters

## Add an Exception Handler

### To add an exception handler

1. To open the .NET Application Performance Monitoring template, in the Operations Manager console, in the navigation pane, click the  **Authoring**  button, click  **Management Pack Templates** , and then click  **.NET Application Performance Monitoring**.
2. Right click the application group you want to modify, and then select  **Properties**.
3. On the  **Server-Side Defaults**  tab, click  **Advanced Settings**.
4. On the  **Advanced settings**  page, click  **Critical Exceptions**  to open the  **Exception handlers list**  page. This is where you can add exception handlers.
5. To add an exception handler, click  **Add**  and type the method you want to add to the exception handlers list. If you want this exception handler to affect monitoring, make sure the  **Enable monitoring**  checkbox is selected. Click  **OK**.

    > [!Important]
    > Adding handlers that are defined in the .NET Framework as part of mscorlib as Critical Exceptions will not produce any effect.

    > [!NOTE]
    > The method name is case sensitive and should be specified in the following format: Namespace.ClassName.MethodName

## Edit an Exception Handler

### To edit an exception handler

1. Open the .NET Application Performance Monitoring template. In the Operations Manager console, in the navigation pane, click the  **Authoring**  button, click  **Management Pack Templates** , and then click  **.NET Application Performance Monitoring**.
2. Right click the application group you want to modify and select  **Properties**.
3. On the Server-Side Defaults tab, click  **Advanced Settings**.
4. On the  **Advanced settings**  page, click  **Critical Exceptions**. This opens the  **Exception handlers list**  page where you can edit exception handlers.
5. To edit an exception handler, click  **Edit** , select the exception handler you want to change, and then modify it. Click  **OK**.

   > [!NOTE]
   > The method name is case sensitive. Additionally, the method name should be specified in the following format: Namespace.ClassName.MethodName

## Remove an Exception Handler

### To remove an exception handler

1. Open the .NET Application Performance Monitoring template. In the Operations Manager console, in the navigation pane, click the  **Authoring**  button, click  **Management Pack Templates** , and then click  **.NET Application Performance Monitoring**.
2. Right click the application group you want to modify and select  **Properties**.
3. On the Server-Side Defaults tab, click  **Advanced Settings**.
4. On the  **Advanced settings**  page, click  **Critical Exceptions**. This opens the  **Exception handlers list**  page where you can remove exception handlers.
5. To remove an exception handler, select the exception handler you want to remove, click  **Remove** , and then click  **OK**.
