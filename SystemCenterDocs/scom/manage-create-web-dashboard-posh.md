---
ms.assetid:
title: How to create a dashboard with the PowerShell widget in the Web console
description: This article describes how to create a new HTML5 dashboard in System Center Operations Manager with the PowerShell widget.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 07/22/2018
ms.custom: na
ms.prod: system-center
monikerRange: 'sc-om-1807'
ms.technology: operations-manager
ms.topic: article
---

# How to create a dashboard with the PowerShell widget in the Web console

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

In System Center Operations Manager version 1801 and higher, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to create a dashboard in the new HTML5 Web console with the PowerShell widget.

The script will typically use the Operations Manager cmdlets to retrieve information from the management group.  It must then use the ScriptContext object to create a Data Object and then add that object to the ReturnCollection property. Typically with the Silverlight-based PowerShell widget, scripts were configured with the variable named $dataObject, and this variable held data returned from ScriptContext object.  However, this widget doesn't support that variable name and will return an error when you attempt to save your changes. Replace this variable name with a custom name such as $results.  

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console.

2. From the left pane in the Web console, select **+ New dashboard**.

    ![Screenshot of the Select New Dashboard in Web console.](./media/create-web-dashboard-alerts/web-console-new-dashboard-01.png)

3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.

    ![Screenshot of the Specify name and description for new dashboard.](./media/create-web-dashboard-alerts/web-console-new-dashboard-02.png)

4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** dropdown list or you can save the dashboard by creating a new management pack by selecting **New** next to the **Management Pack** dropdown list and provide a name, description, and optionally a version number.

    ![Screenshot of Specify name and description for new MP.](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)

5. When you've completed specifying where to save the new dashboard to, select **OK**.

6. Select **Save** after providing a name and description for the new dashboard.

7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard** and **View in fullscreen** options on the top of the page. Select **Add Widget**.

    ![Screenshot of the New dashboard canvas.](./media/create-web-dashboard-alerts/web-console-new-dashboard-04.png)

8. Select **PowerShell Widget** from the **Select Widget** dropdown list.

9. In the PowerShell widget pane, write or copy and paste your PowerShell script into the textbox.

    ![Screenshot of Enter PowerShell script.](./media/create-web-dashboard-posh/add-posh-widget-01.png)  

    The following sample script creates a table of numbered Windows Computer objects and displays the ID, health state, and display name for each.  

    ```
    $class = Get-SCOMClass -Name Microsoft.Windows.Computer  
    $computers = Get-SCOMClassInstance -Class $class  
    $i=1  
    foreach ($computer in $computers)  
    {  
        $results=$ScriptContext.CreateFromObject($computer,"Id=Id,HealthState=HealthState,DisplayName=DisplayName",$null)   
        $results["CustomColumn"]=$i   
        $ScriptContext.ReturnCollection.Add($results)   
        $i++   
    }  
    ```

10. Complete the configuration by providing a **Name**, **Description**, and **Widget refresh interval** (default interval is 5 minutes) for the widget. Select **Save Widget** to save your new dashboard.  

After the widget has been created, it displays the results of your script.  

![Screenshot of PowerShell widget results example.](./media/create-web-dashboard-posh/dashboard-posh-widget-results.png)

## Actions with PowerShell widget
With a PowerShell widget, you can perform such actions as:

- Export the alerts to Excel for further analysis

## Next steps

To learn how to create a dashboard in the new web console with the State widget, see [How create a dashboard with the State widget in the Web console](manage-create-web-dashboard-state.md).
