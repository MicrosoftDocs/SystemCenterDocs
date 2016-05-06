---
title: Management Pack Life Cycle
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4aff9aea-e074-4103-b9db-f8dd327817d8
---
# Management Pack Life Cycle
[!INCLUDE[om12long](./Token/om12long_md.md)] uses management packs to extend monitoring functionality. Ideally, a management pack tells you everything you want to know about the application or technology that you are monitoring and nothing that you do not want to know. Management packs are designed to provide a useful monitoring experience for most environments, however you will want to test, tune, and tailor each management pack to provide optimal results for your organization’s needs.

The management pack life cycle, described in the following table, is the recommended approach to using management packs. The sections following the table provide details for each stage.

|Stage|Description|
|---------|---------------|
|Review and evaluate management packs in a pre\-production environment|Before you deploy a management pack in your production environment, you should familiarize yourself with the contents of the management pack and guide, and import the management pack in a pre\-production or test environment. You can also view the management pack in a virtual machine environment.|
|Tune the management pack settings and save in a customized management pack|Use overrides to tune the settings of a management pack—such as monitors, rules, object discoveries, and attributes—to better meet your organization’s needs. You should save overrides to a management pack that you create.|
|Deploy management packs into a production environment|Export the management pack with overrides that is associated with the management pack that you are going to deploy, and import management packs in your production environment.|
|Maintain management pack|After deployment, a management pack might need additional tuning, such as in following circumstances:<br /><br />-   Environmental changes, such as new hardware or new operating system<br />-   Adding a new application to the production environment<br />-   Upgrading a version of an application<br />-   When a new or updated version of the management pack is available<br />-   Policy changes, which result in more or less monitoring based on business needs|

## <a name="bkmk_reviewandevaluate"></a>Review and Evaluate
Each management pack should be accompanied by a management pack guide that is installed to the same folder as the management pack. A management pack guide contains instructions for installing and configuring the management pack, and information about the management pack, such as objects that the management pack discovers and how health rolls up. You can use this information to help you customize the management pack for your purposes. You should always review the management pack guide before you import the management pack.

A tool for reviewing the contents of a sealed management pack is the MPViewer, which can display the following contents of a management pack: rules, monitors, views, tasks, console tasks, and reports. MPViewer will also display the knowledge associated with the particular management pack item. You can install and use MPViewer on any computer on which the Operations Manager Operations console is installed. Search the [MSDN Blogs](http://blogs.msdn.com/b/dmuscett/archive/2012/02/19/boris-s-tools-updated.aspx) at http:\/\/blogs.msdn.com\/b\/dmuscett\/archive\/2012\/02\/19\/boris\-s\-tools\-updated.aspx for the most recent version of MPViewer.

> [!NOTE]
> Microsoft neither endorses nor provides support for this third\-party product. Please contact the specific provider for support issues.

When you have a new management pack, you should import it to a *pre\-production* environment. In Operations Manager, it is a best practice to have a production implementation that is used for monitoring your production applications and a pre\-production implementation that has minimal interaction with the production environment. The pre\-production management group is used for testing and tuning management pack functionality before the management pack is deployed in the production environment.

To accurately measure the data that a management pack gathers, you need to expose the agent to the demands of your production environment. The hardware of the management server in the pre\-production environment should reflect the hardware that is in use in your production environment. Your pre\-production management group should have the same management packs imported to the management server as the production management group. To test interoperability, your pre\-production environment should also include the same types of server roles that are in your production environment, just on a smaller scale.

You can assign an Operations Manager agent to more than one management group, which is called *multihoming*. If you multihome a representative subset of agents in your production environment and your pre\-production environment, the pre\-production environment should give you much of the information you need to correctly tune the management pack. For more information on multihoming agents, see [Configuring Agents](./Configuring-Agents.md).

## <a name="bkmk_tuneandcustomize"></a>Tune and Customize
You can use overrides to refine the settings of a monitoring object in Operations Manager, including monitors, rules, object discoveries, and attributes. You should create a management pack in which to save customizations that you make.

For more information about using overrides, see [Tuning Monitoring by Using Targeting and Overrides](./Tuning-Monitoring-by-Using-Targeting-and-Overrides.md). For more information about creating management packs in which to save customizations, see [Best Practices for Change Control](./Management-Pack-Life-Cycle.md#bkmk_bestpracticesforchangecontrol).

## <a name="bkmk_deploy"></a>Deploy
When you are satisfied with the performance and results of the management pack in the pre\-production environment, you can deploy the management pack and its customizations in the production environment. The management pack in which you saved the customizations must be exported so that you can import it to other computers. For more information, see [How to Export an Operations Manager Management Pack](./How-to-Export-an-Operations-Manager-Management-Pack.md). The management pack that contains the overrides that you set is dependent on the original management pack and can be imported only to management groups that have the original management pack installed.

## <a name="bkmk_maintain"></a>Maintain
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

## <a name="bkmk_bestpracticesforchangecontrol"></a>Best Practices for Change Control
The following are some best practices to follow when managing Operations Manager management packs:

-   Maintain an archive of management pack versions to enable you to roll back changes when necessary. An efficient method for maintaining the archive is by using version control software, such as Microsoft Team Foundation Server or Windows SharePoint Services. Another method is to use a file share on the network with individual folders for each management pack version.

-   When you set overrides for a management pack, save them to a management pack that is named *ManagementPack*\_Override, where *ManagementPack* is the name of the sealed management pack to which the overrides apply. For example, overrides to the management pack Microsoft.InformationWorker.Office.XP.mp would be saved to Microsoft.InformationWorker.Office.XP\_Overrides.xml. For more information, see [Creating a Management Pack for Overrides](./Creating-a-Management-Pack-for-Overrides.md).

-   When a management pack is updated, update the corresponding \_Overrides.xml file with the new version number. You must use an XML editor to update the version number of the \_Overrides.xml file. If you make changes to an \_Overrides.xml file but do not change the version attribute, you can import the file but the settings in the file will not be applied.

-   Document the overrides that you make to management packs. When you set an override, add an explanation of the action you are taking and the reason for it to the description field by clicking **Edit** in the Details pane of the Override Properties dialog box. You may also want to maintain a spreadsheet or other form to document changes that you make to management packs.

## See Also
[Creating a Management Pack for Overrides](./Creating-a-Management-Pack-for-Overrides.md)
[Management Packs Installed with Operations Manager](./Management-Packs-Installed-with-Operations-Manager.md)
[What Is in an Operations Manager Management Pack?](./What-Is-in-an-Operations-Manager-Management-Pack-.md)
[How to Import an Operations Manager Management Pack](./How-to-Import-an-Operations-Manager-Management-Pack.md)
[How to Remove an Operations Manager Management Pack](./How-to-Remove-an-Operations-Manager-Management-Pack.md)
[How to Export an Operations Manager Management Pack](./How-to-Export-an-Operations-Manager-Management-Pack.md)
[How to Add Knowledge to a Management Pack](./How-to-Add-Knowledge-to-a-Management-Pack.md)


