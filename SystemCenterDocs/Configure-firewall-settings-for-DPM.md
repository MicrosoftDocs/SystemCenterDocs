---
title: Configure firewall settings for DPM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ae3f67e-982c-46a7-b1c3-5a94590ae9ea
---
# Configure firewall settings for DPM
DPM uses the following ports and protocols.

|Protocol|Port|Details|
|------------|--------|-----------|
|DCOM|135\/TCP Dynamic|DCOM is used by the DPM server and the DPM protection agent to issue commands and responses. DPM issues commands to the protection agent by invoking DCOM calls on the agent. The protection agent responds by invoking DCOM calls on the DPM server.<br /><br />TCP port 135 is the DCE endpoint resolution point used by DCOM.By default, DCOM assigns ports dynamically from the TCP port range of 1024 through 65535. However, you can configure this range by using Component Services.|
|TCP|5718\/TCP<br /><br />5719\/TCP|The DPM data channel is based on TCP. Both DPM and the protected computer initiate connections to enable DPM operations such as synchronization and recovery. DPM communicates with the agent coordinator on port 5718 and with the protection agent on port 5719.|
|TCP|6075\/TCP|Enabled when you create a protection group to protect client computers. Required for End user recovery.<br /><br />An exception in the Windows Firewall \(DPMAM\_WCF\_Service\) will created for the program Amscvhost.exe\) when you enable Central Console for DPM in Operations Manager.|
|DNS|53\/UDP|Used between DPM and the domain controller, and between the protected computer and the domain controller, for host name resolution.|
|Kerberos|88\/UDP<br /><br />88\/TCP|Used between DPM and the domain controller, and between the protected computer and the domain controller, for authentication of the connection endpoint.|
|LDAP|389\/TCP<br /><br />389\/UDP|Used between DPM and the domain controller for queries.|
|NetBios|137\/UDP<br /><br />138\/UDP<br /><br />139\/TCP<br /><br />445\/TCP|Used between DPM and the protected computer, between DPM and the domain controller, and between the protected computer and the domain controller, for miscellaneous operations. Used for SMB directly hosted on TCP\/IP for DPM functions.|

## <a name="BKMK_WF"></a>Windows Firewall settings
If Windows Firewall enabled when you install DPM then DPM Setup configured Windows Firewall settings as required with the rules and exception summarized in the following table. Note that:

-   If you’re looking for information on setting up firewall exceptions for computers protected by DPM see [Configure firewall exceptions for the agent](assetId:///f53287d3-bcb5-42cf-bb05-6f8cfed0fec7).

-   If Windows Firewall wasn’t available when you install DPM set it up manually using [Configure Windows Firewall manually](#BKMK_Manual).

-   If you’re running the DPM database on a remote SQL Server you’ll need to set up a few firewall exceptions. See [Set up Windows Firewall on the remote SQL Server](#BKMK_SQL).

|Rule name|Details|Protocol|Port|
|-------------|-----------|------------|--------|
|Microsoft System Center 2012 R2 Data Protection Manager DCOM Setting|Required for DCOM communications between the DPM server and protected computers|DCOM|135\/TCP Dynamic|
|Microsoft System Center 2012 R2 Data Protection Manager|Exception for Msdpm.exe \(the DPM service\). Runs on the DPM server.|All protocols|All ports|
|Microsoft System Center 2012 R2 Data Protection Manager Replication Agent|Esception for Dpmra.exe \(protection agent service used to back up and restore data. Runs on the DPM server and protected computers.|All protocols|All ports|

### <a name="BKMK_Manual"></a>Configure Windows Firewall manually

1.  In Server Manager, select **Local Server** > **Tools** > **Windows Firewall with Advanced Security**.

2.  In the Windows Firewall with Advanced Security console verify that Windows Firewall is on for all profiles, and then click **Inbound Rules**.

3.  To create an exception, in the **Actions** pane, click **New Rule** to open the New Inbound Rule Wizard.

    On the **Rule Type** page, verify that **Program** is selected, and then click **Next**.

4.  Configure exceptions to match the default rules that would have been created by DPM Setup if the Windows Firewall was enabled when DPM was installed.

    1.  To manually create the exception that matches the default Microsoft System Center 2012 R2 Data Protection Manager rule on the **Program** page, click **Browse** for the **This program path** box, navigate to **<system drive letter>:\\Program Files\\Microsoft DPM\\DPM\\bin** > **Msdpm.exe** > **Open**> **Next**..

        On the Action page leave the default setting of **Allow the connection**, or modify the settings according to your organization’s guidelines > **Next**.

        On the **Profile** page, leave the default settings of **Domain**, **Private**, and **Public**, or modify the settings according to your organization’s guidelines > **Next**.

        On the **Name** page, type a name for the rule and optionally a description > **Finish**.

    2.  Now use the same steps to manually create the exception that matches the default Microsoft System Center 2012 R2 Data Protection Replication Agent rule by browsing to **<system drive letter>:\\Program Files\\Microsoft DPM\\DPM\\bin**, and selecting **Dpmra.exe**.

    Note that if you’re running System Center 2012 R2 with SP1 the default rules will be named with **Microsoft System Center 2012 Service Pack 1 Data Protection Manager**.

## <a name="BKMK_SQL"></a>Set up Windows Firewall on the remote SQL Server
If you use a remote SQL Server for your DPM database, as part of the process you’ll need to configure the Windows Firewall on that remote SQL Server.

-   After SQL Server installation is complete the TCP\/IP protocol should be enabled for the DPM instance of SQL Server with the following settings: default failure audit, and enable password policy checking.

-   Configure an incoming exception for sqservr.exe for the DPM instance of SQL Server, to allow TCP on port 80. The report server listens for HTTP requests on port 80 for HTTP requests.

-   The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don’t listen on the default 1433 port, you’ll need UDP port 1434.

-   A named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

-   You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management – SQL Server Logs in the entry Server is listening on \[‘any’ <ipv4> port\_number\].

-   You’ll need to enable RPC on the remote SQL Server.


