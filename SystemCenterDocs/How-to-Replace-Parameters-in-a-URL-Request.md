---
title: How to Replace Parameters in a URL Request
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bdc68ab7-419e-4696-a756-27f5862b02a3
---
# How to Replace Parameters in a URL Request
When you capture a web application by using the Web Application Editor, it can include unique information in one or more requests that changes each time you connect to the application. This information is typically included in the response to a request and then used by one or more subsequent requests.

For example, an application might create a unique session ID when a user logs on. This session ID must be included in each request after the logon process. Without the correct session ID, each of these requests fails. Because you do not know what this value is until the first request is run, it cannot be explicitly included in the configuration of the request. If you create the web application by recording a browser session, the session ID is collected in the URL of each request. However, when the application is run, the requests fail because the session ID will have a value that is different from the recorded session ID.

To configure such an application, you can extract a context parameter from the body of the response of one request and use the value of that parameter in one or more subsequent requests. You then replace the explicit value in subsequent requests with a variable that represents the parameter. Each time the synthetic transaction is run, the parameter is populated in the request where it is defined. When the variable is used in the subsequent requests, it is replaced with the collected value before the request is sent to the application.

A single application can use any number of context parameters. Any number of requests can use a single parameter but must be run after the request where the parameter is defined.

## Session ID Example
Consider the example where an application creates a session ID when a user logs on. This session ID is required in each request after the logon page. To implement this scenario, you have to capture the session ID when it is first generated, and then use that value in each subsequent request.

You start by using the process described in [How to Capture Web Application Recording](../Topic/How-to-Capture-Web-Application-Recording.md) to capture the logon and subsequent actions. The recorded session for logging on to the application and performing some actions might look similar to the following example.

```html
http://www.myapp.com/home.aspx
http://www.myapp.com/search.aspx?query=testing&sessionid=32793279321721
http://www.myapp.com/results.aspx?sessionid=32793279321721
http://www.myapp.com/submit.aspx?sessionid=32793279321721
```

In this request sequence, the session ID is created by the first request and used in the second, third, and fourth requests. When you run this monitor, it fails because the first request generates a new session ID that could not match the session ID that was used when the session was captured.

To configure this request sequence with parameter replacement, you have to create an extraction rule on the first request to create a context parameter for the session ID. The extraction rule inspects the body of the request to locate the value for the `sessionid` variable. You would then modify the subsequent requests to use this parameter instead of the value for the session ID.

The modified requests look similar to the following example.

```html
http://www.myapp.com/home.aspx
http://www.myapp.com/search.aspx?query=testing&sessionid=$ParametersContext/sessionID$
http://www.myapp.com/results.aspx?sessionid=$ParametersContext/sessionID$
http://www.myapp.com/submit.aspx?sessionid=$ParametersContext/sessionID$

```

## Creating an Extraction Rule
Context parameters are collected by an *extraction rule*, and each extraction rule collects a single context parameter. You create an extraction rule in the **Properties** dialog box of the request that initially generates the required data. To identify the value to extract, you must view the body of the response returned from the particular request. You can either view the source of the page returned in the browser or use a tool that lets you inspect the details of HTTP responses. You cannot view the text by using the Web Application Editor.

When you have identified the request that contains the information you have to extract, you view the **Extraction Rules** tab in the properties of that request and create one or more extraction rules. The details of each extraction rule are shown in the following table.

|Option|Description|
|----------|---------------|
|Context parameter name|Enter the name to give the context parameter.|
|Starts with|Enter the text in the body of the response that identifies the start of the parameter value. You should specify enough characters to ensure that the string is unique. The value for the parameter starts immediately after the last specified character.|
|Ends with|Enter the text in the body of the response that identifies the end of the parameter value. The value for the parameter ends immediately before the first specified character.|
|Index|If the text in the **Starts with** box occurs more than one time, this value indicates which value to use. If the text only appears one time, or the first occurrence of it shows the text to extract, the value should be 0. If the second value should be extracted, the value should be 1, and so on.|
|Ignore case during search for matching text|Specifies whether to ignore the case of the characters being searched by the **Starts with** and **Ends with** boxes.|
|Perform URI encoding of extracted strings|Specifies whether to encode the extracted string after it is collected.|

