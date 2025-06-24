---
title: Connect to the Operations and Web Console
description: This article describes how to open and configure the Operations Manager consoles to view monitoring data and perform administration in the management group.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 12dba3ee-d394-4575-8fc0-2c403b2818ed
---

# Connect to the Operations and Web Console



System Center Operations Manager includes two consoles:

- The Operations console
- The Web console

To view operational data and administer the management group configuration, you use the Operations console.  The Web console provides a light-weight interface with the essential functionality to view the monitoring data, which avoids having to manage the lifecycle deployment of the Operations console.  

In this section, we provide information on how to connect to the Operations and Web consoles.

## Connect to the Operations console

The System Center Operations Manager Operations console can be installed on any computer that meets the [system requirements](./system-requirements.md). When you open the Operations console on a management server, the console connects to that management server; however, you can use the following procedure to connect to a different management server. When you initially open the Operations console on a computer that isn't a management server, you must specify the management server to connect to. The following image shows the **Connect To Server** dialog.  

![Screenshot showing Dialog box to connect console to server.](./media/manage-consoles-how-to-connect/om2016-operations-console-connect-to-server.png)  

::: moniker range="= sc-om-2016"

### Connect an Operations console to a management server

Follow these steps to connect an Operations console to a management server:

1. To open the Operations console, select **Start** and then select **Microsoft System Center 2016\Operations Console**.

2. In the **Connect To Server** dialog, enter the server name or select a server from the list. (In the image above, the console hasn't yet connected to any management group. If the console has previously connected to any management servers, the servers will be listed in **Recent Connections**.)  

::: moniker-end

::: moniker range=">= sc-om-2019"

### Connect an Operations console to a management server

Follow these steps to connect an Operations console to a management server:

1. To open the Operations console, select **Start** and then select **Microsoft System Center\Operations Console**.

2. In the **Connect To Server** dialog, enter the server name or select a server from the list. (In the image above, the console hasn't yet connected to any management group. If the console has previously connected to any management servers, the servers will be listed in **Recent Connections**.)  

::: moniker-end

The Operations console opens with the focus on the Monitoring workspace.

### Change the management server that the Operations console is connected to

1. In the Operations console, select **Tools**, and then select **Connect...** as shown in the following image, which will open the **Connect To Server** window.  

    ![Screenshot showing Connect option from the Tools menu.](./media/manage-consoles-how-to-connect/om2016-operations-console-menu-connect.png)  

## Connect to the Web console

In System Center Operations Manager, the Web console provides a monitoring interface for a management group that can be opened on any computer that has connectivity to the Web console server. The Web console is limited to My Workspace and the Monitoring workspace.  

::: moniker range="sc-om-2016"

> [!NOTE]  
> You must use Internet Explorer 11 to connect to the web console in System Center 2016 - Operations Manager to access the Silverlight-enabled dashboards. In addition, the Operations Manager web console requires that JavaScript be enabled and Silverlight version 5 is installed on the client computer. To enable JavaScript in Internet Explorer, open **Internet Options**, and select the **Security** tab. Select the zone for the Web console (Internet, Local intranet, or Trusted sites), and select **Custom level**. Enable **Active scripting**, select **OK**, select **OK**, and then connect to the Web console.  The web console doesn't support running IE in Compatibility View, otherwise you'll receive a blank page when attempting to access the console. To turn off Compatibility View feature, please see [How to use Compatibility View in Internet Explorer](https://mskb.pkisolutions.com/kb/2536204)

::: moniker-end

By default, the web console session is limited to 30 minutes. You can change this limit by editing the web.config file (C:\Program Files\Microsoft System Center\Operations Manager\\WebConsole\WebHost is the default path) and changing the *autoSignOutInterval* value from **30** to a shorter or longer interval, or disable the session limit by changing the value to **0**, as shown in the following example.  

```  
<connection autoSignIn="true" autoSignOutInterval="0">  
```  

> [!NOTE]  
> After you change the web.config file, you must open a new Web console session for the changes to take effect.  

### Connect to a Web console  

- Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console.  

    For information on installing the Web console, see [Install the Operations Manager Web console](~/scom/deploy-install-web-console.md).  

## Next steps

In the Operations console, you view monitoring data, manage monitoring configuration, create your own custom views and dashboards that are personalized for your experience, and perform management group configuration administration by [Using the Operations Manager Operations console](welcome.md).
