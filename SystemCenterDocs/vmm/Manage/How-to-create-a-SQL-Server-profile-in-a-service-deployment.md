---
title: How to create a SQL Server profile in a service deployment
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75f2f67b-4b39-4005-adc1-bbc66cd5e926
---
# How to create a SQL Server profile in a service deployment
You can use the following procedure to create a SQL Server profile in [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)]. The SQL Server profile provides instructions for installing an instance of Microsoft SQL Server on a virtual machine.

> [!IMPORTANT]
> You can only use a SQL Server profile when you want to deploy a virtual machine as part of a service. In addition, you must use a virtual hard disk that contains a prepared instance of SQL Server \(generalized by using the Sysprep tool\). With [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](../../includes/sc_threshold_1_md.md)], you can choose from the following versions of SQL Server:
> 
> -   SQL Server 2012
> -   SQL Server 2014

### To create a SQL Server profile

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create**, and then click **SQL Server Profile**.

    The **New SQL Server Profile** dialog box opens.

3.  On the **General** tab, in the **Name** box, enter a name for the SQL Server profile. For example, enter **Corporate Finance SQL Server**.

4.  Click the **SQL Server Configuration** tab, and then, next to **Add**, click **SQL Server Deployment**.

    > [!NOTE]
    > A SQL Server deployment corresponds to the configuration of one instance of SQL Server. If you want to configure multiple instances of SQL Server on the same virtual machine, you must add and configure a SQL Server deployment for each instance.

5.  Under **SQL Server Deployment**, do the following:

    1.  Click **SQL Server Deployment, Deployment 1**. In the results pane, enter the required configuration information.

        Required information includes the name of this SQL Server deployment \(for which you can choose to enter a more meaningful name than "Deployment 1"\), the SQL Server instance name, and the SQL Server instance ID \(the instance ID specified during installation of SQL Server\). The installation Run As account is optional and uses the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] Service account unless you specify otherwise. For more information about Run As accounts, see [Configuring Run As accounts in VMM](Configuring-Run-As-accounts-in-VMM.md).

    2.  Click **Configuration**. In the results pane, enter the required configuration information.

        Required information includes the media source \(the path to the SQL Server installation media folder where Setup.exe is located\) and the SQL Server administrators.

    3.  Click **Service Accounts**. In the results pane, enter the Run As accounts to use.

    After you have made your selections, click **OK**.

6.  To verify that the profile was created, in the **Library** pane, expand **Profiles**, and then click **SQL Server Profiles**.

    The SQL Server profile appears in the **Profiles** pane.


