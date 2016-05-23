---
title: Install the Agent Using the Discovery Wizard
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46b4d047-51ef-441c-8e21-f9d3087228f6
---
# Install the Agent Using the Discovery Wizard
You can use the Operations console to search your environment for manageable objects and then deploy an agent to any object that you want to monitor. The process of searching your environment is called “discovery.” One of the advantages of using discovery is that it lists *all* manageable objects, including any that you might not be aware of.

The Discovery Wizard does not show computers that the management group is already monitoring. If you are doing a phased rollout of your management group, you can run the wizard to add new computers to the group. Also, after your initial deployment, you can use the Discovery Wizard to add newly installed computers to be managed.

When agents are pushed out to computers, [!INCLUDE[scom_threshold_1](../../Token/scom_threshold_1_md.md)] sends credentials that have local administrator rights for that computer; this is required to install the agent.

If the Discovery Wizard is not right for your needs \(for example, if you have a set list of computers to which you want to deploy agents\), you have the option of manually installing agents on systems to be managed. Agents can also be embedded in the host image of the monitored computer.

Use the following procedures to discover computers  and to deploy the Operations Manager agent to the discovered computers from the Operations console. For a list of the supported operating system versions, see [Supported Configurations](http://go.microsoft.com/fwlink/p/?LinkID=223642).

You can use the Discovery Wizard to install an agent to  Windows, UNIX or Linux systems. To install on a Windows system follow the steps describe in the section [To install an agent on a computer running Windows by using the Discovery Wizard](#WindowsProcedure) to install on a UNIX or Linux system follow the steps described in the section [To discover and install an agent on a UNIX or Linux Computer](#LinuxProcedure).

> [!NOTE]
> For information about port requirements for agents, see [Agent and Agentless Monitoring](http://go.microsoft.com/fwlink/p/?LinkId=230474) in the Deployment Guide.

## <a name="WindowsProcedure"></a>To install an agent on a computer running Windows by using the Discovery Wizard

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  At the bottom of the navigation pane, click **Discovery Wizard**.

    > [!NOTE]
    > The Discovery Wizard links in the Operations console open the Computer and Device Management Wizard.

4.  On the **Discovery Type** page, click **Windows computers**.

5.  On the **Auto or Advanced?** page, do the following:

    1.  Select either **Automatic computer discovery** or **Advanced discovery**. If you select **Automatic computer discovery**, click **Next**, and then go to step 7. If you select **Advanced discovery**, continue with the following steps.

        > [!NOTE]
        > Automatic computer discovery scans for Windows\-based computers in the domain. Advanced discovery allows you to specify criteria for the computers that the wizard will return, such as computer names starting with NY.

    2.  In the **Computer and Device Classes** list, select **Servers and Clients**, **Servers Only**, or **Clients Only**.

    3.  In the **Management Server** list, click the management server or gateway server to discover the computers.

    4.  If you selected **Servers and Clients**, you can select the **Verify discovered computers can be contacted** check box. This is likely to increase the success rate of agent deployment, but discovery can take longer.

        > [!NOTE]
        > If the Active Directory catalog does not contain the NetBIOS names for computers in a domain, select **Verify discovered computers can be contacted**. Otherwise, the **Browse, or Type In** option fails to find computers. This affects computers in the same domain as the management server, in another domain with a full trust relationship, and in untrusted domains by using a gateway server.

    5.  Click **Next**.

    > [!NOTE]
    > The wizard can return approximately 4000 computers if **Verify discovered computers can be contacted** is selected, and it can return 10,000 computers if this option is not selected. Automatic computer discovery verifies that discovered computers can be contacted. A computer that is already managed by the management group is not returned.

6.  On the **Discovery Method** page, you can locate the computers that you want to manage by either scanning or browsing Active Directory Domain Services or typing the computer names.

    If you want to scan, do the following:

    1.  If it is not already selected, select **Scan Active Directory** and then click **Configure**.

    2.  In the **Find Computers** dialog box, type the criteria that you want to use for discovering computers, and then click **OK**.

    3.  In the **Domain** list, click the domain of the computers that you want to discover.

    If you want to browse Active Directory Domain Services or type the computer names, do the following:

    -   Select **Browse for, or type\-in computer names**, click **Browse**, specify the names of the computers that you want to manage, and then click **OK**.

    -   In the **Browse for, or type\-in computer names** box, type the computer names, separated by a semi\-colon, comma, or a new line. You can use NetBIOS computer names or fully qualified domain names \(FQDN\).

7.  Click **Next**, and on the **Administrator Account** page, do one of the following:

    -   Select **Use selected Management Server Action Account** if it is not already selected.

    -   Select **Other user account**, type the **User name** and **Password**, and then select the **Domain** from the list. If the user name is not a domain account, select **This is a local computer account, not a domain account**.

        > [!IMPORTANT]
        > The account must have administrative privileges on the targeted computers. If **This is a local computer account, not a domain account** is selected, the management server action account will be used to perform discovery.

8.  Click **Discover** to display the **Discovery Progress** page. The time it takes discovery to finish depends on many factors, such as the criteria specified and the configuration of the IT environment. If a large number \(100 or more\) of computers are being discovered or agents are being installed, the Operations console will not be usable during discovery and agent installation.

    > [!NOTE]
    > Computers that are already managed by the management group will not be returned by the wizard.

9. On the **Select Objects to Manage** page, do the following:

    1.  Select the computers that you want to be agent\-managed computers.

    2.  In the **Management Mode** list, click **Agent** and then click **Next**.

    > [!NOTE]
    > The discovery results show virtual nodes of clusters. Do not select any virtual nodes to be managed.

10. On the **Summary** page, do the following:

    1.  Leave the **Agent installation directory** set to the default of **%ProgramFiles%\\System Center Operations Manager** or type an installation path.

        > [!IMPORTANT]
        > If a different **Agent installation directory** is specified, the root of the path must exist on the targeted computer or the agent installation fails. Subdirectories, such as **\\Agent**, are created if they do not exist.

    2.  Leave **Agent Action Account** set to the default, **Local System**, or select **Other** and type the **User name**, **Password**, and **Domain**. The Agent Action Account is the default account that the agent will use to perform actions.

    3.  Click **Finish**.

11. In the **Agent Management Task Status** dialog box, the **Status** for each selected computer changes from **Queued** to **Success**; the computers are ready to be managed.

    > [!NOTE]
    > If the task fails for a computer, click the targeted computer. The reason for the failure is displayed in the **Task Output** text box.

12. Click **Close**.

## <a name="LinuxProcedure"></a>To discover and install an agent on a UNIX or Linux Computer

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  At the bottom of the navigation pane, click **Discovery Wizard**.

4.  On the **Discovery Type** page, click **Unix\/Linux computers**.

5.  On the **Discovery Criteria** page, do the following:

    1.  Click **Add** to define a discovery scope. In the **Discovery Criteria** dialog box, do the following:

        1.  For the **Discovery scope**, click the ellipsis button **…** to specify the host name, IP address, or range of IP addresses of the UNIX\- or Linux\-based computers to be discovered.

        2.  For the **Discovery type** select **Discover all computers** or **Discover only computers with the UNIX\/Linux agent installed**.

            If you choose to discover only computers with the agent installed, the only credential that you will need to provide is for the agent verification. This can be a low\-privileged account on the UNIX or Linux computer.

            > [!IMPORTANT]
            > Discovering only computers with the agent installed requires that the agent is currently installed and configured with a signed certificate.

        3.  To specify the credentials for installing an agent, click **Set credentials**.

        4.  Click **Save**.

    2.  Select a management pool to monitor the UNIX or Linux computer.

        > [!NOTE]
        > The option will be changed from **management pool** to **resource pool** in the final release of Operations Manager.

6.  Click **Discover** to display the **Discovery Progress**  page. The time it takes to finish discovery depends on many factors, such as the criteria specified and the configuration of the environment. If a large number \(100 or more\) of computers are being discovered or agents are being installed, the Operations console will not be usable during discovery and agent installation.

7.  On the **Computer Selection** page, on the **Manageable computers** tab, select the computers that you want to be managed. The **Additional results** tab lists any errors and computers that are already being managed.

8.  Click **Manage**.

9. On the **Computer Management** page, after the deployment process is completed, click **Done**.

You must have, at a minimum, a UNIX\/Linux Action Account profile configured with a Monitoring Run As Account to monitor the UNIX or Linux computer. For more information, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](https://technet.microsoft.com/library/hh212926.aspx).

> [!NOTE]
> Solaris Zones are supported on Solaris 10 or newer versions. In monitoring a computer with Zones, each Zone is treated like a separate computer. You must install the agent on each computer that you want to monitor. Install the agent on the global zone first, because sparse zones share files with the global zone. If you try to install on a sparse zone first, the installation fails. For more information about troubleshooting, see [Operating System Issues](http://go.microsoft.com/fwlink/?LinkId=318149).


