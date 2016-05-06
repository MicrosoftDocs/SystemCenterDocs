---
title: How to Create a Single URL Web Application Monitor
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 184a6363-44d5-4c54-bdf8-da324cbcbd7f
---
# How to Create a Single URL Web Application Monitor
The most basic **Web Application Transaction Monitoring** template includes a single request. This may be sufficient for testing the general availability of a website, or as the basis for creating a more complex monitoring scenario by adding requests either manually or by capturing them in a browser session.

### To create a single URL web application transaction monitoring template

1.  Start the Operations console with an account that has Author user rights in the management group.

2.  Open the **Authoring** pane.

3.  Right\-click **Management Pack Templates**, and then select **Add Monitoring Wizard**.

4.  On the **Select Monitoring Type** page, select **Web Application Transaction Monitoring**, and then click **Next**.

5.  On the **General Properties** page, do the following:

    1.  In the **Name** and **Description** boxes, type a name and an optional description.

    2.  Select a management pack in which to save the monitor, or click **New** to create a new management pack. For more information, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

    3.  Click **Next**.

6.  On the **Web Address** page, do the following:

    1.  In the **URL** box, specify that the request uses http or https.

    2.  Type the URL to connect to.

    3.  Click the **Test** button to perform a test connection to the URL. If the connection succeeds, click **Details** to inspect the response time and other details of the connection. This information can be valuable if you decide to manually edit the request after the template is created.

        > [!NOTE]
        > The test is performed from the workstation that you are using to run the wizard. If this workstation cannot access the website, this test fails. When the template is completed, the test is run from the watcher nodes that you specify.

    4.  Click **Next**.

7.  On the **Watcher Node** page, do the following:

    1.  Select one or more [Watcher Nodes](../Topic/Watcher-Nodes.md) to run the web requests.

    2.  Specify the frequency to run the web request in the **Run this query every** box.

    3.  Click **Next**.

8.  On the **Summary** page, review the summary of the monitor, and then click **Create**.

## See Also
[How to Edit Settings or Requests in a Web Application](../Topic/How-to-Edit-Settings-or-Requests-in-a-Web-Application.md)
[How to Capture Web Application Recording](../Topic/How-to-Capture-Web-Application-Recording.md)

