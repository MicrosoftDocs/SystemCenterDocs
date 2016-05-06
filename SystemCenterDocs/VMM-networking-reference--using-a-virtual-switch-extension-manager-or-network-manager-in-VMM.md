---
title: VMM networking reference: using a virtual switch extension manager or network manager in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb75bf3c-32bc-4e71-bcf5-e35f9caedb6e
---
# VMM networking reference: using a virtual switch extension manager or network manager in VMM
With [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)], if you add a virtual switch extension or network manager to [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], you can use the console for that virtual switch extension or network manager in a way that is coordinated with the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server. This helps you keep the settings that you see in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] synchronized with the settings that you configured through an interface other than [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

To do this, you must first install the provider software \(provided by the vendor\) on the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server. Then you can add the virtual switch extension or network manager to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

## Prerequisites
If you want to add a virtual switch extension or network manager to your configuration in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you must first perform the following tasks:

1.  Obtain provider software from the manufacturer of the virtual switch extension or network manager, install the provider on the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server, and then restart the System Center Virtual Machine Manager service. If you have installed a high\-availability [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server on a cluster, be sure to install the provider on all nodes of the cluster. For more information about installing the provider, refer to the manufacturer’s documentation.

2.  For your virtual switch extension or network manager, make sure that you know the manufacturer and model, the name of an account that has configuration permissions, the connection string, and the host groups to include. If certificates are used for the provider software, make sure you know how to view the thumbprint information for those certificates.

#### To add a virtual switch extension or network manager in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]

1.  Confirm that you have installed the necessary provider software. To do this, open the **Settings** workspace, and in the **Settings** pane, click **Configuration Providers**. In the **Configuration Providers** pane, review the list of installed provider software.

2.  Open the **Fabric** workspace.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Fabric** pane, expand **Networking**, and then click **Network Service**.

    Network services include gateways, virtual switch extensions, network managers, and top\-of\-rack \(TOR\) switches.

5.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Network Service**.

    The Add Network Service Wizard opens.

6.  On the **Name** page, type a name and optional description for the virtual switch extension or network manager, and then click **Next**.

7.  On the **Manufacturer and Model** page, in the **Manufacturer** list, select a provider manufacturer, in the **Model** list, select a model, and then click **Next**.

8.  On the **Credentials** page, either click **Browse** and then on the **Select a Run As Account** dialog box, select an account, or click **Create Run As Account** and create a new account. Then click **Next**.

9. On the **Connection String** page, in the **Connection string** box, type the connection string that is used by the virtual switch extension or network manager, and then click **Next**.

    For example, you might enter the connection string **mynetworkmanager1.contoso.com:443**.

    > [!IMPORTANT]
    > The syntax of the connection string is defined by the manufacturer of the virtual switch extension or network manager. For more information about the required syntax, refer to the manufacturer’s documentation.

10. If the **Certificates** page appears and certificates are listed, verify that the thumbprints of those certificates match the thumbprints of the certificates that are installed on the virtual switch extension or network manager. Then select the check box to confirm that the certificates can be imported to the trusted certificate store. Click **Next**.

    > [!NOTE]
    > If no certificates are listed, the connection string that was provided probably does not require certificates, and you can continue to the next page of the wizard. However, if no certificates are listed but your virtual switch extension or network manager requires them, confirm that the certificates were installed correctly on your device. Then, to refresh the display on the **Certificates** page of the wizard, click **Previous** and then click **Next**.

11. On the **Provider** page, in the **Configuration provider** list, select an available provider, and then click **Test** to use the selected provider to run basic validation tests against the virtual switch extension or network manager. If the tests indicate that the provider works as expected, click **Next**.

    Results that say **Passed** or **Failed** indicate whether the provider works as expected. One possible cause of failure is insufficient permissions in the Run As account. Results that say **Implemented** and **Not implemented** are informational only, and indicate whether the provider supports a particular API.

12. On the **Host Group** page, select one or more host groups to which the virtual switch extension or network manager will be available.

13. On the **Summary** page, review and confirm the settings, and then click **Finish**.

## See Also
[Prerequisites for gateways in VMM](./Prerequisites-for-gateways-in-VMM.md)
[VMM networking reference: adding a top-of-rack &#40;TOR&#41; switch in VMM](./VMM-networking-reference--adding-a-top-of-rack--TOR--switch-in-VMM.md)
[VMM networking reference: using an IPAM Server in VMM](./VMM-networking-reference--using-an-IPAM-Server-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](./VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


