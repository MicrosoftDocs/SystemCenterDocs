title: System Center 1711 Preview - Operations Manager Release Notes
description: This article describes issues and workarounds for System Center 1711 Preview Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/10/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.assetid: 
ms.technology: operations-manager
ms.topic: article
---

# System Center 1711 Preview - Operations Manager Release Notes

The following release notes apply to System Center 1711 Preview - Operations Manager.

## Telemetry

**Description:** Usage telemetry collected from Application Insights and presented in HTLM5 dashboards are enabled by default and cannot be disabled in this preview.  For more information on what telemetry is collected by Application Insights, see [Usage analysis with Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-usage-overview).

**Workaround:** None

## Performance widget

**Description:** Data points on the horizontal and vertical axis of performance widget are getting overlapped at the end of the respective axis. The tool tip which is displayed on hover of the performance graph displays the object ID in this preview.

**Workaround:** None

## Topology widget

**Description:** The delete image action “X” on top of the uploaded image in the topology image is not working.

**Workaround:** None

**Description:** Repositioning the state indicator icons with Firefox or IE browser is not working.

**Workaround:** You can reposition them using Edge or Chrome browser.

## Localization

**Description:** Sign in screen is not localized in this preview

**Workaround:** None

**Description:** Send us feedback pane is not localized in this preview

**Workaround:** None

**Description:** Edit company knowledge action in the alerts drill down page is not working for localized languages in this preview

**Workaround:** None

## My workspace

**Description:** When there are no views in My Workspace and you add a view to My Workspace from the Web console, the view is not displayed.

**Workaround:** You must access My Workspace from Operations Console one time. Afterwards, this behavior never reoccurs.  

## Using Operations Console with SSL

**Description:** While accessing Web console with HTTPS, during authentication certificate validation is bypassed between two AppPools - **OperationsManager** and **MonitoringView**

**Workaround:** None

## Edit Company Knowledge

**Description:** If the company knowledge of an alert/monitor/rule is already saved while editing in the Operations console and then the company knowledge of the same alert/monitor/rule is edited and saved using the new HTLM5 dashboards in the Web console, the content that was saved originally using the Operations console is overridden with the content saved through the Web console.

**Workaround:** None

**Description:** When you access Silverlight dashboards, a “Web Console Configuration Required” message is displayed.

**Workaround:** 

1. Click **Configure** in the dialog box.
2. When prompted to run or save the SilverlightClientConfiguration.exe file, click **Save**.
3. Run the SilverlightClientConfiguration.exe file.
4. Right-click the .exe file, click **Properties**, and then select the **Digital Signatures** tab.
5. Select the certificate that has Digest Algorithm as SHA256, and then click **Details**.
6. In the **Digital Signature Details** dialog box, click **View Certificate**.
7. In the dialog box that appears, click **Install Certificate**.
8. In the **Certificate Import** wizard, change the store location to **Local Machine**, and then click **Next**.
9. Select the Place all certificates in the following store option and then select **Trusted Publishers**.
10. Click **Next** and then click **Finish**.
11. Refresh your browser window.
