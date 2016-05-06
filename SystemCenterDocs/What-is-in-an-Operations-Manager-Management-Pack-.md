---
title: What Is in an Operations Manager Management Pack?
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85abccbf-62b5-4f57-b04d-4f03d52b5fae
---
# What Is in an Operations Manager Management Pack?
Management packs typically contain monitoring settings for applications and services. After a management pack is imported into a management group, [!INCLUDE[om12long](./Token/om12long_md.md)] immediately begins monitoring objects based on default configurations and thresholds that are set by the management pack.

Each management pack can contain any or all of the following parts:

-   Monitors, which direct an agent to track the state of various parts of a managed component.

-   Rules, which direct an agent to collect performance and discovery data, send alerts and events, and more.

-   Tasks, which define activities that can be executed by either the agent or the console.

-   Knowledge, which provides textual advice to help operators diagnose and fix problems.

-   Views, which offer customized user interfaces for monitoring and managing this component.

-   Reports, which define specialized ways to report on information about this managed component.

-   Object discoveries, which identify objects to be monitored.

-   Run As profiles, which allow you to run different rules, tasks, monitors, or discoveries under different accounts on different computers.

## Parts of a Management Pack
Every management pack defines a model of the component that it manages. This model is expressed as one or more classes, each representing something that can be monitored and managed. When a management pack’s information is sent to an agent, the agent relies on specific discovery rules in the management pack to find the actual instances of the classes this pack defines.

To reduce network utilization and storage requirements on the agent, only the parts of the management pack that are required by the agent to perform monitoring are downloaded to the agent for local storage.  For example, the sections of the management packs which define rules and monitors are downloaded, while the sections for knowledge and reports are not.

### Monitors
Each management pack defines one or more classes that can be managed, and then specifies a group of monitors for instances of the classes. These monitors keep track of the state of each class instance, making it easier to avoid problems before they occur.

Each monitor reflects the state of some aspect of a class instance, and changes as the state of the class instance changes. For example, a monitor that tracks disk utilization might be in one of three states: green, if the disk is less than 75 percent full; yellow, if it is between 75 and 90 percent full; and red, if the disk is more than 90 percent full. A monitor that tracks the availability of an application might have only two states: green, if the application is running; and red, if it is not. The author of each management pack defines the monitors it contains, how many states each monitor has, and what aspect of the managed class this monitor tracks.

### Rules
In Operations Manager, a rule defines the events and performance data to collect from computers, and what to do with the information after it is collected. A simple way to think about rules is as an if\/then statement. For example, a management pack for an application might contain rules such as the following:

-   If a message indicating that the application is shutting down appears in the event log, send an alert.

-   If a logon attempt fails, collect the event that indicates this failure.

As these examples show, rules can send alerts, events, or performance data. Rules can also run scripts, such as allowing a rule to attempt to restart a failed application.

### Views
The Operations Manager Operations console provides standard views such as State, Alerts, and Performance. A management pack might include specialized views, unique to that management pack. In addition, you can create a personalized view in the Operations console.

### Knowledge
Knowledge is content, embedded in rules and monitors, that contains information from the management pack author about the causes of an alert and suggestions on how to fix the issue that caused an alert to be raised. Knowledge appears as text in the console, and its goal is to help an operator diagnose and fix problems. The text can include links to tasks, allowing the author of this knowledge to walk an operator through the recovery process. For example, the operator might first be instructed to run task A, and then based on the result of this task, run either task B or task C. Knowledge can also contain links to performance views and to reports, giving the operator direct access to information needed to solve a problem.

Knowledge is referred to as *product knowledge* or *company knowledge*. Product knowledge is added to the management pack by the management pack author. Administrators can add their own knowledge to rules and monitors to expand the troubleshooting information and provide company\-specific information for operators, which is known as company knowledge. For more information on adding company knowledge to a management pack, see [How to Add Knowledge to a Management Pack](./How-to-Add-Knowledge-to-a-Management-Pack.md).

