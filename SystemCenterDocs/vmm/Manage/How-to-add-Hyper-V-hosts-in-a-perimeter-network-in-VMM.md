---
title: How to add Hyper-V hosts in a perimeter network in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0cc143d-e618-4724-972e-323a0126798a
---
# How to add Hyper-V hosts in a perimeter network in VMM
You can use the following procedure to add existing Hyper-V hosts that are in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet) as managed Hyper-V hosts in Virtual Machine Manager (VMM). You can only add stand-alone hosts that are in a perimeter network. VMM does not support managing a host cluster in a perimeter network.

> [!NOTE]
> You can also use this procedure to add a stand-alone Hyper-V host that is in a workgroup and not part of a domain.

Before you can add a host that is on a perimeter network to VMM, you must install an agent locally on the server that you want to add.

### To install the VMM agent on the target host

1.  On the VMM product media or network share, right-click **Setup.exe**, and then click **Run as administrator**.

2.  On the Setup menu, under **Optional Installations**, click **Local Agent**.

3.  On the **Welcome** page, click **Next**.

4.  Review and accept the software license terms, and then click **Next**.

5.  On the **Destination Folder** page, accept the default location or click **Change** to specify a different location, and then click **Next**.

6.  On the **Security File Folder** page, do the following:

    1.  Select the **This host is on a perimeter network** check box.

    2.  In the **Security file encryption key** box, enter an encryption key, and then enter it again in the **Confirm encryption key** box.

        > [!IMPORTANT]
        > The encryption key is a value that you choose. We recommend that you enter an encryption key that contains a mix of uppercase and lowercase letters, numbers and symbols.

        > [!IMPORTANT]
        > Make note of the encryption key that you use to create the security file. You must enter this same key again when you add the host in the VMM console.

    3.  Either accept the default location where the encrypted security file will be stored, or click **Change** to specify a different location to store the encrypted security file.

        > [!IMPORTANT]
        > Make note of the location where you stored the security file. In the “To ensure that the Security.txt file is available to VMM” procedure, you must transfer the security file to a location that is accessible to the computer on which a VMM console is installed.

    4.  To use a certificate to encrypt communications between the VMM management server and the host, select the **Use a CA signed certificate for encrypting communications with this host** check box. In the **Thumbprint of the certificate** box, enter the thumbprint of the certificate.

        > [!NOTE]
        > To obtain the thumbprint of a certificate, open the Certificates snap-in, and then select **Computer account**. In the Certificates snap-in, locate and then double-click the certificate that you want to use. On the **Details** tab, select the **Thumbprint** field. In the lower pane, highlight the thumbprint value, and then press Ctrl+C to copy the value to the clipboard.

    5.  When you are finished, click **Next**.

7.  On the **Host network name** page, specify how the VMM management server will contact the host, and then click **Next**. You can select either of the following options:

    -   **Use local computer name**

    -   **Use IP address**

    If you select **Use IP address**, click an IP address in the list.

    > [!IMPORTANT]
    > Make note of the computer name or IP address of the host. You must enter this same information again when you add the host in the VMM console.

8.  On the **Configuration settings** page, accept the default port settings, or specify different ports, and then click **Next**.

    > [!IMPORTANT]
    > We recommend that you do not change the default port 5986 for agent communication. The port settings that you assign for the agent must identically match the port setting that the VMM management server uses. By default, the VMM management server uses port 5986 for agent communication with hosts in a perimeter network, and port 443 for file transfers.

9. On the **Ready to install** page, click **Install**.

### To ensure that the SecurityFile.txt file is available to VMM

1.  On the target host, navigate to the folder where the security file is stored. By default, the location is C:\Program Files\Microsoft System Center 2012\Virtual Machine Manager. The name of the security file is SecurityFile.txt.

2.  Transfer the security file to a location that is accessible to the computer on which a VMM console is installed. For example, transfer the file to the computer where the VMM console is installed, to an internal file share, or to a USB flash drive.

### To add the Hyper-V host in the perimeter network

1.  In the VMM console, open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**.

3.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Hyper-V Hosts and Clusters**.

    The Add Resource Wizard starts.

4.  On the **Resource location** page, click **Windows Server computers in a perimeter network**, and then click **Next**.

5.  On the **Target resources** page, do the following:

    1.  In the **Computer name** box, enter the NetBIOS name or the IP address of the host in the perimeter network.

    2.  In the **Encryption key** box, enter the encryption key that you created when you installed the agent on the target host.

    3.  In the **Security file path** box, enter the path of the **SecurityFile.txt** file, or click **Browse** to locate the file.

    4.  In the **Host group** list, click the host group where you want to add the host.

        For example, click the **Seattle\Tier2_SEA** host group.

    5.  Click **Add**.

        The computer is listed under **Computer Name** in the lower pane.

    6.  Repeat this step to add other hosts in the perimeter network. When you are finished, click **Next**.

6.  On the **Host settings** page, in the **Add the following path** box, enter the path on the host where you want to store the files for virtual machines that are deployed on hosts, and then click **Add**. If you leave the box empty, the default path of %SystemDrive%\ProgramData\Microsoft\Windows\Hyper-V is used. Be aware that it is a best practice not to add default paths that are on the same drive as the operating system files.

    Repeat this step if you want to add more than one path. When you are finished, click **Next**.

    > [!NOTE]
    > You can ignore the **Reassociate this host with this Virtual Machine Manager environment** check box. This setting does not apply to hosts in a perimeter network.

7.  On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears to show the job status. Make sure that the job has a status of **Completed**, and then close the dialog box.

8.  To verify that the host was successfully added, in the **Fabric** pane, expand **Servers**, expand **All Hosts**, expand the host group where you added the host, and then click the host. In the **Hosts** pane, verify that the host status is **OK**.

    > [!TIP]
    > To view detailed information about host status, right-click the host in the VMM console, and then click **Properties**. On the **Status** tab you can view the health status for different areas such as overall health, host agent health, and Hyper-V role health. If there is an issue, you can click **Repair all**. VMM will to try to automatically fix the issue.

## See Also
[Adding Windows servers as Hyper-V hosts or host clusters in VMM](Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


