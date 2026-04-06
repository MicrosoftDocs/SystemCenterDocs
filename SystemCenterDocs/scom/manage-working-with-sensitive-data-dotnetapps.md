---
title: Work with sensitive data for .NET applications
description: This article describes how to filter sensitive data collected by Application Performance Monitoring.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: engagement-fy23, UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 69f2c1e7-4732-49f0-8643-4d95bdbb144c
---

# Work with sensitive data for .NET applications

Here are some ways to work with sensitive data and .NET Application Performance Monitoring in System Center - Operations Manager.  

## Mask sensitive data for .NET applications

Masking sensitive data allows you to use a regular expression to filter out common parameters and insert \**\** or some other character in place of the real value. This is used for functions and exceptions where you might capture sensitive information, such as credit card information, passwords, and other customer information.  

1. To open the .NET Application Performance Monitoring template, in the Operations Manager Operations console, in the navigation pane, select **Authoring**, expand **Management Pack Objects**, select **Rules**, and select **change scope** at the right-hand side of the information bar to see the current scoping.  

2. In the **Scope Management Packs objects** page, select **.NET Application Monitoring Agent** to the current scope, and select **OK**.  

3. To override the **Sensitive Data Rules** property of the **Apply APM Agent Configuration** rule, right-click **Apply APM Agent configuration**, select **Overrides**, select **Override the Rule**, and select **For all objects of class: .NET Application Monitoring Agent**.  

4. On the **Override Properties** page, in the **Override-controlled parameters** section, select **Sensitive data rules**.  

5. In the **Sensitive data rules** row, in the **Override Value** column, enter the formula for the mask you want to apply, using the syntax `<Hidden><Expression>((pwd|password)=?)[^;]*</Expression><CompareExpression>((pwd|password)=?)[^;]*</CompareExpression><Replacement>$1*****</Replacement><Type>all</Type></Hidden>`, where the \<Expression\> and \<CompareExpression\> use regular expression syntax and \<Replacement\> defines the characters to use when masking out the actual value of the parameter.  

6. In the **Management Pack** section, select an existing management pack or create a new one where the override will be stored.  

7. Select **OK**.  

## Avoid Collecting Sensitive Data

If you don't want to capture this sensitive information at all, here's how to avoid it. Some applications will pass sensitive information embedded in the exceptions raised or parameters collected. To avoid the sensitive information, you can disable monitoring for specific methods and restrict the collection of specific exceptions. To do this, disable parameter collection of a method or disable collection of exceptions thrown from specific namespaces or classes.  

### Disable parameter collection of a method  

1. To open the .NET Application Performance Monitoring template, in the Operations Manager Operations console, in the navigation pane, select **Authoring**, select **Management Pack Templates**, select **.NET Application Performance Monitoring**, right-click the application group you want to modify, and select **Properties**.  

2. On the **What to Monitor** tab, select the application component you want to change and select **Customize**.  

    > [!NOTE]  
    > Methods can also be defined at the application group level and be applied to all application components. To do this, follow the same steps after selecting the **Advanced Settings** button on the **Server-Side Defaults** tab.  

3. On the **Modifying Settings** page, select **Set Methods**. Specify the method name for the function where you want to disable parameter collection, and then clear the **Collect function parameters** checkbox.  

    Additionally, if you don't want to continue monitoring this method, clear the **Enable monitoring** checkbox.  

4. Select **OK**.  

### Disable collection of exceptions  

1. To open the .NET Application Performance Monitoring template, in the Operations Manager Operations console, in the navigation pane, select **Authoring**, select **Management Pack Templates**, select **.NET Application Performance Monitoring**, right-click the application group you want to modify, and select **Properties**.  

2. On the **Server-Side Defaults** tab, select **Advanced Settings**.  

3. On the **Advanced settings** page, select **Exception Tracking**.  

4. On the **Exception tracking list** page, select **Add**, enter the namespace or class where you want to stop collecting exceptions, and then clear the **Enable monitoring** checkbox.  

5. Select **OK**.  
