---
ms.assetid: 7f64b190-0af1-431d-85ca-6b6ac9f0ce0e
title: How to Install the Operations Console
description: This article describes how to install the Operations Manager Operations console.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Install the Operations console

>Applies To: System Center 2016 - Operations Manager

After you install System Center 2016 - Operations Manager, you can install the Operations console on other servers and computers. For example, you might want to view monitoring data from your desktop computer.

You must ensure that the computer that will host the Operations console meets the minimum system requirements. For more information, see [System Requirements for System Center 2016 - Operations Manager](plan-system-requirements.md)

#### To install the Operations console

1.  Log on to the computer that will host the Operations console with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select **Operations console**. To read more about what each feature provides and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default location of **C:\Program Files\System Center 2016\Operations Manager**, or type a new location or browse to one, and then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again**.

6.  If the Prerequisite checker returns no warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Help improve System Center - Operations Manager** page, select your options, and then click **Next**.

8.  If Windows Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

9. Review the options on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

10. When Setup is finished, the **Setup is complete** page appears. Click **Close**, and the Operations console opens.

11. In the Operations console, on the **Connect to Server** page, type the name of the first management server that you installed in the management group in the **Server name** box, and then click **Connect**.

> [!IMPORTANT]
> If you are going to edit company knowledge on this computer, you also have to install the [Microsoft Visual Studio 2010 Tools for Office Second Edition Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=48217).

> [!IMPORTANT]
> Company knowledge cannot be edited with the x64 version of Microsoft Word 2010. You must install the x86 version of Microsoft Office 2010 or an earlier version to edit knowledge.

### To install the Operations console from the Command Prompt 

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    ```
    setup.exe /silent /install /components:OMConsole /EnableErrorReporting:[Never|Queued|Always]/SendCEIPReports:[0|1] /UseMicrosoftUpdate: [0|1]
    ```

## Next steps

- See [Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
