---
ms.assetid: 7f64b190-0af1-431d-85ca-6b6ac9f0ce0e
title: Install the Operations Console
description: This article describes how to install the Operations Manager operations console on other servers and computers.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/19/2025
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install the Operations Manager operations console

After you install System Center Operations Manager, you can install the operations console on other servers and computers. For example, you might want to view monitoring data from your desktop computer.

## Prerequisites

Ensure that the computer that will host the operations console meets the minimum [system requirements](./system-requirements.md).

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

## Install the operations console

1. Sign in to the computer that will host the operations console. Use an account that has local administrative credentials.

2. On the Operations Manager installation media, run **Setup.exe**, and then select **Install**.

3. On the **Getting Started** > **Select features to install** page, select **Operations console**. To read more about what each feature provides and its requirements, select **Expand all** (or expand the button next to each feature). Then select **Next**.

4. On the **Getting Started** > **Select installation location** page, accept the default location. Or you can enter a new location or browse to one. Then select **Next**.

5. On the **Prerequisites** page, review and address any warnings or errors that the prerequisites checker returns. Then select **Verify Prerequisites Again**.

6. If the prerequisites checker returns no warnings or errors, the **Prerequisites** > **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration** > **Help improve System Center - Operations Manager** page, select your options. Then select **Next**.

8. If Windows Update isn't enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then select **Next**.

9. Review the options on the **Configuration** > **Installation Summary** page, and then select **Install**.

10. When Setup finishes, the **Setup is complete** page appears. Select **Close**. The operations console then opens.

11. In the operations console, on the **Connect to Server** page, fill in the **Server name** box. Enter the name of the first management server in which you installed in the management group. Then select **Connect**.

> [!IMPORTANT]
> If you plan to edit company knowledge on this computer, you also have to install the [Microsoft Visual Studio 2010 Tools for Office Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=105522).
>
> You can't edit company knowledge by using the x64 version of Microsoft Word 2010. You must install the x86 version of Microsoft Office 2010 or an earlier version.

## Install the operations console from the command prompt

1. Sign in to the server by using an account that has local administrative credentials.

2. Open the Command Prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager **Setup.exe** file is located, and then run the following command:

    ```
    setup.exe /silent /install /components:OMConsole /EnableErrorReporting:[Never|Queued|Always] /SendCEIPReports:[0|1] /UseMicrosoftUpdate: [0|1] /AcceptEndUserLicenseAgreement:[0|1]
    ```

## Related content

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed deployment of Operations Manager](deploy-distributed-deployment.md).
