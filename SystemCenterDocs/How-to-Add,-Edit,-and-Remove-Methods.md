---
title: How to Add, Edit, and Remove Methods
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84bf3d38-dda8-49c7-a7af-c400835ab2e1
---
# How to Add, Edit, and Remove Methods
Methods define entry points used to start measuring for performance events and to monitor for exceptions. If the application defines custom entry points that are not directly called from .NET, these entry points might not be monitored because we don’t that calls to this function are not part of an existing transaction. Methods also let you make fine\-grained changes to how data is collected by .NET Application Performance Monitoring. You can create a method for a specific function and then disable monitoring or disable the collection of parameters. This allows you to ensure that functions working with sensitive data are not going to send that data to the development team who might be working with performance events.

## Add a Method

#### To add a method

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group whose settings you want to modify, and then select **Properties**.

3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Set Methods** to open the **Methods list** page. This is where you can add methods.

5.  To add a method, on the **Methods list** page, click **Add**, type the method name and in the **Settings** section, select if you want to **Enable monitoring**, set a **Sensitivity threshold** for this method, and **Collect function parameters**. Click **OK** and the application performance monitoring service will add this method to the list of monitored methods.

    > [!IMPORTANT]
    > Adding Methods that are defined in the .NET Framework as part of mscorlib will not produce any effect.

    > [!NOTE]
    > The method name is case\-sensitive and should be specified in the following format: Namespace.ClassName.MethodName

## Edit a Method

#### To edit a method

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group whose settings you want to modify, and then select **Properties**.

3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Set Methods** to open the **Methods list** page. This is where you can edit methods.

5.  To edit a method, on the **Methods list** page, click **Edit**, make your changes, and then click **OK**.

    > [!NOTE]
    > The method name is case\-sensitive and should be specified in the following format: Namespace.ClassName.MethodName

## Remove a Method

#### To remove a method

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](../Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, and then click **.NET Application Performance Monitoring**.

2.  Right click the application group whose settings you want to modify, and then select **Properties**.

3.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.

4.  On the **Advanced settings** page, click **Set Methods** to open the **Methods list** page. This is where you can remove methods.

5.  To remove a method, on the **Methods list** page, select the method you want to remove, click **Remove**, and then click **OK**.

