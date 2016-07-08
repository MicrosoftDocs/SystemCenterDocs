---
title: How to Add, Edit, and Remove Exception Tracking
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5cc4e36-2259-4f5d-a5de-f96cf20545f5
author:markgalioto
---
# How to Add, Edit, and Remove Exception Tracking
Adding functions to the Exception tracking list allows you to add namespace or classes where [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] tracks exception parameters or variables and collects additional information about each exception that is raised from a namespace or class.  
  
The default list of .NET functions that are monitored for exceptions includes namespaces and functions, some of which have monitoring disabled by default. For more information, see [Using Exception Handlers to Define Critical Exceptions](../../om/manage/Using-Exception-Handlers-to-Define-Critical-Exceptions.md), which includes a list of default exception handlers.  
  
> [!WARNING]  
> Exception tracking is set on the process level. If you add a function to the Exception tracking list for an application that is running in the process and then disable it for a different application running in that process, there will be a conflict and application monitoring will be disabled. To resolve this, you must make the Exception tracking list the same for all applications in the same process.  
  
## Add a Class or Namespace to the Exception Tracking List  
  
#### To add a class or namespace to the exception tracking list  
  
1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.  
  
2.  Right click the application group whose settings you want to modify, and then select **Properties**.  
  
3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.  
  
4.  On the **Advanced settings** page, click **Exception tracking** to open the **Exception tracking class or namespace** page. This is where you can add classes or namespaces where you intend to collect exceptions.  
  
5.  To add a class or namespace, on the **Exception tracking class or namespace** page, click **Add**, select whether you want to collect exceptions for a particular **Namespace or class** or for **All namespaces**, and then type the class or namespace you want to add. The **Enable monitoring** checkbox is selected by default, which means that you want to enable monitoring for this class or namespace. To explicitly disable monitoring of exceptions in a particular class or namespace, clear the checkbox. Click **OK**.  
  
    [!INCLUDE[sc2012sp1note](../../om/manage/includes/sc2012sp1note_md.md)]**All namespaces** is present and enabled in this list by default. However, **All namespaces**, does not include namespaces that have been explicitly disabled.  
  
    > [!IMPORTANT]  
    > Adding Exception Tracking for namespaces or classes that are defined in the .NET Framework as part of mscorlib will not produce any effect.  
  
    > [!NOTE]  
    > The Namespace and Class names are case\-sensitive and should be specified in the following format: Namespace.ClassName  
  
## Edit a Class or namespace on the Exception Tracking List  
  
#### To edit a class or namespace on the exception tracking list  
  
1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.  
  
2.  Right click the application group whose settings you want to modify, and then select **Properties**.  
  
3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.  
  
4.  On the **Advanced settings** page, click **Exception tracking** to open the **Exception tracking class or namespace** page. This is where you can edit the list of classes or namespaces where to look for exceptions.  
  
5.  To edit a class or namespace, on the **Exception tracking class or namespace** page, click **Edit**, modify the settings you want to change, and then click **OK**.  
  
    > [!NOTE]  
    > The Namespace and Class names are case\-sensitive and should be specified in the following format: Namespace.ClassName  
  
## Remove a Class or Namespace on the Exception Tracking List  
  
#### To remove a class or Namespace on the exception tracking list  
  
1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.  
  
2.  Right click the application group whose settings you want to modify, and then select **Properties**.  
  
3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.  
  
4.  On the **Advanced settings** page, click **Exception tracking** to open the **Exception tracking class or namespace** page. This is where you can remove classes or namespaces from the list.  
  
5.  To remove a class or namespace, on the **Exception tracking class or namespace** page, click **Edit**, modify the settings you want to change, and then click **OK**.  
  
    > [!NOTE]  
    > The Namespace and Class names are case\-sensitive and should be specified in the following format: Namespace.ClassName  
  