### Tasks
A task is a script or other executable code that runs either on the management server or on the server, client, or other device that is being managed. Tasks can potentially perform any kind of activity, including restarting a failed application and deleting files. Like other aspects of a management pack, each task is associated with a particular managed class. For example, running chkdsk makes sense only on a disk drive while a task that restarts Microsoft Exchange Server is meaningful only on a computer that is running Exchange Server. If necessary, an operator can also run the same task simultaneously on multiple managed systems. Monitors can have two special kinds of tasks associated with them: diagnostic tasks that try to discover the cause of a problem, and recovery tasks that try to fix the problem. These tasks can be run automatically when the monitor enters an error state, providing an automated way to solve problems. They can also be run manually, because automated recovery isn’t always the preferred approach.

### Reports
Just as a management pack can contain views customized for the objects that management pack targets, it can also contain custom reports. For example, a management pack might include a customized definition of one of Operations Manager’s built\-in reports, specifying the exact objects that the report should target.

### Object Discoveries
Object discoveries are used to find the specific objects on a network that need to be monitored. Management packs define the type of objects that the management pack monitors. The object discoveries can use the registry, WMI, scripts, OLE DB, LDAP, or even custom managed code to find objects on a network. If an object discovery finds objects on your network that you do not want to monitor, you can limit the scope of object discoveries by using overrides.

### Run As Profiles
A management pack can include one or more Run As profiles. Run As profiles and Run As accounts are used to select users with the privileges needed for running rules, tasks, and monitors.

Management pack authors can create a Run As profile and associate the profile with one or more rules, monitors, tasks, or discoveries. The named Run As profile is imported along with the management pack into Operations Manager . The Operations Manager administrator then creates a named Run As account and specifies users and groups. The administrator adds the Run As account to the Run As profile and specifies the target computers that the account should run on. The Run As account provides the credentials for running the rules, monitors, tasks, and discoveries that are associated with the Run As profile to which the Run As account belongs.

## <a name="bkmk_sealedandunsealedmanagementpacks"></a>Sealed and Unsealed Management Packs
Management packs are either sealed or unsealed. A sealed management pack is a binary file that cannot be edited. An unsealed management pack is an XML file that can be edited. Sealed management packs should have an .mp extension, while unsealed management packs should have an .xml extension.

In general, management packs obtained from an application or hardware device vendor are sealed.

Although you cannot change the settings in a sealed management pack, you can still customize the applied settings of a management pack after it is imported by using overrides or by creating additional settings such as rules, monitors, and tasks that supersede the management pack's default settings. All customizations that you create are saved to a separate management pack file.

## Management Pack Libraries and Dependencies
Certain management packs are referred to as *libraries*, because they provide a foundation of classes on which other management packs depend. A management pack that you download from the Operations Manager Catalog might include a library management pack. Several library management packs are imported as part of the Operations Manager installation process. For a list of management packs imported during the installation of [!INCLUDE[om12short](./Token/om12short_md.md)], see [Management Packs Installed with Operations Manager](./Management-Packs-Installed-with-Operations-Manager.md).

A dependency exists when a management pack references other management packs. You must import all referenced management packs before you can import the management pack that depends on those management packs. Management packs include a management pack guide that should document the dependencies of the management pack. In addition, if you attempt to import a management pack and the management packs that it is dependent on are not present, the **Import Management Packs** dialog box will display a message that the management pack will fail to import and a list of the missing management packs. After you import a management pack, you can view its dependencies in the Operations console.

#### To view the dependencies for a management pack

1.  In the Operations console, in the **Administration** workspace, click **Management Packs**.

2.  Right\-click the desired management pack, and then click **Properties**.

3.  In the **Properties** dialog box for the management pack, click the **Dependencies** tab.

    The **Dependencies** tab lists any management packs that the selected management pack depends on and any management packs that depend on the selected management pack.

## See Also
[Creating a Management Pack for Overrides](./Creating-a-Management-Pack-for-Overrides.md)
[Management Packs Installed with Operations Manager](./Management-Packs-Installed-with-Operations-Manager.md)
[Management Pack Life Cycle](./Management-Pack-Life-Cycle.md)
[How to Import an Operations Manager Management Pack](./How-to-Import-an-Operations-Manager-Management-Pack.md)
[How to Remove an Operations Manager Management Pack](./How-to-Remove-an-Operations-Manager-Management-Pack.md)
[How to Export an Operations Manager Management Pack](./How-to-Export-an-Operations-Manager-Management-Pack.md)
[How to Add Knowledge to a Management Pack](./How-to-Add-Knowledge-to-a-Management-Pack.md)


