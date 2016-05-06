---
title: Monitoring Java Applications
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13f2661d-ad31-4d01-92b4-fb9b2e7173f8
---
# Monitoring Java Applications
Java Application Performance Monitoring \(APM\) in [!INCLUDE[omblue_1](Token/omblue_1_md.md)] lets you monitor Java applications to get details about application performance and exception events that can help you determine the root causes of problems. The System Center 2012 Management Pack for Java Application Performance Monitoring lets you monitor Java application performance and exception events by using [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Application Advisor. With [!INCLUDE[omblue_2](Token/omblue_2_md.md)] Application Advisor, you can investigate method and resource timing for performance events, stack traces for exception events, Java specific counters for events \(such as Average Request Time, Requests Per Second, JVM Memory, and Class Loader\), and run some of the standard Application Performance Monitoring reports. Additionally, you get [!INCLUDE[omblue_2](Token/omblue_2_md.md)] level alerting on Java application server counters. Download the Management Pack for Java Application Performance Monitoring from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=313918).

Java Application Performance Monitoring shares many concepts with .NET Application Performance Monitoring. However, there are some important differences, including: object hierarchy, the method for working with overrides and alerting \(Java Application Performance Monitoring has no authoring and configuration template, so you change configurations with management pack overrides\), and sever\-level information is not handled in Java Application Performance Monitoring reports.

## Supported Configurations
The Management Pack for Java Application Performance Monitoring requires Windows Server 2012 R2, [!INCLUDE[omblue_1](Token/omblue_1_md.md)], and [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)].

Supported configurations:

-   Tomcat 5, Tomcat 6, and Tomcat 7

    -   Windows

    -   Linux

-   Java JDK 5, Java JDK 6

-   Web Technologies

    -   GenericServlet

    -   Struts

    -   Struts2

    -   Axis2

## Prerequisites
To run the Management Pack for Java Application Performance Monitoring, you must have the Management Pack for Java Enterprise Edition \(JEE\) configured for deep monitoring. This management pack monitors JEE application servers and provides initial application level discovery. For more information, see [How to Configure Monitoring for Java Applications](How-to-Configure-Monitoring-for-Java-Applications.md) and the Management Pack Guide for JEE for your particular type of application server, available on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=325020).

## Java Application Performance Monitoring Topics

-   [How to Configure Monitoring for Java Applications](How-to-Configure-Monitoring-for-Java-Applications.md)

-   [How to Monitor Java Applications](How-to-Monitor-Java-Applications.md)

-   [Strategies for Monitoring a New Java Application](Strategies-for-Monitoring-a-New-Java-Application.md)


