---
title: How to Configure Error Transmission Settings for Client Monitoring in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f5d5467-2ef2-4ee4-b4a7-7092977127ef
---
# How to Configure Error Transmission Settings for Client Monitoring in Operations Manager
When you enable Client Monitoring for a management group, you can configure it to forward error reports for Microsoft products to Microsoft. Error Transmission settings allow you to specify which error reports are sent to Microsoft and the additional diagnostic data that is included with the error reports.

> [!NOTE]
> For information about enabling the Client Monitoring feature of [!INCLUDE[om12long](../Token/om12long_md.md)], see [How to Configure a Management Server for Client Monitoring](../Topic/How-to-Configure-a-Management-Server-for-Client-Monitoring.md).

### To find the Error Transmission tab of the Global Management Server Settings \- Privacy dialog box

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Settings**.

4.  In the **Settings** pane, expand **Type: General**, right\-click **Privacy**, and then click **Properties**.

5.  In the **Global Management Server Group Settings \- Privacy** dialog box, click the **Error Transmission** tab.

    > [!NOTE]
    > Click **Read the privacy statement** to view the privacy statement.

### To filter errors that are sent to Microsoft

1.  On the **Error Transmission** tab of the **Global Management Server Group Settings \- Privacy** dialog box, click **Filter**.

2.  In the **Error Forwarding Filters** dialog box, select one or more of the options for sources of errors that you do not want forwarded to Microsoft, such as **that come from specific computers**.

3.  In the **Criteria description** text box, click **specific**, and provide the values for the criteria of errors that you do not want forwarded to Microsoft, such as **contoso.com**.

4.  Click **OK** twice.

### To configure diagnostic data sent to Microsoft with error reports

1.  On the **Error Transmission** tab of the **Global Management Server Settings \- Privacy** dialog box, do one or more of the following:

    1.  Select **Upload diagnostic data collection request,** select the additional diagnostic data that you want to send with error reports from computers reporting errors to the management servers, and then forward from the management server to Microsoft with the error reports.

    2.  Set **Maximum number of CAB files to send to Microsoft per error group** to help Microsoft diagnose the error. Ten is the recommended number.

    3.  Select **Display links to solutions from Microsoft on error reporting computers**. A link to available solutions will display to end users after the error is first encountered and the link to the solution is downloaded to the management server.

    4.  Select **Display links to surveys from Microsoft on error reporting computers**.

    5.  Specify the **Default solution link when no Microsoft solution is available**. This could be an internal Web page for technical support, for example.

2.  Click **OK**.

## See Also
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../Topic/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)
[How to Configure Clients for Client Monitoring](../Topic/How-to-Configure-Clients-for-Client-Monitoring.md)
[How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups](../Topic/How-to-Customize-Client-Monitoring-Data-Collection-and-Solution-Response-URLs-for-Error-Groups.md)
[How to Configure a Management Server for Client Monitoring](../Topic/How-to-Configure-a-Management-Server-for-Client-Monitoring.md)
[Forwarding Client Error Reports &#40;Client Monitoring&#41;](../Topic/Forwarding-Client-Error-Reports--Client-Monitoring-.md)

