---
title: Management Pack Lifecycle
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Management Pack Lifecycle

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager uses management packs contain monitoring settings for applications and services. Ideally, a management pack tells you everything you want to know about the application or technology that you are monitoring and nothing that you do not want to know. Management packs are designed to provide a useful monitoring experience for most environments, however you will want to test, tune, and tailor each management pack to provide optimal results for your organization's needs.  
  
The management pack lifecycle, described in the following table, is the recommended approach to using management packs. The sections following the table provide details for each stage.  
  
|Stage|Description|  
|---------|---------------|  
|Review and evaluate management packs in a pre\-production environment|Before you deploy a management pack in your production environment, you should familiarize yourself with the contents of the management pack and guide, and import the management pack in a pre\-production or test environment. You can also view the management pack in a virtual machine environment.|  
|Tune the management pack settings and save in a customized management pack|Use overrides to tune the settings of a management pack-such as monitors, rules, object discoveries, and attributes-to better meet your organization's needs. You should save overrides to a management pack that you create.|  
|Deploy management packs into a production environment|Export the management pack with overrides that is associated with the management pack that you are going to deploy, and import management packs in your production environment.|  
|Maintain management pack|After deployment, a management pack might need additional tuning, such as in following circumstances:<br><br>-   Environmental changes, such as new hardware or new operating system<br>-   Adding a new application to the production environment<br />-   Upgrading a version of an application<br>-   When a new or updated version of the management pack is available<br>-   Policy changes, which result in more or less monitoring based on business needs|  
  
## Review and evaluate  

Each management pack should be accompanied by a management pack guide that is installed to the same folder as the management pack. A management pack guide contains instructions for installing and configuring the management pack, and information about the management pack, such as objects that the management pack discovers and how health rolls up. You can use this information to help you customize the management pack for your purposes. You should always review the management pack guide before you import the management pack.  
  
