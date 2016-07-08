---
title: Setting Up a Service Manager 2012 Lab Environment with Production Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34e9880c-5faf-4e67-ac1b-7043ab4dc8ad
 

















---
# Setting Up a Service Manager 2012 Lab Environment with Production Data
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This section explains how to create a lab environment and populate it with production data so that upgrades can be performed and tested before an actual upgrade in the production environment. The procedures in this section show you how to configure <token>smlong12</token> in a lab environment with production data. You then perform an in-place upgrade to <token>smlong12</token> SP1. It is important to follow the steps in this section in sequence.</para>
    <list class="ordered">
      <listItem>
        <para>
          <link xlink:href="03747a1c-cdb9-47ce-83d1-55ee9d6c8119">How to Install an Additional Management Server in the Production Service Manager Management Group</link>
        </para>
      </listItem>
      <listItem>
        <para>Install any cumulative updates that you installed on the Primary Management server on the Secondary Management Server.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="48fa12ca-e61b-4658-8eda-f9cc3af16dfc">How to Copy the Workflow Assembly Files</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="4bf9b574-f6d0-46f1-a989-aa0464f9a1ed">How to Disable Service Manager Connectors in the Production Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="1317d2e6-b47b-41c0-826b-f7a4b3adf11b">How to Disable Email Notifications  in the Production Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>Disable all workflows in the production environment that you do not want to be running in the lab environment.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="b4f30bdb-d45e-4390-b873-509d0b012398">How to Stop Service Manager Services on the Secondary Management Server</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="4ebe6cb4-0352-4c71-b2a9-0a235c0102d5">How to Back Up the Production Service Manager Database</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="0b055821-641a-4f09-96d9-14b1f84a950d">How to Enable Service Manager Connectors  in the Production Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="441c09d3-16e6-4cc3-a242-83aad9ec3c4a">How to Enable Email Notifications in the Production Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>Enable all workflows in the Production Service Manager environment that you disabled in step 6.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="acc6c46d-3377-47ce-9c94-ce20997d376f">How to Restore the Service Manager Database in the Lab Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="7d3b8b19-77f9-4a96-a117-8ffef08da01a">How to Prepare the Service Manager Database in the Lab Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>If possible, block communications to SQL from the Secondary Management server to the production Service Manager Database server.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="c6eecbd1-f867-4050-b66f-de9427410bb7">How to Start Service Manager Services on the Secondary Management Server</link>
        </para>
      </listItem>
      <listItem>
        <para>Verify that the lab environment works. Try to open the console on the Secondary Management server and see if you can connect to the console. Confirm that the Data Warehouse and Reporting do not appear. After you confirm that this works, complete the rest of the steps.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="df0bc01c-a314-441f-a983-27dfd92f95c0">How to Promote a Secondary Management Server in a Lab Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="20ec2aaa-9fee-463b-a1d7-9cb272d8dd73">How to Enable the Connectors in the Lab Environment</link>
        </para>
        <alert class="note">
          <para>Do not enable or delete the Operations Manager alert connector in the lab environment. This will cause the alert connector in the production environment to fail.</para>
        </alert>
      </listItem>
      <listItem>
        <para>If you want to test the email notification and incoming email functionality, use a separate SMTP instance to send emails to eliminate flooding the inboxes of users with test emails. To test the incoming email feature, you can point to a test share and drop the eml files into this share when you are ready to test.</para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="239ee325-d396-4e8c-8d1e-adc7d28f3f04">How to Install a New Data Warehouse Server in the Lab Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="ab0ec9ba-ba35-4a29-b933-472dfd18276a">How to Register the Data Warehouse Server in the Lab Environment</link>
        </para>
      </listItem>
      <listItem>
        <para>Back up this lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.</para>
      </listItem>
      <listItem>
        <para>If you are able to successfully complete all the previous steps, you are ready to attempt the in-place upgrade.</para>
      </listItem>
      <listItem>
        <para>Test everything. Document any discrepancies and fixes. Send feedback through the MS Connect web site.</para>
      </listItem>
      <listItem>
        <para>Backup the <token>smshort</token> lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.</para>
      </listItem>
      <listItem>
        <para>The lab environment is now ready for <token>smlong12</token> SP1 in-place upgrade.</para>
      </listItem>
    </list>
  </introduction>
  <?Comment TN: DO NOT USE the related topics tag in this sort of parent node topic. Reserve its use only for topics that do not provide any navigation function. 2012-08-06T12:40:00Z  Id='1?>
  <relatedTopics>
    <?CommentEnd Id='1'
    ?>
  </relatedTopics>
</developerConceptualDocument>
