---
title: How to create an application profile in a service deployment
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ce1f959-fb44-4f37-9f68-640f15505185
---
# How to create an application profile in a service deployment
You can use the following procedure to create an application profile in Virtual Machine Manager \(VMM\). An application profile provides instructions for installing Microsoft Web Deploy applications or Microsoft SQL Server data\-tier applications \(DACs\), and instructions for running scripts, when a virtual machine is deployed as part of a service. Application profiles are not supported for Linux operating systems because application profiles are designed for technologies that are specific to Windows operating systems.

> [!IMPORTANT]
> You can only use an application profile when you deploy a virtual machine as part of a service.

### To create an application profile

1.  Confirm that your application components, such as packages, scripts, and so on, have been copied to the VMM library share. For example, if you plan to create a profile for a SQL Server application host, confirm that your SQL Server DAC packages and SQL Server scripts have been copied to the VMM library share.

2.  Open the **Library** workspace.

3.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Application Profile**.

    The **New Application Profile** dialog box opens.

4.  On the **General** tab, in the **Name** box, enter a name for the application profile. For example, enter **Corporate Finance Application**.

5.  On the **General** tab, in the **Compatibility** list, choose an appropriate option:

    -   For deployment of any application type or combination of application types that are listed at the beginning of this topic, keep the default selection, **General**.

    -   For deployment of SQL Server DAC packages or SQL Server scripts to an existing instance of SQL Server in your environment, click **SQL Server Application Host**. If you click **SQL Server Application Host**, you can add only SQL Server DAC packages and SQL Server scripts to the application profile.

    -   For deployment of web applications to a server that runs Internet Information Services \(IIS\), click **Web Application Host**. If you click **Web Application Host**, you can add only Web Deploy packages and associated scripts to the application profile.

6.  Click the **Application Configuration** tab, and then do the following:

    1.  Click **OS Compatibility**, and then select the guest operating systems on which the application is supported.

    2.  Click **Add**, and then click the type of application or script that you want to add to the application profile.

        -   You can add more than one of each type of application. For example, you can add three web applications.

        -   If you kept the **Compatibility** option \(described in the previous step\) set to the default option, **General**, you can add more than one type of application or script to the application profile. For example, you can add a web application and a data\-tier application. Also, you can add an application that will be deployed by running a script, such as a script based on a Setup.exe installation program. To add such an application, select **Script Application**.

        -   After you add an application, you can select **Application script** to add application scripts. You can add one application script that will run before the application is installed or uninstalled, and one application script that will run after the application is installed or uninstalled.

        -   Regardless of whether you add an application, if you kept the **Compatibility** option set to **General**, you can select **Scripts** to add a script. The number of scripts is not limited, and you can specify the order in which the scripts will run.

            You can use scripts to create a guest cluster out of multiple virtual machines that are all deployed as part of a VMM service. For example, you can specify that one script will run at **Creation: First VM** \(to form the cluster on the first virtual machine\) and a different script will run at **Creation: VMs After First** \(to add additional virtual machines to the cluster\). For more information, see [How to create a guest cluster by using a service template in VMM](How-to-create-a-guest-cluster-by-using-a-service-template-in-VMM.md).

    3.  For each application or script that you add, configure the appropriate settings. Some of the settings that you can configure are as follows:

        -   For application packages, you can specify settings such as certificate, port, or folder settings for the application. To specify a setting, under **Applications**, select the application, select the setting, and then click **Properties**. Type the value, and then click **OK**.

            > [!NOTE]
            > An application package can contain settings to be entered when you configure the service for deployment. To format this type of setting, enter the parameter in the **Value** field, in this format: @<SettingLabel>@. For example, you might prompt for the instance name of a SQL Server for a SQL Server database tier application by using the parameter @SQLServerInstanceName@.

        -   For scripts, you can configure a variety of settings, such as parameters, the security account under which the script should run, time\-out, failure, and restart policies that specify what to do if there is an error, and other settings. To configure these settings, under **Scripts**, select the script and review or change the parameters, deployment order, time\-out, or other settings. As needed, click **Advanced** and view or configure advanced settings such as failure and restart policies.

    After you have made your selections, click **OK**.

7.  To verify that the profile was created, in the **Library** pane, expand **Profiles**, and then click **Application Profiles**.

    The application profile appears in the **Profiles** pane.



