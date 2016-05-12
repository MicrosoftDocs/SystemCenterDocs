---
title: Connecting Management Groups in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13890833-d295-4387-abc9-94bc520b5f00
---
# Connecting Management Groups in Operations Manager
Connecting management groups in [!INCLUDE[om12long](Token/om12long_md.md)] enables the ability to view and interact with data from multiple management groups in a single Operations console. The management group in which the consolidated view is available is called the local management group, and those that contribute their data to the consolidated view are called the connected management groups. They relate to each other in a hierarchical fashion, with connected groups in the bottom tier and the local group in the top tier. The connected groups are in a peer\-to\-peer relationship with each other. Each connected group has no visibility or interaction with the other connected groups; the visibility is strictly from the local group into the connected group.

> [!NOTE]
> Operations Manager does not support communication of data between peer management groups. Only the local to connected hierarchy configuration is supported. Multiple tiers, where a management group would be both a local group and a connected group, are not supported.

When you connect management groups, you are not deploying any new servers; rather, you are allowing the local management group to have access to the alerts and discovery information that is in a connected management group. In this way, you can view and interact with all the alerts and other monitoring data from multiple management groups in a single Operations console. In addition, you can run tasks on the monitored computers of the connected management groups.

Connecting management groups offers these additional services:

-   Consolidated monitoring and alerting for greater than 6,000 agents

-   Consolidated monitoring across trust boundaries

> [!IMPORTANT]
> Both management groups must be running the same build of Operations Manager. For example, both management groups must be running System Center 2012 – Operations Manager.

In addition to all of the communications channels used in the multiple server, single management group configuration, connected management groups require communication between the management servers of the local group and the management servers of the connected group over TCP 5723 and 5724. For a complete list of ports used by Operations Manager, see [Operations Manager Supported Configurations](http://go.microsoft.com/fwlink/p/?LinkID=219650).

Connected management groups support all Operations Manager user roles and makes use of the Operations Manager Connector Framework to enable bidirectional communication between the connected groups and local groups.

In this procedure, you create a connection between two management groups. These management groups can be in the same domain, or they can be in trusted domains. You can connect to management groups that are in domains that are not trusted, but you cannot view data from those domains until you add an account from the domain of the local management groups to an Operations Manager role for the connected management group. To do this, a trust must be established between the domains.

### Before you start

1.  To connect management groups, you must provide the fully qualified domain name \(FQDN\) of the root management server \(RMS\) of the connected management group. The management server of the local management group must be able to resolve this FQDN. If the two management groups do not use the same Domain Name System \(DNS\) service, you must create a secondary DNS zone in the DNS service that the local management group uses. This secondary DNS zone transfers the DNS information from the primary DNS zone of the connected management group. The transferred information is essentially a copy of the DNS information that is available to the management server of the local management group.

2.  Add the System Center Data Access service and System Center Management Configuration service account of the connected management groups to the Operations Manager Administrator role for the connected management group, or add it to the domain\-based Operations Manager Administrator security group in the connected management group’s domain, which has already been added to the Operations Manager Administrator role.

3.  Collect the System Center Data Access service and System Center Management Configuration service account credentials from the connected management groups. These credentials are needed when you add the connected management group in the local management group.

4.  Identify users in the domain of the local management group that will need access to data from the connected management groups. They must be added to the appropriate Operations Manager roles in the connected management group.

### To connect management groups

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators user role.

2.  In the Operations console that is connected to the destination management group, click **Administration**.

3.  In the **Administration** workspace, right\-click **Connected Management Groups**, and then click **Add Management Group**.

4.  In the **Add Management Group** dialog box, do the following:

    1.  Type the **Management Group name** of the management group to be connected.

    2.  Type the fully qualified domain name \(FQDN\) of a **Management Server** in the desired management group to be connected.

    3.  Specify the account that will be used for the initial connection to the connected management group, either by leaving **Use SDK service account** selected or selecting **Other user account** and typing in the **User name**, **Password**, and **Domain**. The account must be a member of the Operations Manager Administrators role for the connected management group.

5.  Click **Add**.

### To grant access to Connected Management Groups

1.  Identify users in the local management group that need access to the connected management groups.

2.  Add those users as members to the appropriate user role in the connected management groups.

    > [!NOTE]
    > If local and connected management groups are not in the same domain and there is no trust relationship between the two domains, you will have to create accounts in the connected management group domain for the users in the local management group domain to use.

3.  In the Operations console for the local management group, in the **Administration** view, expand **Security**, and then click **User Roles**.

4.  In the right pane, right\-click the user role to which you want to grant connected management group access, and then click **Properties**.

5.  On the **Group Scope** tab, select the connected management groups to which you want to grant access to this user role, and then click **OK**. A user with both permission and access to at least one connected management group will see the **Show Connected Alerts** button in the toolbar of any **Alert** view in the **Monitoring** space.

6.  A **Log On** dialog box appears and prompts the user for credentials \(to log on to the connected management groups\). Enter the credentials, and then click **OK**. Alerts appear from all connected management groups for which you have access and permission. You can run tasks in the managed computers of connected management groups.

## See Also
[General Tasks in Operations Manager_1](General-Tasks-in-Operations-Manager_1.md)
[Managing Alerts](Managing-Alerts.md)
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)
[Creating and Managing Groups](Creating-and-Managing-Groups.md)
[Running Tasks in Operations Manager](Running-Tasks-in-Operations-Manager.md)
[How to Create a Resource Pool](How-to-Create-a-Resource-Pool.md)
[Managing Resource Pools for UNIX and Linux Computers](Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)
[Using Operations Manager Shell](Using-Operations-Manager-Shell.md)


