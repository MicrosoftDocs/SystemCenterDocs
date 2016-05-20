---
title: How to discover and classify Virtual Fibre Channel Fabrics with VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44b64f8d-5590-4e04-a469-905c39ca771a
---
# How to discover and classify Virtual Fibre Channel Fabrics with VMM
You can discover and add Virtual Fibre Channel storage fabrics to manage in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] for [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]. You can also assign classifications to the added fabrics.

Before you begin, verify the following prerequisites:

-   Ensure you are a member of the Administrator user role, or a member of the Delegated Administrator user role.

-   Ensure you have installed the SMI\-S provider for the device on a server that the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server can access over the network by IP address or FQDN. For information about how to obtain SMI\-S providers, see [Configuring Storage Overview](assetId:///55836f52-ebe1-4b5a-a37b-b29d4bb2c355).

    > [!NOTE]
    > Do not install the SMI\-S provider on the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server. This configuration is not supported.

### To discover and classify Fibre Channel fabrics

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  On the **Home** tab, click **Add Resources**, and then click **Storage Devices** to start the **Add Storage Devices Wizard**.

4.  On the **Select Provider Type**  page, select **Fibre Channel fabric discovered and managed by a SMI\-S provider**.

5.  On the **Specify Discovery Scope** page, do the following:

    1.  In the **Provider IP address or FQDN** box, enter either the IP address or the FQDN of the storage provider.

    2.  In the **TCP\/IP port** box, enter the port number that is used to connect to the provider.

    3.  If required, select **Use Secure Sockets Layer \(SSL\) connection** to enable HTTPS for communicating with the provider.

    4.  Next to the **Run As account** box, click **Browse**, and select a Run As account that can access the storage provider. If you do not have an account. click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account** and follow the instructions.

6.  On the **Gather Information** page, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] automatically discovers and imports the Fibre Channel fabric information. If the discovery process succeeds, the discovered fabric name, switches and fabric World Wide Node Names \(WWNN\) are listed on the page. When the process successfully completes, click **Next**. To retry the discovery process for an unsuccessful attempt, click **Scan Provider**.

    **Note**: If you selected the SSL connection, the following occurs:

    1.  During discovery the **Import Certificate** dialog box appears. Review the certificate information for the storage provider, and then click **Import**.

    2.  By default, when you import a certificate for a storage provider, verification of the common name \(CN\) that is used in the certificate occurs. However, this may cause an issue where storage discovery fails when the certificate does not contain a CN value, or the CN value does not match the expected format of NetBIOS name, FQDN or IP address that [!INCLUDE[vmm12short](Token/vmm12short_md.md)] uses.

7.  On the **Fibre Channel Fabrics** page, do the following for each storage fabric that requires a classification:

    1.  In the **Storage Device** column, select the check box next to a Fibre Channel fabric that you want [!INCLUDE[vmm12short](Token/vmm12short_md.md)] to manage.

    2.  In the **Classification** column, select the classification that you want to assign to the fabric. For instructions on creating a new fabric classification, see [Overview: storage classifications in VMM](Overview--storage-classifications-in-VMM.md). When finished, click **Next**.

    > [!NOTE]
    > The fabric classification task is separate from that for storage classification, although the concept is similar.

8.  On the **Summary** page, confirm the settings, and then click **Finish**.

## See Also
[Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