## Inserting a Parameter into a Request
You use a parameter in a request by replacing the explicit value with a variable representing the parameter. The format of the variable is `$ParametersContext/<ContextParameterName>$`. When the request is run, the variable is replaced with the data extracted by the parameter.

You can insert the variable into the request by using one of the two following methods:

-   In the **Request Properties** dialog box, click the **General** tab, and then click **Request URL** to modify the request URL for the request.

-   In the **Request Properties** dialog box, click the **General** tab, and then click the **Insert parameter** button. Use the **Insert Parameter** dialog box for the request. This is accessed from the **Insert parameter** button on the **General** tab in the **Request Properties** dialog box for the request.

## Sample Web Application Using Parameter Extraction
The following procedure provides an example of using parameter extraction in a web application. This example performs a query for the first entry in the **Popular Now** section of the Bing home page. Because this value changes regularly, you have to first connect to the main page and collect the search term from the body of the response. You then use this term to build the request to perform the actual search.

The main Bing page is shown below with the **Popular Now** section highlighted.

![](../Image/OM2007_UsersGuide_BingHomepage.gif)

To determine where in the response body the search term appears, you can view the source of the page. A portion of the source is shown below with the HTML code of the **Popular Now** section. In this HTML code, you only need the search string which is highlighted in the following illustration. The request is formed from **http:\/\/www.bing.com** followed by this string.

![](../Image/OM2007_UsersGuide_PopularNowSearchStringHTML.gif)

You could just pull out the term itself, but it is more straightforward to include the entire string in the parameter. This string is preceded by the characters **<h3>Popular now<\/h3><ul><li><a href\="** and ends with the next occurrence of **"**. Those are the values that you will use when you define the parameter extraction.

#### To record a sample web application

1.  Use the procedure in [How to Capture Web Application Recording](../Topic/How-to-Capture-Web-Application-Recording.md) to record a web application.

2.  While recording, connect to **http:\/\/www.bing.com**.

3.  Optionally, use the option on your browser to view the source of the Bing home page and locate the **Popular Now** section of the HTML code.

4.  Click the first search term under **Popular Now**.

5.  Save the recording to the web application.

6.  Remove the last request because this is not required. To remove the last request, select the request, and then click **Delete** in the **Actions** pane. The resulting requests should look similar to the following URLs:

    ![](../Image/OM2007_UsersGuide_WebAppRecorded.gif)

#### To create an extraction rule

1.  Select the first request, and then click **Properties** in the **Actions** pane.

2.  Select the **Extraction Rules** tab.

3.  Click **Add**. The **Add Extraction Rule** dialog box opens.

4.  In the **Add Extraction Rule** dialog box, in the **Context parameter name** box, type **SearchString**.

5.  In the **Starts with** box, type **<h3>Popular now<\/h3><ul><li><a href\="**.

6.  In the **Ends with** box, type **"**. The extraction rule should look similar to the following illustration.

    ![](../Image/OM2007_UsersGuide_ExtractionRule.gif)

7.  Click **OK** to save and close the extraction rule.

8.  Click **OK** to save and close the request.

#### To insert a parameter into a request

1.  Select the second request, and then click **Properties** in the **Actions** pane.

2.  On the **General** tab, click **Insert parameter**.

3.  In the **String** box, delete all text after **www.bing.com\/**.

4.  With the cursor positioned at the end of the URL, just after **www.bing.com**, select **SearchString** in the **Parameters** box, and then click **Insert**. This inserts the variable `$ParametersContext/SearchString$`. The final request looks similar to the following illustration.

    ![](../Image/OM2007_UsersGuide_InsertParameter.gif)

5.  Click **OK** to close the dialog box.

6.  Click **OK** to save and close the request. The modified request sequence should look similar to the following illustration.

    ![](../Image/OM2007_UsersGuide_WebAppModified.gif)

7.  Click **Apply** to apply the changes, and then close the **Web Application Editor**.

