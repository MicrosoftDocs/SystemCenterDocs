---
title: VMM networking reference: adding a top-of-rack (TOR) switch in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b1a2528-00f0-4d42-b045-635f4ba888c1
---
# VMM networking reference: adding a top-of-rack (TOR) switch in VMM
With System Center 2016 Technical Preview, you can add a top\-of\-rack \(TOR\) switch as a resource in Virtual Machine Manager \(VMM\). This helps you keep the settings in the TOR switch synchronized with the settings that you see in VMM.

To do this, you must first ensure that you have the necessary provider software on the VMM management server. If your switch is based on the Common Information Model \(CIM\) network switch profile, you can use the provider that is included in VMM in System Center 2016 Technical Preview. Otherwise, you must obtain the provider software that is provided by the switch vendor and install it on the VMM management server. Then you can add the TOR switch to VMM.

## Prerequisites
If you want to add a TOR switch to your configuration in VMM, you must first perform the following actions:

1.  Ensure that you have the necessary provider software on the VMM management server. If your switch is based on the Common Information Model \(CIM\) network switch profile, you can use the provider that is included in VMM in System Center 2016 Technical Preview. Otherwise, you must obtain the provider software that is provided by the switch vendor and install it on the VMM management server. After you install the provider software, restart the System Center Virtual Machine Manager service.

    If you have installed a high availability VMM management server on a cluster, ensure that the provider is installed on all nodes of the cluster.

    For more information about installing provider software, refer to the manufacturer’s documentation.

2.  For your TOR switch, make sure that you know the manufacturer and model, the name of an account that has configuration permissions, the connection string, and the host groups to include. If certificates are used for the provider software, make sure you know how to view the thumbprint information for those certificates.

#### To add a top\-of\-rack \(TOR\) switch in VMM

1.  If you installed provider software as part of fulfilling the “Prerequisites” that are listed before this procedure, confirm that the provider is listed in VMM. To do this, open the **Settings** workspace, and in the **Settings** pane, click **Configuration Providers**. In the **Configuration Providers** pane, review the list of installed provider software.

2.  Open the **Fabric** workspace.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Fabric** pane, expand **Networking**, and then click **Network Service**.

    Network services include gateways, virtual switch extensions, network managers, and TOR switches.

5.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Network Service**.

    The **Add Network Service Wizard** opens.

6.  On the **Name** page, enter a name and optional description, and then click **Next**.

7.  On the **Manufacturer and Model** page, make selections as follows:

    -   To use the provider software that is included in VMM, in the **Manufacturer** list, click **Microsoft**, and in the **Model** list, click **Microsoft Network Switch Profile Switch**.

    -   To use provider software that is provided by the switch vendor, click the appropriate **Manufacturer** and **Model** for your switch.

    Then click **Next**.

8.  On the **Credentials** page, either click **Browse** and then on the **Select a Run As Account** dialog box, select an account, or click **Create Run As Account** and create a new account. Then click **Next**.

9. On the **Connection String** page, in the **Connection string** box, type the connection string that is used by the TOR switch, and then click **Next**.

    For example, you might enter the following connection string:

    **https:\/\/TORswitch1.contoso.com:5986**

    > [!IMPORTANT]
    > If you are not using the provider software that is included in VMM, when you enter the connection string, use the syntax that is defined by the manufacturer of your TOR switch. For more information about the required syntax, refer to the manufacturer’s documentation.

10. On the **Certificates** page, if certificates are listed, verify that the thumbprints of those certificates match the thumbprints of the certificates that are installed on the TOR switch. Then select the box to confirm that the certificates can be imported to the trusted certificate store. Click **Next**.

    > [!NOTE]
    > If no certificates are listed, the connection string that was provided probably does not require a certificate, and you can continue to the next page of the wizard. However, if no certificates are listed but your TOR switch requires them, confirm that the certificates were installed correctly on your device.

11. On the **Provider** page, in the **Configuration provider** list, select an available provider, and then click **Test** to run basic validation against the TOR switch by using the selected provider. If tests indicate that the provider software works as expected, click **Next**.

12. On the **Host Group** page, select one or more host groups to which the TOR switch will be available.

13. On the **Summary** page, review and confirm the settings, and then click **Finish**.

## See Also
[Configuring Hyper-V host properties in VMM](Configuring-Hyper-V-host-properties-in-VMM.md)
[VMM networking reference: using a virtual switch extension manager or network manager in VMM](VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md)
[VMM networking reference: using an IPAM Server in VMM](VMM-networking-reference--using-an-IPAM-Server-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