A tool for reviewing the contents of a sealed management pack is the MPViewer, which can display the following contents of a management pack: rules, monitors, views, tasks, console tasks, and reports. MPViewer will also display the knowledge associated with the particular management pack item. You can install and use [MPViewer](https://github.com/dani3l3/mpviewer) on any computer on which the Operations Manager Operations console is installed.   
  
> [!NOTE]  
> Microsoft neither endorses nor provides support for this third\-party product.   
  
When you have a new management pack, you should import it to a *pre\-production* environment. In Operations Manager, it is a best practice to have a production implementation that is used for monitoring your production applications and a pre\-production implementation that has minimal interaction with the production environment. The pre\-production management group is used for testing and tuning management pack functionality before the management pack is deployed in the production environment.  
  
To accurately measure the data that a management pack gathers, you need to expose the agent to the demands of your production environment. The hardware of the management server in the pre\-production environment should reflect the hardware that is in use in your production environment. Your pre\-production management group should have the same management packs imported to the management server as the production management group. To test interoperability, your pre\-production environment should also include the same types of server roles that are in your production environment, just on a smaller scale.  
  
You can assign an Operations Manager agent to more than one management group, which is called *multihoming*. If you multihome a representative subset of agents in your production environment and your pre\-production environment, the pre\-production environment should give you much of the information you need to correctly tune the management pack. For more information on multihoming agents, see [Configuring Agents](configuring-agents.md).  
  
## Tune and customize  

You can use overrides to refine the settings of a monitoring object in Operations Manager, including monitors, rules, object discoveries, and attributes. You should create a management pack in which to save customizations that you make.  

To effectively tune the monitoring configuration of your IT services, which may involve one or more management packs depending on the complexity of that service, you should involve the service owner or subject matter experts, a representative from the service desk, a representative from the operations team members who monitor the alerts and events and take action when something requires attention, and the engineering team responsible for the Operations Manager infrastructure. Depending on the service that is monitored by the management pack(s), you might also include representation from the networking and security teams.  Those responsible for the Operations Manager infrastructure might not have the knowledge and experience with the service to effectively tune the management pack(s) without expert input.  

Start by reviewing the most common alerts in an effort to improve monitoring accuracy by focusing on high-volume alerts.  Identify the following and prioritize based on impact:

- Number and percentage of alerts caused by existing/known problems
- Number and percentage of repeated or duplicate alerts.  May indicate additional tuning is necessary or there is a potential issue to investigate further.
- Number and percentage of alerts indicating performance or availability issues
- Ratio of alerts to tickets generated
- Alerts whose resolution state has been set to a state indicating the workflow is generating a high volume of alerts and is determined through investigation to be faulty by operations or tier-2 support

Leverage the following reports to determine if additional tuning is required:

- Most Common Alerts Report
- Alerts Report
- Data Volume by Management Pack
 
The following reports are important to validate we are efficiently monitoring the service in its entirety, and there isn’t:

- Configuration churn due to discovery rules running too frequently or there is a property/attribute being collected that changes frequently 
- Performance data being collected too frequently or doesn’t need to be collected because the organization will not use it in a report, view, or dashboard
- Event data being collected which adds no value and is only enabled for troubleshooting (short period of time)
- Health State flip flopping due to misconfiguration, bug, or other symptom
- Alert rule with high repeat count


At a minimum, each workflow should be evaluated according to the following criteria:  

- Measurable and identifiable occurrence.  Anything not aligning with that category is disabled.
- When the alert occurs, do we know how to resolve it?
- Exceptions (warnings) that provide a proactive notice of potential service impact are exposed to the NOC/Service Desk, besides any Incident (error) that indicates disruption of service. 
- Is discovery running too frequent?
- Do we need to collect this performance data?  Is it useful?
- Is the alert understandable, relevant, and up to date?
- Should the monitor auto-resolve if the symptom/problem corrects itself?
 
  
### What to Tune  
  
-   Discovery frequency  
  
-   Monitor thresholds  
  
-   Targets  
  
-   Intervals for script-based rules/monitors and performance collection rules  
  
-   Parameters  
  
### Tips  
  
-   Review any new alerts reported for servers monitored with the new management pack. You can use the Alerts and Most Common Alerts reports to help you discover your most common alerts. When you first install a management pack, it tends to discover a multitude of previously unknown issues. Monitor the alerts to determine potential areas of concern  
  
-   Override the monitor or rule as applicable for all objects of a particular class, a group, or a specific object.  
  
-   Disable the monitor or rule if the issue is not severe enough to warrant an alert and you do not need to be made aware of the specific situation being monitored.  
  
-   Change the threshold of the monitor that is generating the alert if you want the underlying condition to be monitored, but the alert is being generated before the condition is actually a problem for your particular environment.  
  
-   When you set overrides for a management pack, save them to a management pack that is named ManagementPack\_Override, where ManagementPack is the name of the sealed management pack to which the overrides apply. 
  
  
## Deploy  

When you are satisfied with the performance and results of the management pack in the pre\-production environment, you can deploy the management pack and its customizations in the production environment. The management pack in which you saved the customizations must be exported so that you can import it to other computers. For more information, see [How to Import, Export, and Remove Management Packs](how-to-import-remove-export-management-packs.md). The management pack that contains the overrides that you set is dependent on the original management pack and can be imported only to management groups that have the original management pack installed.  
  
## Maintain  

After a management pack has been deployed, you should periodically evaluate its performance and results in the production environment to ensure that it continues to meet business needs. The following list describes common events that might require changes to a management pack:  
  
-   **Environmental changes, such as new hardware or a new operating system**  
  
    When you are testing new hardware or a new operating system that you plan to add to your production environment, you should include existing management packs in your test plan to identify any additional tuning that might be necessary. For a new operating system, you might need to import new management packs specific to that operating system.  
  
-   **Adding a new application to the production environment**  
  
    A new application might require a new management pack or adjustments to existing management packs.  
  
-   **Upgrading a version of an application**  
  
    When organizations upgrade application versions, they usually either upgrade in stages, during which both versions of the application will exist in the network, or upgrade all installations of the application at one time. After testing the management packs with the new version and making any necessary adjustments, you should use the same approach for deploying the management packs that you use for deploying the upgrades. If both versions of the application will be in use at one time, you should install management packs appropriate for each version. If all installations of the application will be upgraded at one time, remove the management pack for the old version of the application and install the management pack for the new version.  
  
-   **When a new or updated version of the management pack is available**  
  
    You should use the pre\-production environment to review and tune new or updated versions of a management pack.  
  
-   **Policy changes**  
  
    Ongoing changes in your business or organization might require adjustments to management packs to accomplish more monitoring or less monitoring.  
  
## Best Practices for change control  

The following are some best practices to follow when managing Operations Manager management packs:  
  
-   Maintain an archive of management pack versions to enable you to roll back changes when necessary. An efficient method for maintaining the archive is by using version control software, such as Microsoft Team Foundation Server or SharePoint Server. Another method is to use a file share on the network with individual folders for each management pack version.  
  
-   When you set overrides for a management pack, save them to a management pack that is named *ManagementPack*\_Override, where *ManagementPack* is the name of the sealed management pack to which the overrides apply. For example, overrides to the management pack Microsoft.SQLServer.2012.Monitoring.mp would be saved to Microsoft.SQLServer.2012.Monitoring\_Overrides.xml. For more information, see [Creating a Management Pack for Overrides](How-to-create-a-management-pack-for-overrides.md).  
  
-   When a management pack is updated, update the corresponding \_Overrides.xml file with the new version number. You must use an XML editor to update the version number of the \_Overrides.xml file. If you make changes to an \_Overrides.xml file but do not change the version attribute, you can import the file but the settings in the file will not be applied.  
  
-   Document the overrides that you make to management packs. When you set an override, add an explanation of the action you are taking and the reason for it to the description field by clicking **Edit** in the Details pane of the Override Properties dialog box. You may also want to maintain a spreadsheet or other form to document changes that you make to management packs.  
  
## Next steps

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](How-to-Create-a-Management-Pack-for-Overrides.md).  

- To understand what an Operations Manager management pack is and how it helps you proactively monitor your services and applications, see [What is in an Operations Manager Management Pack](What-Is-in-an-Operations-Manager-Management-Pack.md).  
 
- See [How to Import, Export, and Remove an Operations Manager Management Pack](how-to-import-remove-export-management-packs.md) to perform common administrative tasks with management packs in your management group.

-  