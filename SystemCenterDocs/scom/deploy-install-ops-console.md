---
ms.assetid: 7f64b190-0af1-431d-85ca-6b6ac9f0ce0e
title: Install the Operations Console
description: This article describes how to install the Operations Manager Operations console on other servers and computers.
author: jyothisuri
ms.author: jsuri
ms.date: 03/19/2025
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install the Operations console

After you install System Center - Operations Manager, you can install the Operations console on other servers and computers. For example, you might want to view monitoring data from your desktop computer.

You must ensure that the computer that will host the Operations console meets the minimum system requirements. For more information, see [System Requirements for System Center - Operations Manager](./system-requirements.md)

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

## Install the Operations console

Follow these steps to install the Operations console:

1. Sign in to the computer that will host the Operations console with an account that has local administrative credentials.

2. On the Operations Manager installation media, run **Setup.exe**, and select **Install**.

3. On the **Getting Started**, **Select features to install** page, select **Operations console**. To read more about what each feature provides and its requirements, select **Expand all**, or expand the buttons next to each feature, and select **Next**.

4. On the **Getting Started**, **Select installation location** page, accept the default location or enter a new location or browse to one, and select **Next**.

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify Prerequisites Again**.

6. If the Prerequisite checker returns no warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration**, **Help improve System Center - Operations Manager** page, select your options, and select **Next**.

8. If Windows Update isn't enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and select **Next**.

9. Review the options on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

10. When the Setup is finished, the **Setup is complete** page appears. Select **Close**, and the Operations console opens.

11. In the Operations console, on the **Connect to Server** page, enter the name of the first management server that you installed in the management group in the **Server name** box, and select **Connect**.

> [!IMPORTANT]
> If you're going to edit company knowledge on this computer, you also have to install the [Microsoft Visual Studio 2010 Tools for Office Second Edition Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=48217).

> [!IMPORTANT]
> Company knowledge can't be edited with the x64 version of Microsoft Word 2010. You must install the x86 version of Microsoft Office 2010 or an earlier version to edit knowledge.

## Install the Operations console from the command prompt

Follow these steps to install the Operations console from the command prompt:

1. Sign in to the server by using an account that has local administrative credentials.

2. Open the command prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager setup.exe file is located, and run the following command:

    ```
    setup.exe /silent /install /components:OMConsole /EnableErrorReporting:[Never|Queued|Always] /SendCEIPReports:[0|1] /UseMicrosoftUpdate: [0|1] /AcceptEndUserLicenseAgreement:[0|1]
    ```

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
