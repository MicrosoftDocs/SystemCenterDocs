---
ms.assetid: 3b2683c5-6f10-437e-87cb-cb389356ea00
title: OLE DB data source template in Operations Manager management pack
description: This article provides an overview about OLE DB data source template
author: v-anesh
ms.author: v-anesh
manager: vvithal
ms.date: 10/14/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# OLE DB data source template

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

_OLE DB_ (Object Linking and Embedding Database) is a Microsoft technology for accessing a variety of data sources by using a common method to connect to different databases such as Microsoft SQL Server.

The  **OLE DB Data Source**  template lets you monitor the availability and performance of any database that can be accessed with OLE DB. One or more watcher nodes connect to the database to verify its availability and test its performance. The watcher nodes can test the connection to the database or measure the time taken to perform a particular query.

The database can reside on any computer whether it has an agent for Operations Manager installed or not, but it must be accessible from the watcher nodes. Each watcher node must have an Operations Manager agent installed.

## Scenarios

Use the  **OLE DB Data Source**  template in scenarios where applications rely on a database. You can either define a single watcher node to ensure that the database is accessible and responds to requests, or you can define each application server as a watcher node. The monitors that the template creates attempt to connect to the database from each location at the defined interval, and verify that each watcher node can connect successfully. In addition to validating the health of the database itself, any network connections and other required features between the watcher node and the database are also validated. You can use any number of watcher nodes, but it is typically most useful to select a sample that represents different environment or network segments.

## Monitoring performed by OLE DB data source template

Depending on your selections in the OLE DB Data Source Template wizard, the monitoring performed by the created monitors and rules can include any of the following settings.

| Type | Description | Enabled? |
| --- | --- | --- |
| Monitors | Success of the database connection or query | Enabled by default. |
|| Time to connect to database | Enabled if specified in wizard. |
|| Time to complete query | Enabled if specified in the wizard and the query is provided. |
|| Time to fetch results of query | Enabled if specified in the wizard and the query is provided. |
| Collection Rules | Collection of time to connect to the database | Enabled by default. |
|| Collection of time to complete the query | Always enabled if the query is provided. |
|| Collection of time to fetch results of query | Always enabled if the query is provided. |

## Viewing monitoring data

All data collected by the  **OLE DB Data Source**  template is available in the  **OLE DB Data Source State**  view located in the  **Synthetic Transaction**  folder. In this view, an object represents each of the watcher nodes. The state of each object represents the worst state of the set of database monitors that are running on that node. If one or more of the nodes is shown with an error while at least one other node is healthy, it could indicate a problem with that particular node accessing the database, a network issue. If all of the nodes are unhealthy, it could indicate a problem with the database itself.

You can view the state of the individual database monitors by opening the Operations Manager Health Explorer for each object. You can view performance data by opening the Performance view for each of these objects.

## Wizard options

When you run the  **OLE DB Data Source**  template, you have to provide values for options in the following tables. Each table represents a single page in the wizard.

## General properties

The following options are available on the  **General Options**  page of the wizard.

| Option | Description |
| --- | --- |
| Name | The name used for the monitoring wizard. This name is displayed in the Operations console in the  **OLE DB Data Source State**  view. |
| Description | Optional description of the monitor. |
| Management Pack | Management pack to store the classes, monitors, and rules that the template created. For more information about management packs, see [Selecting a Management Pack File](select-management-pack-file.md). |

## Connection String

The following options are available on the  **Connection String**  page of the wizard.

| Option | Description |
| --- | --- |
| Connection string | The connection string to connect to the database. A connection string contains the properties required to locate and connect to the database. It contains such information as the server that is hosting the database, the database name, and the type of authentication to perform. You can type a connection string or build a connection string in a dialog box by clicking  **Build**.For more detailed information about connection strings, see [Connection String Syntax](/previous-versions/windows/desktop/ms722656(v=vs.85)). |
| Query to execute | Optional query after the connection to the database has been made. If no query is provided, the monitor only attempts to connect to the database. |
| Query time-out | If a query is provided, this option specifies the maximum number of seconds that the query can take before it times out. You must set the  **Query Time-out**  value. |

## Query Performance

The following options are available on the  **Query Performance**  page of the wizard.

| Option | Description |
| --- | --- |
| Connection time in milliseconds | If selected, the values  **Error Threshold**  and  **Warning Threshold**  provide the number of milliseconds for the connection when the monitor enters that state and an alert is generated. If not selected, the connection time is not monitored. |
| Query time in milliseconds | If selected, the values  **Error Threshold**  and  **Warning Threshold**  define the number of milliseconds the query can run before the monitor enters that state and generates an alert. If not selected, the time to run the query is not monitored. If a query is not provided, this option is not available. |
| Fetch time in milliseconds | If selected, the values  **Error Threshold**  and  **Warning Threshold**  define the number of milliseconds to retrieve the results of the query before the monitor enters that state and generates an alert. If not selected, the time to retrieve the results of the query is not monitored. If a query is not provided, this option is not available. |

## Watcher Nodes

The following options are available on the  **Watcher Nodes**  page of the wizard.

| Option | Description |
| --- | --- |
| Select one or more agent-managed computers | Specify one or more agent-managed computers to run the monitor. For more information, see [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29). |
| Run this query every | The frequency to attempt the connection to the database and run the query, if specified. |

