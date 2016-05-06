---
title: How to Capture Web Application Recording
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb965b50-f319-46da-96b6-ca224c22f61e
---
# How to Capture Web Application Recording
The fastest and easiest way to create a **Web Application Transaction Monitoring** template with multiple requests is to record a session from Internet Explorer. Using the **Web Recorder**, you can interactively record a sequence of actions that are stored in the request sequence with default settings. After the session has been recorded, you can manually edit the individual requests if any of them require unique configuration.

You can run the **Web Recorder** to create a **Web Application Transaction Monitoring** template, or you can run it from an existing template to add additional requests.

### To record a new web application

1.  Start the Operations console with an account that has Author user rights in the management group.

2.  Open the **Authoring** pane, expand **Management Pack Templates**, and then click **Web Application Transaction Monitoring**.

3.  In the **Actions** pane, click **Record a browser session**.

4.  In the **Web Application Editor** dialog box, do the following:

    1.  Type a name and optionally a description of the recording. The name appears in the **Monitoring** pane.

    2.  Select a management pack in which you want to save your Web Application object, and then click **OK**. For more information, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

5.  Click **Start capture**.

    Follow the steps in [To use the Web Recorder](../Topic/How-to-Capture-Web-Application-Recording.md#WebRecorder).

### To add a web recording to an existing browser session

1.  Start the Operations console with an account that has Author user rights in the management group.

2.  Open the **Authoring** pane, expand **Management Pack Templates**, and then click **Web Application Transaction Monitoring**.

3.  Select the template that you want to edit, and then click **Edit Web Application settings**.

4.  Select the location in the browser session to include the recorded requests.

5.  Click **Start capture** in the **Actions** pane.

    Follow the steps in [To use the Web Recorder](../Topic/How-to-Capture-Web-Application-Recording.md#WebRecorder).

## <a name="WebRecorder"></a>To use the Web Recorder

1.  When you start the capture, Internet Explorer opens with the **Web Recorder** in the navigation pane. If you do not see the **Web Recorder**, see [Troubleshooting Web Capture](../Topic/Troubleshooting-Web-Capture.md).

2.  In the browser window, follow the actions that you want to be monitored. For example, you might click some links or add a product to a shopping cart. As you perform actions, they are recorded in the **Web Recorder** pane.

3.  When you have completed the recording, click **Stop** in the **Web Recorder** pane. Internet Explorer closes, and the actions you performed are added to the **Web Application Editor**.

4.  Optionally, click **Run Test** in the **Actions** pane to immediately run the recorded actions and view the results. At this point, you might encounter the following errors:

    -   If the web application requires authentication, running a test of the web application might fail. While running the test, credentials that have been configured for this web application are not used. If the site you are testing does not explicitly require authentication, the test might still succeed. In the **Actions** pane, under **Web Application**, you can click **Configure Settings** for any website to select authentication settings.

    -   If you see an error message that the server name or address cannot be resolved, but you can access the web application through Internet Explorer while not recording a session, you might have to configure your proxy settings. In the **Actions** pane, under **Web Application**, you can click **Configure Settings** for any website to select authentication settings.

5.  Optionally, add requests or edit captured requests by using the **Insert request** or the **Properties** options in the **Actions** pane.

    For more information, see [How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md).

## See Also
[Troubleshooting Web Capture](../Topic/Troubleshooting-Web-Capture.md)

