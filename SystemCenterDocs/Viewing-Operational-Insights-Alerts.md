---
title: Viewing Operational Insights Alerts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a885bba6-4114-4ed2-bd5a-3fff66db27ee
---
# Viewing Operational Insights Alerts
Microsoft Azure Operational Insights is an online service that analyzes installations of Microsoft server software. With [!INCLUDE[omblue_1](../Token/omblue_1_md.md)], you can view Operational Insights alerts in the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console.

Operational Insights collects data from your installations, analyzes it, and generates alerts that identify potential issues \(such as missing security patches\) or deviations from identified best practices with regard to configuration and usage. Operational Insights also provides both current and historical views of the configuration of servers in your environment.

In previous versions of Operational Insights called System Center Advisor, the Advisor agent used a gateway to communicate with the Advisor service, however it is not supported by Operational Insights. Using Operational Insights as an attached service in Operations Manager extends the value of Operational Insights to Operations Manager.

You can learn more about Operational Insights, including the workloads that it analyzes, in the online help system, available at [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=194601](http://go.microsoft.com/fwlink/?LinkID=194601).

Use the following information to configure the Operations console so you can view Operational Insights alerts.

## Pre\-requisites
Before you can view Operational Insights alerts in the Operations console, ensure the following pre\-requisites are met:

-   If you want to view Operational Insights alerts about SharePoint Server 2010 or Lync Server 2010, you need to configure a Run As account. See [Set the Run As Account for SharePoint](http://go.microsoft.com/fwlink/?LinkID=247268) for information about creating this account for SharePoint Server and [Set the Run As Account for Lync Server](http://go.microsoft.com/fwlink/?LinkID=266611) for information for Lync Server.

    > [!NOTE]
    > The Run As account you use must be a Windows account.

## Configure the Operations console to display Operational Insights alerts
Use the following steps to configure the Operations console to view Operational Insights alerts.

1.  On the Administration workspace, click **Operational Insights** and then **Operational Insights Connection** in the navigation pane to open the Operational Insights page in the console.

2.  Click **Register with Operational Insights**.

3.  Follow the instructions in the Operational Insights Onboarding wizard to complete your configuration.

4.  If your environment requires the use of a proxy server to communicate with the internet, configure the proxy server. See [Firewall Information for Operational Insights](http://go.microsoft.com/fwlink/?LinkId=294186) for details on the domains and URLs that need to be accessible through the firewall.

5.  Add computers to analyze with Operational Insights. Click **Operational Insights** and then **Operational Insights Managed** in the navigation pane. Click **Add a Computer**, and then follow the instructions in the UI.

    > [!IMPORTANT]
    > If you have already installed an older Advisor gateway or agent on a computer that you want to view through the Operations console, you need to uninstall System Center Advisor \(through Add\/Remove Programs\) before you can do so.

## View Operational Insights alerts
You can view Operational Insights alerts on the Monitoring workspace. Open the Monitoring workspace, click **Operational Insights**, and then click **Active Alerts** to see the alerts. Click any alert to view detailed information.

An Operational Insights alert contains information about the computer or instance where the alert was discovered and remediation information to address the issue. To view the remediation information, in the **Alert Details** section, click **View additional knowledge**. This will open a KB or TechNet article about the issue detected.

You can also learn more about Operational Insights from an alert by clicking the **Learn more about Operational Insights** link in the **Knowledge** section.

## Manage Operational Insights alerts
You can view, close, or ignore an Operational Insights alert through the Operations console.

To close an alert, click **Close Alert** in the Operational Insights Tasks list.

To ignore an alert, click the specific alert in the results pane, and then click **Ignore Alert**. You can manage alerts, including those that you have ignored, by clicking **Manage Alert Rules**. For more information about ignoring Operational Insights alerts, see [Ignore an Alert](http://go.microsoft.com/fwlink/?LinkID=245622) in the Operational Insights online help system.

## View configuration information
In addition to viewing alerts from Operational Insights, you can also view the configuration information that Operational Insights collects about the computers listed as “Operational Insights Managed.” To view configuration information, from the Operational Insights page on the Monitoring workspace, click **View Configuration** in the Operational Insights Tasks list.

