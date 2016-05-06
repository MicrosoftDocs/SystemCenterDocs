---
title: Working with Sensitive Data for .NET Applications
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69f2c1e7-4732-49f0-8643-4d95bdbb144c
---
# Working with Sensitive Data for .NET Applications
Here are some ways to work with sensitive data and .NET Application Performance Monitoring in [!INCLUDE[om12long](Token/om12long_md.md)].

## Masking Sensitive Data for .NET Applications
Masking sensitive data allows you to use a regular expression to filter out common parameters and insert **\*** or some other character in place of the real value. This is used for functions and exceptions where you might capture sensitive information, such as credit card information, passwords, and other personally identifiable information.

#### To mask sensitive data for .NET applications

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, expand **Management Pack Objects**, click **Rules**, and then click **change scope** in the right\-hand side of the information bar to see the current scoping.

2.  In the **Scope Management Packs objects** page, select **.NET Application Monitoring Agent** to the current scope, and click **OK**.

3.  To override the **Sensitive Data Rules** property of the **Apply APM Agent Configuration** rule, right\-click **Apply APM Agent configuration**, select **Overrides**, select **Override the Rule**, and then select **For all objects of class: .NET Application Monitoring Agent**.

4.  On the **Override Properties** page, in the **Override\-controlled parameters** section, select **Sensitive data rules**.

5.  In the **Sensitive data rules** row, in the **Override Value** column, enter the formula for the mask you want to apply, using the syntax `<Hidden><Expression>((pwd|password)=?)[^;]*</Expression><CompareExpression>((pwd|password)=?)[^;]*</CompareExpression><Replacement>$1*****</Replacement><Type>all</Type></Hidden>`, where the <Expression> and <CompareExpression> use regular expression syntax and <Replacement> defines the characters to use when masking out the actual value of the parameter.

6.  In the **Management Pack** section, select an existing management pack or create a new one where the override will be stored.

7.  Click **OK**.

## Avoid Collecting Sensitive Data
If you do not want to get this sensitive information at all, here is how to avoid it. Some applications will pass sensitive information embedded in the exceptions raised or parameters collected. To avoid the sensitive information, you can disable monitoring for specific methods and restrict collection of specific exceptions. To do this, you disable parameter collection of a method or you disable collection of exceptions thrown from specific namespaces or classes.

#### To disable parameter collection of a method

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, click **.NET Application Performance Monitoring**, right\-click the application group you want to modify, and then click **Properties**.

2.  On the **What to Monitor** tab, select the application component you want to change and click **Customize**.

    > [!NOTE]
    > Methods can also be defined at the application group level and be applied to all application components. To do this, follow the same steps after clicking the **Advanced Settings** button on the **Server\-Side Defaults** tab.

3.  On the **Modifying Settings** page, click **Set Methods**. Specify the method name for the function where you want to disable parameter collection, and then clear the **Collect function parameters** checkbox.

    Additionally, if you do not want to continue monitoring this method, clear the **Enable monitoring** checkbox.

4.  Click **OK**.

#### To disable collection of exceptions

1.  To open the .NET Application Performance Monitoring template, in the [!INCLUDE[om12short](Token/om12short_md.md)] console, in the navigation pane, click the **Authoring** button, click **Management Pack Templates**, click **.NET Application Performance Monitoring**, right\-click the application group you want to modify, and then click **Properties**.

2.  On the **Server\-Side Defaults** tab, click **Advanced Settings**.

3.  On the **Advanced settings** page, click **Exception Tracking**.

4.  On the **Exception tracking list** page, click **Add**, enter the namespace or class where you want to stop collecting exceptions, and then clear the **Enable monitoring** checkbox.

5.  Click **OK**.

## See Also
[Operations Manager Privacy Statement](http://go.microsoft.com/fwlink/?LinkID=190868)


