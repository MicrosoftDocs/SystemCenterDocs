---
title: Tuning Monitoring by Using Targeting and Overrides
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c0f5967-227b-480c-a84f-965c7c232513
---
# Tuning Monitoring by Using Targeting and Overrides
When you import a management pack, [!INCLUDE[om12long](Token/om12long_md.md)] discovers the objects defined by the management pack and begins applying the management pack’s rules and monitors to the discovered objects. You should always import a new management pack in a pre\-production environment first so that you can evaluate the management pack and adjust or tune the management pack as necessary to meet your business needs.

To tune a management pack effectively, you should involve the service owner or subject matter experts, the operations team members who monitor the alerts and events and take action when something requires attention, and the engineering team responsible for the Operations Manager infrastructure. Depending on the service that is monitored by the management pack, you might also include the networking or security teams.  Those responsible for the Operations Manager infrastructure might not have the knowledge and experience with the service to effectively tune the management pack without expert input.

### Tuning Approach
For servers or applications, tune from the highest severity alerts and dependencies to the lowest. Look at alerts first, then open the Health Explorer to gather more detailed information for the problem. Validate results of the alerts generated, verify scope of monitoring against intended targets \(servers or services\), and ensure the health model is accurate.

Each rule should be evaluated according to the following criteria:

-   **Actionability**: An alert is actionable if it tells you what went wrong and how to fix it. When alerts are generated that do not require any action, consider disabling alerting for the rule.

-   **Validity**: An alert is valid if the issue that generated the alert can be confirmed and the issue actually occurred at the moment the alert was generated.

-   **Suppression**: There should be only one alert stating the issue occurred.

### What to Tune

-   Discovery frequency

-   Monitor thresholds

-   Targets

-   Intervals

-   Parameters

### Tips

-   Import a single management pack at a time.

-   Review any new alerts reported for servers monitored with the new management pack. You can use the Alerts and Most Common Alerts reports to help you discover your most common alerts. When you first install a management pack, it tends to discover a multitude of previously unknown issues. Monitor the alerts to determine potential areas of concern

-   Override the monitor or rule as applicable for a particular object type, a group, or a specific object.

-   Disable the monitor or rule if the issue is not severe enough to warrant an alert and you do not need to be made aware of the specific situation being monitored.

-   Change the threshold of the monitor that is generating the alert if you want the underlying condition to be monitored, but the alert is being generated before the condition is actually a problem for your particular environment.

-   When you set overrides for a management pack, save them to a management pack that is named ManagementPack\_Override, where ManagementPack is the name of the sealed management pack to which the overrides apply. For example, overrides to the management pack Microsoft.InformationWorker.Office.XP.mp would be saved to Microsoft.InformationWorker.Office.XP\_Overrides.xml..

## Tuning Monitoring by Using Targeting and Overrides topics

-   [Using Classes and Groups for Overrides in Operations Manager](Using-Classes-and-Groups-for-Overrides-in-Operations-Manager.md)

-   [How to Override a Rule or Monitor](How-to-Override-a-Rule-or-Monitor.md)

-   [How to Enable or Disable a Rule or Monitor](How-to-Enable-or-Disable-a-Rule-or-Monitor.md)

-   [Using the Enforced Attribute in Overrides](Using-the-Enforced-Attribute-in-Overrides.md)

-   [How to Enable Recovery and Diagnostic Tasks](How-to-Enable-Recovery-and-Diagnostic-Tasks.md)

## Other resources for this component

-   [TechNet Library main page for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=223634)

-   [Operations Guide for System Center 2012 - Operations Manager](Operations-Guide-for-System-Center-2012---Operations-Manager.md)

-   [Managing Discovery and Agents](Managing-Discovery-and-Agents.md)

-   [Using Management Packs](Using-Management-Packs.md)


