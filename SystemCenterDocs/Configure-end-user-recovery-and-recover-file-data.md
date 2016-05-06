---
title: Configure end-user recovery and recover file data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4caa796b-27fe-41c2-b644-c4cc952896f0
---
# Configure end-user recovery and recover file data
End\-user recovery enables users to independently recover file data by retrieving recovery points of their files. Note the following:

-   Only short\-term, disk\-based recovery is available for end\-user recovery.

-   Enabling end\-user recovery modifies the Active Directory schema.

-   If you enable end\-user recovery you can’t specify on which file servers end\-user recovery is enabled.

-   You can’t control which Active Directory users or groups can perform end\-user recovery.

Configuring end\-user recovery requires the following:

1.  [Configure AD DS to support end\-user recovery](#BKMK_Config)—Performing this procedure does the following:

    -   Extends the AD DS schema

    -   Creates an AD DS container

    -   Grants permissions to the DPM server to change the container contents

    -   Adds mappings between the source shares and the replica shares

    For administrators who are both schema and domain administrators in AD DS this procedure can be completed with a couple of clicks in the DPM console. For non\-administrators the DPMADSchemaExtension tool runs to complete the configuration. This tool is located on the DPM server in the Microsoft DPM\\DPM\\End User Recovery folder. It will be run on each DPM server in your deployment. For more information about the tool, see D[Changes made to AD DS for end-user recovery](./Changes-made-to-AD-DS-for-end-user-recovery.md).

2.  [Enable or disable end\-user recovery on the DPM server](#BKMK_Enable)—This step is only required for client computers running computers running Windows XP with SP2 or later and Windows Server 2003 with or without SP1. Computers running later versions of operating systems can skip this step.

3.  [Install the shadow copy client software on client computers](#BKMK_Shadow)

## <a name="BKMK_Config"></a>Configure AD DS to support end\-user recovery
The following procedures show you how to configure Active Directory Domain Services and enable end\-user recovery of file data sources.

#### To configure AD DS \(if you’re a schema and domain administrators\)

1.  In DPM Administrator Console, click **Options** on the tool ribbon.

2.  In the **Options** dialog box, on the **End\-user Recovery** tab, click **Configure Active Directory**.

3.  In the **Configure Active Directory** dialog box, select **Use current credentials** or type the user name and password for an account that has both schema and domain administrator privileges, and then click **OK**.

4.  On the confirmation and notification prompts, click **Yes** and then click **OK**.

5.  After configuration of Active Directory Domain Services is complete, select the check box for the **Enable end\-user recovery** option and then click **OK**.

#### To configure AD DS \(if you’re not a schema and domain administrators\)

1.  Direct a user who is both a schema and domain administrator to configure the Active Directory schema by running **<drive:>\\Program Files\\Microsoft Data Protection Manager\\DPM\\End User Recovery\\DPMADSchemaExtension.exe** on a computer that is a member of the same domain as the DPM server.

    > [!NOTE]
    > If the protected computer and DPM reside in different domains, the schema needs to be extended by running the DPMADSchemaExtension.exe tool on the other domain.

2.  In the **Enter Data Protection Manager Computer Name** dialog box, type the name of the computer for which you want end\-user recovery data in Active Directory Domain Services, and then click **OK**.

3.  Type the DNS domain name of the DPM computer for which you want end\-user recovery data in Active Directory Domain Services, and then click **OK**.

4.  In the **Active Directory Configuration for Data Protection Manager** dialog box, click **OK**.

5.  In DPM Administrator Console, on the **Action** menu, click **Options**.

6.  In the **Options** dialog box, on the **End\-user Recovery** tab, select the check box for the **Enable end\-user recovery** option, and then click **OK**.

## <a name="BKMK_Enable"></a>Enable or disable end\-user recovery on the DPM server
In [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)], if you want to allow end users to recover their own data, you can use the following procedure to enable the end\-user recovery option.

#### To enable end\-user recovery

1.  In DPM Administrator Console, go to the **Recovery** view.

2.  Click **End\-user recovery**.

3.  On the **End\-user recovery** tab, select the **Enable end**\-**user recovery** check box.

4.  Click **OK**.

    This action takes effect after the next successful synchronization job is completed. If you want this action to take effect immediately, you can manually synchronize the replica.

#### To disable end\-user recovery

1.  In DPM Administrator Console, go to the **Recovery** view.

2.  Click **End\-user recovery**.

3.  On the **End\-user recovery** tab, clear the **Enable end**\-**user recovery** check box.

4.  Click **OK**.

    This action takes effect after the next successful synchronization job is completed. If you want this action to take effect immediately, you can manually synchronize the replica.

## <a name="BKMK_Shadow"></a>Install the shadow copy client software on client computers
Before users on operating systems running Windows XP with SP2 or later and Windows Server 2003 with or without SP1 can begin independently recovering previous versions of their files and applications, the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] shadow copy client software must be installed on their computers. If a client for Shadow Copies of Shared Folders is present on the computer, the client software must be updated to support [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)]. Note that this isn’t required for computers running later versions of operating systems.

#### To install Shadow Copy Client software

1.  Download the software as follows:

    1.  Windows XP SP2—[http:\/\/go.microsoft.com\/fwlink\/?LinkId\=46064](http://go.microsoft.com/fwlink/?LinkId=46064)

    2.  Windows Server 2003—[http:\/\/go.microsoft.com\/fwlink\/?LinkId\=184264](http://go.microsoft.com/fwlink/?LinkID=184264)

2.  Install the client software on users’ workstations by using your usual software distribution method—for example, Group Policy Software Installation, Microsoft Systems Management Server, Microsoft System Center Configuration Manager, or shared folders. If your users will install the client software on their own workstations, instruct them to copy the Setup program to any location on their computer, double\-click the file name or icon, and then follow the instructions in the wizard.

    If the setup fails, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] displays the end\-user recovery permissions update failed alert.

3.  When using the end\-user recovery functionality of [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)], disable the local shadow copies on the protected server.


