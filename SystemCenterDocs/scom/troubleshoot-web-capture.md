---
title: Troubleshoot Web capture
description: This article describes how to resolve issues with the Web Recorder feature in System Center Operations Manager 2025.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/06/2026
ms.service: system-center
ms.subservice: operations-manager
ms.topic: troubleshooting-known-issue
monikerRange: 'sc-om-2025'
---

# Troubleshoot Web capture 

This article describes how to resolve issues with the Web Recorder feature in System Center Operations Manager 2025.

## Issue

In System Center Operations Manager 2025, when you start a Web Recorder session, you either get a blank page or the following error message in Internet Explorer:

:::image type="content" source="media/troubleshoot-web-capture/blank-page.png" alt-text="Screenshot showing blank page." :::

:::image type="content" source="media/troubleshoot-web-capture/error-message.png" alt-text="Screenshot showing error message." :::

## Cause

This issue might be due to certain default settings in Internet Explorer and/or security hardening of the OS, hosting the System Center Operations Manager console.  

>[!NOTE]
>The browser recorder feature is compatible only with Internet Explorer and is not supported in Microsoft Edge or other modern browsers. 

## Workaround 

Depending on your environment, you may need some or all of the changes, outlined. To test your progress, attempt to load the feature after each change.  

To resolve this issue, do the following: 

## Enable third-party browser extensions in Internet Explorer 

To enable third-party browser extensions in the Internet Explorer settings, follow these steps: 

1. Open Internet Explorer and navigate to **Tools** > **Internet Options** > **Advanced** tab. 

2. Under **Settings** > **Browsing**, select the checkbox **Enable third-party browser extensions***.
   
   :::image type="content" source="media/troubleshoot-web-capture/internet-options.png" alt-text="Screenshot showing Internet options page." :::

3. Right-click and select **Run as administrator** to load the Operations Manager console as administrator. You should be able to see the web recorder add-in as shown below:

   :::image type="content" source="media/troubleshoot-web-capture/web-recorder-option.png" alt-text="Screenshot showing web recorder option page." :::

If the issue persists, do the following:  

## Modify registry 

To modify the registry, follow these steps: 

>[!NOTE]
>These registry keys are only applied for the current user. Every user using the web recorder feature must perform these steps. 

1. Navigate to the following registry key and add a new DWORD 32-bit value - *TabProcGrowth* and then set it to 0. 
 
   `HKEY_CURRENT_USER\Software\Microsoft\Internet Explorer\Main`

2. Navigate to the following registry key: 

   `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Discardable\PostSetup\Component Categories64\` 

3. Delete the following two subkeys (These are the cached BHO IE objects related to the Web Recorder). This forces Internet Explorer to recache next launch. 

 
   **{00021493-0000-0000-C000-000000000046}** <br>
   **{00021494-0000-0000-C000-000000000046}**

To ensure browser launches the 64-bit version instead of 32-bit, do the following to the IEXPLORE.EXE key: 

1. Navigate to the following registry key: 

   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppPaths\IEXPLORE.EXE` 

2. Change the values to remove the **(x86)** from the path for both the default and path values. See the following example:  

    **Before**: C:\Program Files (x86)\Internet Explorer\IEXPLORE.EXE 
    **After**: C:\Program Files\Internet Explorer\IEXPLORE.EXE 

The Web Recorder feature must now load as expected: 

:::image type="content" source="media/troubleshoot-web-capture/web-recorder-option.png" alt-text="Screenshot showing web recorder option page." :::

You might receive the following error when you start web recording:  

:::image type="content" source="media/troubleshoot-web-capture/internet-explorer-error.png" alt-text="Screenshot showing Internet explorer error." :::

To resolve this, disable the Internet Explorer advanced setting **Enable Enhanced Protection Mode***:  

:::image type="content" source="media/troubleshoot-web-capture/internet-option-disabled.png" alt-text="Screenshot showing Internet option disabled." :::
