---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to add and classify SMI S and SMP storage devices in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  96db0f54-5b56-426a-9866-9e3b0902609c
---

# How to add and classify SMI-S and SMP storage devices in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Use the following procedure to add remote storage devices in Virtual Machine Manager (VMM). You can add and discover external storage arrays that are managed by Storage Management Initiative � Specification (SMI-S) or Store Management Provider (SMP) providers. You can assign friendly-name classifications for the added storage. For example, you can assign a Gold classification to solid-state drive (SSD) storage and a Bronze classification to slower drives.

**Account requirements** To complete this procedure, you must be a member of the Administrator user role, or a member of the Delegated Administrator user role.

Before you begin this procedure, verify the following prerequisites:

-   Ensure that you are using a supported storage array. For a list of supported arrays, see the "Supported Storage Arrays" section of the topic [Configuring Storage in VMM](assetId:///55836f52-ebe1-4b5a-a37b-b29d4bb2c355).

-   To add an SMI-S storage device, ensure that you have installed the SMI-S provider for the array on a server that the VMM management server can access over the network by IP address or by fully qualified domain name (FQDN). For information about how to obtain SMI-S providers, see [Configuring iSCSI Target Server and the SMI-S Provider in VMM](Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md).

    > [!NOTE]
    > Do not install the SMI-S provider on the VMM management server. This configuration is not supported.
    > 
    > WMI SMP providers from Dell EqualLogic and NexSan must be installed on the VMM server.

-   You can create a Run As account before or while you are run the Add Storage Devices Wizard to discover storage. The Run As account must have permissions to access the SMI-S provider. You can create a Run As account in the **Settings** workspace. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

Use the following procedures to add and classify block storage devices:

-   [To discover storage devices](#BKMK_Discover)

-   [To change the storage classification for a storage pool](#BKMK_changeclass)

## <a name="BKMK_Discover"></a>To discover storage devices

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  On the **Home** tab, click **Add Resources**, and then click **Storage Devices** to start the Add Storage Devices Wizard.

4.  On the **Select Provider Type**  page, select one of the following:

    1.  Select the **Add a storage device that is managed by an SMI-S provider** check box to specify and discover a storage device or an array that is supported by the SMI-S protocol.

    2.  Select **Add a storage device that is managed by an SMP provider** to specify and discover a storage device or an array that is supported by the SMP protocol.

5.  On the **Specify Discovery Scope** page, do the following:

    1.  If you are adding an SMI-S provider storage device, do the following:

        1.  In the **Protocol** list, select one of the following:

            -   **SMI-S CIMXML** Choose this option to specify the SMI-S CIMXML-based storage provider that can be used to manage the storage devices.

            -   **SMI-S WMI WMI** Choose this option to specify the SMI-S WMI-based storage provider that can be used to manage the storage devices.

        2.  In the **Provider IP address or FQDN** box, enter either the IP address or the FQDN of the storage provider.

        3.  In the **TCP/IP port** box, enter the port number that is used to connect to the provider.

        4.  Select the **Use Secure Sockets Layer (SSL) connection** check box to enable HTTPS for communicating with the SMI-S CIMXML provider. This setting is not available for the SIM-S WMI protocol.

        5.  Next to the **Run As account** box, click **Browse**, and select a Run As account that can access the storage provider. If you do not have an account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    2.  To add an SMP provider, select it from the **Provider** list. If the SMP provider is not in the list, click **Import** to refresh the list.

6.  On the **Gather Information** page, VMM automatically tries to discover and import the storage device information. To retry discovery, click **Scan Provider**. Note the following if you selected the option to use an SSL connection for an SMI-S provider:

    1.  During discovery, the **Import Certificate** dialog box appears. Review the certificate information for the storage provider, and then click **Import**.

    2.  By default, when you import a certificate for a storage provider, verification of the common name (CN) that is used in the certificate occurs. However, this process might cause an issue where storage discovery fails when the certificate does not contain a CN value, or the CN value does not match the expected format of NetBIOS name, FQDN, or IP address that VMM uses.

    3.  If you receive the error messages "SSL certificate common name is invalid" or "Certificate Authority not recognized", you must disable CN verification for the storage provider certificate in the registry. To do this, follow these steps on the VMM management server:

        > [!WARNING]
        > This task contains steps that indicate how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, ensure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up the registry, which is included in the system state, see [Windows Server Backup](http://technet.microsoft.com/library/cc770757.aspx).

        1.  Click **Start**, type **regedit** in the **Search programs and files** box, and then press ENTER.

        2.  In the **User Account Control** dialog box, click **Yes** to continue.

        3.  In Registry Editor, locate, and then click the following registry subkey:

            **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Storage Management/**

        4.  On the **Edit** menu, point to **New**, and then click **DWORD (32-bit) Value**.

        5.  Type **DisableHttpsCommonNameCheck**, and then press ENTER.

        6.  Double-click **DisableHttpsCommonNameCheck**.

        7.  In the **Value data** box, type a value of **1**, and then click **OK**.

        8.  Close Registry Editor.

    If the discovery process succeeds, the discovered storage arrays, storage pools, manufacturer, model, and capacity are listed on the page. When the process finishes, click **Next**.

7.  On the **Select Storage Devices** page, do the following for each storage pool that requires a classification:

    1.  Select the check box next to a storage pool that you want VMM to manage.

    2.  In the **Classification** column, select the storage classification that you want to assign. For instructions about how to create a new classification, see [How to create storage classifications in VMM](How-to-create-storage-classifications-in-VMM.md). Then click **Next**.

8.  On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Ensure that the job has a status of **Completed**, and then close the dialog box.

9. To verify the newly discovered storage information, in the **Fabric** workspace, on the **Home** tab, click **Fabric Resources**. In the **Fabric** pane, expand the **Storage** node, and then do any of the following:

    -   To view the storage pools that are assigned to a classification, click **Classifications and Pools**, and then expand the classification where you added storage. Expand a storage pool to view logical unit information for the pool.

    -   To view storage provider information, click **Providers**. You can view the storage provider name, management address, managed arrays, and the provider status.

    -   To view discovered storage arrays, click **Arrays**. You can view the name of the array, total and used capacity, the number of managed storage pools, the provider name, and the provider status.

## <a name="BKMK_changeclass"></a>To change the storage classification for a storage pool

1.  In the **Fabric** workspace, expand **Storage**, and then click **Classification and Pools**.

2.  In the **Classifications, Storage Pools and Logical Units** pane, expand the storage classification that contains the storage pool that you want to reclassify.

3.  Right-click the storage pool that you want to reclassify, and then click **Properties**.

4.  In the **Classification** list, click the classification that you want to assign, and then click **OK**.

## See Also
[Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



