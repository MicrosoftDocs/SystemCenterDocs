---
title: How to Install the Operations Console
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f88980f5-521f-41cc-98db-997db0019c0f
---
# How to Install the Operations Console

>Applies To: System Center 2016 Technical Preview - Operations Manager

After you install System Center 2016 Technical Preview - Operations Manager, you can install the Operations console on other servers and computers. For example, you might want to view monitoring data from your desktop computer. Before you install an Operations Manager Operations console, you must install [Microsoft .NET Framework 3.5 SP1 hotfix](http://go.microsoft.com/fwlink/p/?LinkID=194637).

You must ensure that the computer that will host the Operations console meets the minimum system requirements. For more information, see [System Requirements for System Center Technical Preview](../../system-requirements/System-Requirements-for-System-Center-Technical-Preview.md)

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
> If you are going to edit company knowledge on this computer, you also have to install the [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime](http://go.microsoft.com/fwlink/p/?LinkId=74969).

> [!IMPORTANT]
> Company knowledge cannot be edited with the x64 version of Microsoft Word 2010. You must install the x86 version of Microsoft Office 2010 or an earlier version to edit knowledge.

### To install the Operations console by using the Command Prompt window

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    ```
    setup.exe /silent /install /components:OMConsole /EnableErrorReporting:[Never|Queued|Always] /SendCEIPReports:[0|1] /UseMicrosoftUpdate: [0|1]
    ```

## See Also
[Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md)



