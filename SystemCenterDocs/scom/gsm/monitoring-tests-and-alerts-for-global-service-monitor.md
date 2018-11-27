---
title: "Monitoring Tests and Alerts for Global Service Monitor | Microsoft Docs"
ms.custom: ""
ms.date: 4/26/2018
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.tgt_pltfrm: ""
ms.topic: article
applies_to: System Center 2016 - Operations Manager
ms.assetid: 9f769a08-3ab4-4b73-ba14-6f0498d0081d
author: jyothi
ms.author: magoedte
manager: carmonm
---
# Monitoring Tests and Alerts for Global Service Monitor
## Monitoring Tests and Alerts for Web Application Availability  
  
#### To view overall web application health  
  
1.  For a view of the general health of each application that you are monitoring, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Monitoring**, and then click **Application Monitoring**.  
  
2.  Click **Web Application Availability Monitoring**, and then click **Web Applications State**. This is the best view to see the overall health of each application.  
  
     The alert state for each application is displayed according to the alert configurations that you used when you set up the tests:  
  
    -   Green=Healthy  
  
    -   Yellow=Error  
  
    -   Red=Warning  
  
3.  To see details about a particular application, click the application and then, in the **Tasks** pane, click **Health Explorer**.  
  
     The Health Explorer lets you to see the health states for each criterion so that you can pinpoint what caused the application to show an error or warning.  
  
#### To view alerts and alert details  
  
1.  To see active alerts for the applications that you are monitoring, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**, and then, in the **Web Application Availability Test Actions** section, click **View active alerts**. As with the application health, the alert state is displayed in the color according to your alert configurations.  
  
2.  To see alert details, click the alert to see the **Alert Details** pane.  
  
3.  To see more details about an alert, double-click the alert to open the **Alert Properties** page.  
  
     On the **Alert Properties** page **General** tab, you can reassign the alert, see the alert description, and change the alert status to **New** or, if you have resolved the issue, **Closed**. Use **Previous** and **Next** to scroll through the alerts for easy review. When you are finished viewing or changing properties, click **OK** to save your changes.  
  
    > [!IMPORTANT]
    >  The Alert Context tab displays details that describe why the alert was generated.  
  
#### To view data for individual URLs and locations  
  
1.  For a view of each test that you configured in the Web Application Availability template, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**, and then, in the **Web Application Availability Test Actions** section, click **View test state**. If there are alerts, you can see them listed in the **Test State** pane. As with the application health, the alert state is displayed in the color according to your alert configurations.  
  
2.  > [!NOTE]
    >  A test is one URL and one location.  
  
3.  To see the details of a particular test, click the test and then, in the **Tasks** pane, click **Health Explorer**.  
  
     The Health Explorer lets you see the health states for each criterion so that you can see in detail what caused the test to show an error or warning.  
  
## Monitoring Tests and Alerts for Visual Studio Web Tests  
  
#### To view overall web application health  
  
1.  For a view of the general health of each application that you are monitoring, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Monitoring**, and then click **Application Monitoring**.  
  
2.  Click **Visual Studio Web Test Monitoring**, and then click **Visual Studio Web Test Status**. This is the best view to see the overall health of each application.  
  
3.  To see details about a particular application, click the application and then, in the **Tasks** pane, click **Health Explorer**.  
  
     The Health Explorer lets you to see the health states for each criterion so that you can pinpoint what caused the application to show an error or warning.  
  
#### To view alerts and alert details  
  
1.  To see active alerts for the applications that you are monitoring, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**, and then, in the **Visual Studio Web Tests Actions** section, click **View active alerts**. If there are alerts, you can see them listed in the **Active Alerts** pane. As with the application health, the alert state is displayed in the color according to your alert configurations.  
  
2.  To see alert details, click the alert to see the **Alert Details** pane.  
  
3.  To see more details about an alert, double-click the alert to open the **Alert Properties** page.  
  
     On the **Alert Properties** page **General** tab, you can reassign the alert, see the alert description, and change the alert status to **New** or, if you have resolved the issue, **Closed**. Use **Previous** and **Next** to scroll through the alerts for easy review. When you are finished viewing or changing properties, click **OK** to save your changes.  
  
#### To view data for individual tests and locations  
  
1.  For a view of each test that you configured in the Visual Studio Web Test template, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Administration**, click **[!INCLUDE[gsmshort](../includes/gsmshort-md.md)]**, and then, in the **Visual Studio Web Tests Actions** section, click **View test state**. If there are alerts, you can see them listed in the **Test State** pane. As with the application health, the alert state is displayed in the color according to your alert configurations.  
  
  > [!NOTE]
  >  A test is one .webtest and one location.  
  
2.  To see the details of a particular test, click the test, and then, in the **Tasks** pane, click **Health Explorer**.  
  
     The Health Explorer lets you see the health states for each criterion so that you can see in detail what caused the test to show an error or warning.
