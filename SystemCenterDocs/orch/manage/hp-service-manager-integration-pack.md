---
title: HP Service Manager Integration Pack for System Center 2016 - Orchestrator
description: The integration pack for HP Service Manager is an add-on for Orchestrator in System Center 2016 and System Center 2016 - Orchestrator that enables you to retrieve, create, update and monitor tickets in HP Service Manager.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6eb5a088-0b37-456c-bd38-8af868e5ae82
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# HP Service Manager Integration Pack for System Center 2016 - Orchestrator

Applies To: System Center 2016 - Orchestrator

The integration pack for HP Service Manager is an add-on for Orchestrator in System Center 2016 and System Center 2016 - Orchestrator that enables you to retrieve, create, update and monitor tickets in HP Service Manager. Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more information, see the [System Center Orchestrator 2012 Privacy Statement](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

The integration pack for HP Service Manager requires the following software to be installed and configured to implementing the integration. For more information about installing and configuring Orchestrator and the HP Service Manager Web Service, refer to the respective product documentation.

-   System Center 2016 integration packs require Orchestrator in System Center 2016
-   HP Service Manager 7.11 or 9

The following software must be installed on each Runbook Server and Runbook Designer:

-   Microsoft .NET Framework 3.5 Service Pack 1
-   Microsoft SQL Server Native Client ODBC driver (Installed with SQL Server Management Tools)
-   For access to the HP Service Manager database on SQL Server:
    -   Microsoft SQL Server Native Client ODBC driver (Installed with SQL Server Management Tools)
-   For access to the HP Service Manager database on Oracle:
    -   Oracle Client (Net Configuration Assistant)
    -   Oracle ODBC driver

## Downloading the Integration Pack

To download this integration pack, see [HP Service Manager Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=54101).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Preparing to connect to the HP Service Manager Server

-   Make a record of the HP Service Manager server name and port number used to connect the HP Service Manager client.
-   For all HP Service Manager servers that you plan to connect to you must create an ODBC data source name (DSN) on each Client and Runbook server. Both SQL Server Native and Oracle ODBC connections are supported. See [Configuring the HP Service Manager Connections](#ConfiguringConnections).
-   The licensing model for the components of HP Service Manager varies depending on the version installed. Consult the HP product documentation to determine which components are licensed separately. This integration pack requires HP Service Manager SOAP web service access to operate correctly. Ensure that this component is installed and licensed, if necessary.
-   Ensure that the user configured to access the HP Service Manager server has been assigned the SOAP-API CAPABILITY WORD in the HP Service Manager system. Depending on the version of HP Service Manager, it may be necessary to purchase extra licensing to enable the SOAP-API CAPABILITY WORD. Consult your HP Sales Representative for further information about licensing.

## Configuring the HP Service Manager Connections

A connection establishes a reusable link between Orchestrator and a HP Service Manager server. You can create as many connections as you require specifying links to multiple servers running HP Service Manager. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

The HP Service Manager integration pack requires a connection to the HP Service Manager SQL Server Database when designing runbooks in the Runbook Designer. A valid ODBC connection must be configured before setting up the HP Service Manager connection in the Runbook Designer.

To avoid possible corruption, do not use alternate means to directly connect to the database. Always use the ODBC connection to ensure a proper integration.

#### To set up a SQL Server ODBC connection

1.  Open the **ODBC Data Source Administrator Utility (32-bit)**. To access this utility, click **Start**, **Run**, and then type **\\Windows\\SysWOW64\\odbcad32.exe** in the **Open** box. Click **OK**.

2.  In the **ODBC Data Source Administrator**, click the **System DSN** tab.

3.  Click **Add**.

4.  Select the driver named **SQL Server Native Client 10.0** from the list of available drivers.

5.  Click **Finish**.

6.  Enter a new name and description for the data source.

7.  Enter the HP Service Manager database server name or IP address in the **Server** box.

8.  Click **Next**.

9.  Select the appropriate authentication method for the database server and enter valid credentials.

10. Click **Next**.

11. Ensure the check box **Change the default database to:** is selected.

12. In the drop-down list below the check box select the HP Service Manager database.

13. Click **Next**.

14. Click **Finish**.

15. Click **Test Data Source** to confirm connectivity to the database.

16. When the test completes, click **OK**.

17. Click **OK**.

#### Setting up an Oracle ODBC Connection

1.  Configure an Oracle Net Service name using the Oracle Net Configuration Assistant. For more information on this step refer to the relevant Oracle product documentation.

2.  Open the ODBC Data Source Administrator Utility (32-bit). To access this utility, click **Start**, then **Run**, and then type **\\Windows\\SysWOW64\\odbcad32.exe** in the **Open** box. Click **OK**.

3.  In the ODBC Data Source Administrator, click the **System DSN** tab.

4.  Click **Add**.

5.  Select the Oracle ODBC driver installed with the Oracle client from the list of available drivers.

6.  Click **Finish**.

7.  Enter a new name and description for the data source.

8.  Enter the TNS Service Name for the HP Service Manager database as configured in the Net Configuration Assistant.

9.  Test the connection, supplying credentials if necessary.

10. Select the appropriate authentication method for the database server and enter valid credentials.

11. Click **OK**.

12. Click **OK** to close the ODBC Data Source Administrator.

#### To set up a HP Service Manager connection

1.  In the Runbook Designer, click the **Options** menu, and select **HP Service Manager**. The HP Service Manager dialog box appears.

2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Connection Configuration** dialog box will appear.

3.  In the **Name** box, enter a name for the connection. This could be the name of the HP Service Manager server or a descriptive name to distinguish the type of connection.

4.  In the **Server Address** box, type the name or IP address of the HP Service Manager computer. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).

5.  In the **Polling Interval** box, enter the how often, in minutes, you want to check the state of the HP Service Manager connection.

6.  In the **ODBC DSN** box, type the name of the ODBC data source from one of the previous procedures.

7.  Enter the database user name in the **DB Username** box.

8.  Enter the database password in the **DB Password** box.

9.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the HP Service Manager server.

10. Click **Test Connection**. When the message "Connected Successfully" appears, click **OK**.

11. In the connection list dialog, select the newly created connection by clicking the appropriate item in the list.

12. Click the **Refresh Field Cache** button to retrieve and store the custom configuration from the HP Service Manager server. This operation may take a few minutes to complete and is essential to allow the integration pack to connect correctly to a new HP Service Manager server.

13. Add additional connections to other HP Service Manager servers, if applicable.

14. Click **OK** to close the configuration dialog box, and then click **Finish**.

<br><br><strong>Tip </strong><br>For the DB Username and DB Password - If your HPSM database is on a computer running Windows server and you set up your ODBC DSN with Windows authentication, then you can enter anything in for the username and password because the fields are required only not to be blank in order for the Test Connection button to work. <br> If you are using SQL Server authentication, then you must have the username and password for the HPSM SQL Server database. The user must have read/write access to the database via the DSN connection.<br><br>

## Exposing Required Fields

If an activity reports an error and indicates that a required field must be specified but the IP does not provide the field in the user interface, the field must be exposed through the HP Service Manager Web service API. To expose the field complete the following procedure:

#### To expose a required field

1.  Open the HP Service Manager client.

2.  Connect to the desired HP Service Manager server.

3.  In the System Navigator, navigate to **Tailoring Tools**, then **Web Services**, then **WSDL Configuration** and double click the **WSDL Configuration** option.

4.  In the **External Access Definition** dialog click the **Search** button to list all available objects.

5.  Select the required object from the object list.

6.  Select the **Fields** tab.

7.  Scroll to the bottom of the **Field List**.

8.  Enter the database name of the field to be exposed in the **Field** column.

9.  Enter the name which the web service will refer to this field in the **Caption** column.

10. Ensure the data type is correct in the **Type** column.

11. Click **Save** at the top of the page to save the message.

## Known Issues
----

-   The **Test Connection** button cannot be used to validate Service Manager 7.1 web service connections if the HP ServiceCenter 6.2 web service has been disabled.
-   Certain permissions are required when dealing with Change tickets. These permissions are specified by assigning a user a Change Management Profile. While a user can have more than one profile, it can only belong to one profile per session. If the user is assigned more than one Change Management Profile it will automatically use the first profile in alphabetical order. To avoid confusion it is recommended that the user configured for use with the integration pack is only assigned one Change Management Profile.
-   The user configured for use with the integration pack must have its time zone preferences set to Greenwich/Universal with a date format of mm/dd/yy.
-   In certain versions of HP Service Manager the list of available categories when creating an incident displays Change yet choosing it causes the object to fail with the following message. Please provide a valid category. This is a known issue with the HP Service Manager server. Ensure that the fields are visible to the web service (See Troubleshooting) and that the HP Service Manager server is patched to the latest version.
-   The **Set as default** button available in the **Create Entry**, **Update Entry** and **Close Entry** activities may report an error when clicked. Use the following procedure to work around this issue.
    1.  Note the file path in the error message. For example, C:\\Users\\\[CurrentUser\]\\AppData\\Local\\Microsoft\\System Center 2012\\Orchestrator\\IntegrationPacks\\HPServiceManager\\\[GUID\]\\defaultFields.xml
    2.  Ensure that each of the folders in the file path exists exactly as shown in the error message.
    3.  Create any missing folders if necessary.

    if the Runbook Designer is launched by a user without administrative privileges on the computer. In the current version of the integration pack, ensure that the user has sufficient permissions to write to the **%COMMONPROGRAMFILES(x86)%\\Microsoft System Center 2012\\Orchestrator\\Extensions\\Support\\HPServiceManager\\** directory.