## Security considerations

The  **OLE DB Data Source**  template creates two Run As profiles. The name for each of these profiles starts with the name that you provided in the template and is followed by "Simple Authentication Profile" and "Synthetic Transaction Profile". If no Run As account is added to either of these profiles, the Default Action Account for each watcher node is used to connect the database and run the query. If the Default Action Account does not have access to the database that is being monitored, the connection fails. You can specify either integrated security or simple authentication by creating a Run As account and adding it to the appropriate Run As profile that the  **OLE DB Data Source** template created.

When you run the  **OLE DB Data Source**  template, it creates two Run As profiles. The name for each starts with the  **Name**  that you provided when you ran the template. The  **OLE DB Synthetic Transaction Profile**  is used when you want to use integrated security for the database connection. The  **OLE DB Simple Authentication Profile**  is used when you want to use simple authentication for the database connection.

## Integrated security

Integrated security lets you connect to the database by using credentials stored in Active Directory Domain Services. To connect the watcher nodes to the database by using integrated security, create a Run As account with  **Windows**  as the  **Account type**  and the credentials for the appropriate user account. Then add this Run As profile to the  **OLE DB Synthetic Transaction Profile**.

## Simple authentication

Simple authentication lets you connect to the database by using a simple name and password. For a SQL Server database, this simple authentication could be used for SQL Server authentication. To have the watcher nodes connect to the database by using simple authentication, create a Run As account with  **Simple Authentication**  as the  **Account type**  and the credentials for the appropriate user account. Then add this Run As profile to the  **OLE DB Simple Authentication Profile**. When you specify the connection string for the template, select the  **Use Simple Authentication RunAs Profile created for this OLE DB data source transaction**  check box. This adds variables to the connection string for the user name and password that you specified in the Run As account.

## Creating and modifying OLE DB data source templates

#### To run the OLE DB Data Source wizard

1. Start the Operations console with an account that has Author credentials in the management group.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, right-click  **Management Pack Templates** , and then select  **Add Monitoring Wizard**.
4. On the  **Select Monitoring Type**  page, select  **OLE DB Data Source** , and then click  **Next**.
5. On the  **General Properties**  page, in the  **Name**  and  **Description**  boxes, type a name and an optional description.
6. Select a management pack in which to save the monitor, or click  **New**  to create a new management pack. For more information, see [Selecting a Management Pack File](select-management-pack-file.md).
7. Click  **Next**.
8. In the  **Connection string**  box, type a connection string for the database, or click the  **Build**  button to be prompted for the required information.
9. If you want the monitor to run a query, select  **Query to execute** , and then type a query.
10. If you want to set a time-out for the query, type the number of seconds in the  **Query time-out**  box.
11. Click  **Test**  to perform a test connection by using the connection string and query that you just provided.

     > [!NOTE]
     > The test is performed on the workstation that you are using to run the template. If this workstation cannot access the database, this test fails. When the template is completed, the query is run from the watcher nodes that you specify.

12. Click  **Next**  when you have validated your connection string and query.
13. Select the measurements that you want to monitor and set an error and warning threshold for each. Click  **Next**.
14. Select one or more [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29) to run the monitor.
15. Specify the frequency to run the monitor in the  **Run this query**  box. Click  **Next**.
16. Review the summary of the monitor, and then click  **Create**.
17. If a Run As account with credentials that have access to the database does not exist, create an appropriate Run As account in the  **Administration**  workspace. For more information, see [How to Create a Run As Account](/previous-versions/system-center/system-center-2012-R2/hh321655%28v%3dsc.12%29).

     > [!NOTE]
     > To create and modify a Run As account, you must have administrative credentials for the management group.

18. If the database uses integrated security, add the Run As account to the  **Synthetic Transaction Action Profile**  for the template. If the database uses simple authentication, add the Run As account to the  **Simple Authentication Profile**  for the template.

     > [!NOTE]
     > To create and modify a Run As profile, you must have administrative credentials for the management group.

#### To modify an existing OLE DB Data Source template

1. Open the Operations console with a user account that has Author credentials.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, expand  **Management Pack Templates** , and then select  **OLE DB Data Source**.
4. In the  **OLE DB Data Source**  pane, locate the monitor to change.
5. Right-click the monitor, and then select  **Properties**.
6. Enter the changes that you want, and then click  **OK**.

## Viewing OLE DB data source monitors and collected data

#### To view all OLE DB Data Source monitors

1. Open the Operations console.
2. Open the  **Monitoring**  workspace.
3. In the  **Monitoring**  navigation pane, select  **Synthetic Transaction** , and then click  **OLE DB Data Source State**.

#### To view the state of each monitor

1. In the  **OLE DB Data Source State**  pane, right-click an object. Select  **Open** , and then click  **Health Explorer**.
2. Expand the  **Availability**  and  **Performance**  nodes to view the individual monitors.

#### To view the performance collected for a monitor

1. In the  **OLE DB Data Source State**  pane, right-click an object. Select  **Open** , and then click  **Performance**.
2. In the  **Legend**  pane, select the counters that you want to view.
3. Use options in the  **Actions**  pane to modify the Performance view.

## See also

- [Creating Management Pack Templates](create-management-pack-templates.md)
- [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29)