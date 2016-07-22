---
title: Projector Sample Scenario: Authoring a Report to Display Schema Extensions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c0ac60c-1a0c-4601-9e74-4c6de496ce36
---
# Projector Sample Scenario: Authoring a Report to Display Schema Extensions
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>In this sample scenario, you will import a custom management pack that extends the data warehouse so you can manage projectors in your organization. This will allow you to use a custom projector form to enter information about projectors.</para>
    <para>The <link xlink:href="6438afdd-c997-4b64-9961-2abc0cac9e9b">Directly Authoring a Management Pack File to Manage Projectors</link> topic describes how to create the custom Servicemanager.projector.mp management pack, which is referred to in this scenario.</para>
    <para>The projector sample scenario includes the following steps:</para>
    <list class="nobullet">
      <listItem>
        <para>Step 1: Import the management packs that define the new projector configuration item class.</para>
      </listItem>
      <listItem>
        <para>Step 2: Populate the database with information about the projectors that you want to manage.</para>
      </listItem>
      <listItem>
        <para>Step 3: Create the List of Projectors report, which displays all the projector configuration items that you have previously created.</para>
      </listItem>
      <listItem>
        <para>Step 4: View the List of Projectors report in the Service Manager console.</para>
      </listItem>
    </list>
  </introduction>
  <procedure>
    <title>
      <?Comment ak: Work withMIao, and Rekha. THis is being sent to China testing group. 2011-11-02T12:39:00Z  Id='1?>Step1: To import the management packs <?CommentEnd Id='1'
    ?>that define the new projector configuration item class</title>
    <steps class="ordered">
      <step>
        <content>
          <para>
            <?Comment ak: From where? 2010-08-04T08:50:00Z  Id='2?>Copy the following files<?CommentEnd Id='2'
    ?>:</para>
          <list class="bullet">
            <?Comment ak: The files need to bebundeledand then import the bundled file. 2011-11-02T12:38:00Z  Id='3?>
            <listItem>
              <para>ServiceManager.Projector.mp</para>
            </listItem>
            <listItem>
              <para>Datawarehouse.Projector.mp</para>
            </listItem>
            <listItem>
              <para>New_CI_lab.dll Datawarehouse.Projector.mp<?CommentEnd Id='3'
    ?></para>
            </listItem>
          </list>
          <para>And then, paste the files in your Service Manager installation folder.</para>
          <para>For example, paste the files to the following location: C:\Program Files\Microsoft System Center\Service Manager 2012.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Follow these steps to import the ServiceManager.Projector.mp file:</para>
          <list class="ordered">
            <listItem>
              <para>In the <token>smcons</token>, click <ui>Administration</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Administration</ui> pane, click <ui>Management Packs</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Tools</ui> pane, double-click <ui>Import Management Pack</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Select Management Pack to Import</ui> dialog box, select the <ui>MP files(*.mp)</ui> file type option, select the <ui>Servicemanager.projector.mp</ui> file, and then click <ui>Open</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Import Management Packs</ui> dialog box, click <ui>Import</ui>.</para>
            </listItem>
            <listItem>
              <para>Wait for the import success message, and then click <ui>OK</ui>.</para>
            </listItem>
          </list>
        </content>
      </step>
      <step>
        <content>
          <para>Import the Datawarehouse.Projector.mp file by following the same steps.</para>
          <alert class="note">
            <para>Depending on your configuration, the import of a management pack might take half an hour.</para>
          </alert>
        </content>
      </step>
    </steps>
  </procedure>
  <procedure>
    <title>Step2: To create configuration items in the database for the projectors that you want to manage</title>
    <steps class="ordered">
      <step>
        <content>
          <para>Close and then reopen the <token>smcons</token>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <token>smcons</token>, click <ui>Configuration Items</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Configuration Items</ui> pane, expand <ui>Projectors</ui>, and then select <ui>All Projectors</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Tasks</ui> pane, click <ui>Create Projector</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Enter information about a projector in the projector form, and then click <ui>Submit and Close</ui>. </para>
          <alert class="note">
            <para>In the <ui>Serial Number</ui> field, make sure that you enter only numbers; otherwise, the submission fails.</para>
          </alert>
        </content>
      </step>
      <step>
        <content>
          <para>Repeat this procedure for several projectors.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <procedure>
    <title>Step3: To create the List of Projectors report</title>
    <steps class="ordered">
      <step>
        <content>
          <para>After you import the management packs in the previous procedures, ensure that the dimension has deployed successfully. To do this, run the following SQL query on the data warehouse management server, and verify that the query runs without any error.</para>
          <code>SELECT * FROM DWDataMart.dbo.ProjectorDim</code>
        </content>
      </step>
      <step>
        <content>
          <para>On the data warehouse management server, start SQL Server Business Intelligence Development Studio. To do this, click <ui>Start</ui>, click <ui>Programs</ui>, point to <ui>Microsoft SQL Server 2008</ui>, and then click <ui>SQL Server Business Intelligence Development Studio</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In SQL Server Business Intelligence Development Studio, click <ui>File</ui>, point to <ui>New</ui>, and then click <ui>Project</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>New Project</ui> dialog box, select <ui>Report Server Project Wizard</ui> in the <ui>Visual Studio installed templates</ui> list, and then click <ui>OK</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Complete the Report Wizard as follows:</para>
          <list class="ordered">
            <listItem>
              <para>On the <ui>Welcome</ui> page, click <ui>Next</ui>.</para>
            </listItem>
            <listItem>
              <para>On the <ui>Select the Data Source</ui> page, click <ui>Edit</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Connection Properties</ui> dialog box, select the data warehouse in the <ui>Server Name</ui> box, and select the <ui>SCDM</ui> database in the <ui>Select or enter a database name</ui> box.</para>
            </listItem>
            <listItem>
              <para>Select <ui>Test Connection</ui>, and then click <ui>OK</ui> in the <ui>Test results</ui> dialog box.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Connection Properties</ui> dialog box, click <ui>OK</ui>.</para>
            </listItem>
            <listItem>
              <para>On the <ui>Select the Data Source</ui> page in the Report Wizard, select <ui>Make this a shared data <?Comment TN: If this is a check box, please add that descriptor. 2009-12-28T13:17:00Z  Id='4?>source<?CommentEnd Id='4'
    ?></ui>, and then click <ui>Next</ui>.</para>
            </listItem>
          </list>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Design the Query</ui> page, click <ui>Query Builder</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Query Designer</ui> page, click the <ui>Add Table</ui> icon.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Add Table</ui> dialog box, select the <ui>ProjectorDim</ui>, <ui>ProjectorOwnedByUserFact</ui>, and the <ui>UserDim</ui> tables, click <ui>Add</ui>, and then click <ui>Close</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Drag the <ui>ProjectorOwner_UserDimKey</ui> field from the <ui>ProjectorOwnedByUserFact</ui> table into the <ui>UserDimKey</ui> field in the <ui>UserDim</ui> table.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>ProjectorDim</ui> table, select the following fields: <?Comment TN: List? 2009-12-28T13:17:00Z  Id='5?><ui>Make</ui>, <ui>Model</ui>, <ui>SerialNumber</ui>, <ui>Location</ui> and <ui>Condition</ui>. <?CommentEnd Id='5'
    ?></para>
          <para>In the <ui>UserDim</ui> table, select the <ui><?Comment TN: E-mail? 2009-12-28T13:17:00Z  Id='6?>Email<?CommentEnd Id='6'
    ?></ui> field.</para>
          <para>All selected fields should now display in the <ui>Grid</ui> pane.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Query Designer</ui> click <ui>OK</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Report Wizard</ui>, click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Select the Report Type</ui> page, select <ui>Tabular</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Design the Table</ui> page, select all the fields that are listed under <ui>Available fields</ui>. To do this, press the CTRL and select each field.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Click <ui>Details</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Choose the Table Style</ui> page, select a color, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Choose the Deployment Location</ui> page, leave the default <ui>Report server</ui> value. In the <ui>Deployment folder</ui> <?Comment TN: Is it a text box you type in? 2009-12-28T13:17:00Z  Id='7?>box<?CommentEnd Id='7'
    ?>, type <userInput>Microsoft.SystemCenter.Reporting.Folder.ServiceManager/ServiceManager.Console.Reporting.ConfigurationManagement</userInput>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Completing the Wizard</ui> page, type <userInput>List of Projectors</userInput> in the <ui>Report name</ui> box, and then <?Comment ak: You can add other elements to the report in the "Design" view. Extra credit for: Adding parameters to the report by right-clicking on the "Parameters" folder in the "Report Data" pane to the left of the report. Adding charts to the report. This can be done by moving the report fields and title box down in the report field, right clicking on the report field and choosing &gt; Insert &gt; Chart. 2009-12-28T13:17:00Z  Id='8?>click<?CommentEnd Id='8'
    ?> <ui>Finish</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Click <ui>Build</ui>, and then click <ui>Deploy Report &lt;report name&gt;</ui>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <procedure>
    <title>Step4: To view the List of Projectors report in the Service Manager console</title>
    <steps class="ordered">
      <step>
        <content>
          <para>On the Service Manager management server, open the <token>smcons</token>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <token>smcons</token>, click <ui>Reporting</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Reporting</ui> pane, click <ui>Configuration Management</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Configuration Management</ui> pane, select the <ui>List of Projectors</ui> report.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Tasks</ui> pane, click the <ui>Execute Report</ui> task.</para>
        </content>
      </step>
      <step>
        <content>
          <para>View the report.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics />
</developerHowToDocument>