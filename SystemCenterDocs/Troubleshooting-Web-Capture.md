---
title: Troubleshooting Web Capture
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4355df5c-db7e-4805-94dd-3e5b5281389b
---
# Troubleshooting Web Capture
When you select an option to capture a browser session in [!INCLUDE[om12short](Token/om12short_md.md)], the **Web Recorder** should start, and requests should be recorded as you select them in the browser. If **Web Recorder** does not work correctly, check the following sections to determine a potential cause and to resolve it.

> [!NOTE]
> Web Recorder functionality does not work with Internet Explorer 10 and newer versions on Windows 8 and Windows 8.1.

## Enabling Third\-Party Browser Extensions
Internet Explorer must be configured to allow third\-party extensions on the computer that you are using to perform the capture.

#### To enable third\-party browser extensions

1.  In Internet Explorer, click **Tools**, and then click **Internet Options**.

2.  Click the **Advanced** tab.

3.  Under **Settings**, under **Browsing**, select **Enable third\-party browser extensions**.

## Run As Administrator
If you are using Windows 7 or Windows Server 2008 R2, or if you are using the Windows Vista or Windows Server 2008 operating system with User Account Control \(UAC\) enabled, Internet Explorer must be running as an administrator, or the requests will not be added to the **Web Recorder**. Because the Operations console is starting Internet Explorer, you have to start the Operations console as an administrator.

#### To run the Operations console as administrator

1.  Click **Start**, then **All Programs**, then **System Center Operations Manager 2012**.

2.  Right\-click the **Operations console** icon.

3.  Click **Run as administrator**.

## X64 Version of Internet Explorer
If you are running the Operations console on a 64\-bit operating environment, the Web Recorder might not be displayed when Internet Explorer starts because the x64 version of the add\-on was registered and is not used in the x86 version of Internet Explorer. You have to use the x64 version of Internet Explorer for the capture process.

#### To perform the capture with the x64 version of Internet Explorer

1.  After you start Internet Explorer from the Operations console, close Internet Explorer.

2.  Click the **Start** button, and on the **Start** menu, point to **All Programs**, and then click **Internet Explorer \(64\-bit\)**.

## See Also
[How to Capture Web Application Recording](How-to-Capture-Web-Application-Recording.md)


